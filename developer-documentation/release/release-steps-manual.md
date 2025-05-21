# Manual Release

This section provides the details on performing a release one project at a time manually by the release manager.

**[Publish: Release All](https://github.com/eclipse-pass/main/actions/workflows/pass-complete-release.yml) GitHub Action workflow is the preferred way to release PASS. Releasing PASS manually should only be done if absolutely required.**

## Required Software

The following software is required:

| Name           | Version |
|----------------|---------|
| Java           | 17      |
| Maven          | 3.8.x   |
| Docker         | 20.10.x |
| Docker Compose | 2.x     |
| Git            |         |

### Sonatype

Developers will need a Sonatype Central Portal account to release Java projects.
Maven must be configured to use the account by modifying your `~/.m2/settings.xml`. To learn more about Sonatype, documentation is available on their [website](https://central.sonatype.org/publish/publish-portal-guide/).

Example pom setup:
```xml
<settings>
  <servers>
    <server>
      <id>central</id>
      <username>YOUR_SONATYPE_USERNAME</username>
      <password>YOUR_SONATYPE_PASSWORD</password>
    </server>
  </servers>
  <profiles>
    <profile>
      <id>central</id>
      <activation>
        <activeByDefault>true</activeByDefault>
      </activation>
      <properties>
        <gpg.executable>gpg</gpg.executable>
        <gpg.passphrase>YOUR_GPG_PASSPHRASE</gpg.passphrase>
      </properties>
    </profile>
  </profiles>
</settings>

```
### GitHub Container Registry (GHCR)

Developers will need a GitHub account which is a member of the [eclipse-pass](https://github.com/eclipse-pass) organization.

## Release Sequence

If a manual release is required, a specific order must be followed. The Java projects must follow a strict sequence, following its dependency hierarchy. Other Javascript based projects can be released in any order. Both the Java and non-Java releases can be done in parallel, as there are no direct code dependencies between them.

1. [`main`](https://github.com/eclipse-pass/main)
2. Java projects
    1. [`pass-core`](https://github.com/eclipse-pass/pass-core)
    2. [`pass-support`](https://github.com/eclipse-pass/pass-support)
3. Non-Java projects
    * [`pass-ui`](https://github.com/eclipse-pass/pass-ui)
    * [`pass-acceptance-testing`](https://github.com/eclipse-pass/pass-acceptance-testing)
4. [`pass-docker`](https://github.com/eclipse-pass/pass-docker)

## Java Release

Maven is used to perform many of the release tasks:

* Sets versions and builds
* Tests
* Pushes release artifacts
* May also build Docker images

The versions of all the Java artifacts are the same for a release. The parent pom in `main` sets the version to be inherited by all its children; therefore this project needs to be released first, as all other projects need to reference it. After this project is released, other projects are released in an order which guarantees that all PASS dependencies for them have already been released. You will need to wait for artifacts to show up in Maven Central before building a module which depends on them.

For convenience, we set and export environment variables RELEASE for the release version, and NEXT for the next development version; e.g., `export RELEASE=0.1.0` and `export NEXT=0.2.0-SNAPSHOT`.
For each of these child projects, we first clone the source from GitHub, and operating on the principal branch (usually `main`).

Update the reference to the parent pom and set the release version.
```
mvn versions:update-parent -DparentVersion=$RELEASE
mvn versions:set -DnewVersion=$RELEASE
```

After this, we do build and push the artifacts to Sonatype, commit the version change, and tag it:
```
mvn -ntp -P release clean deploy
git commit -am "Update version to $RELEASE"
git tag $RELEASE
```

Push any created images to GHCR after logging in. Visit the GitHub docs [Working with the Container registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry) for more information.
```
docker push IMAGE_NAME:$RELEASE
```

Push commits and tags to GitHub:
```
git push origin
git push origin --tags
```

Finally, the new development code needs to be built and pushed to GitHub. Repeat the process above with the dev version, but do not create the tag.

At this point, we should have deployed the release to Sonatype (and eventually to Maven Central), pushed a tag to GitHub, and deployed the new development release to Sonatype.

In addition, the project may be released on GitHub. This provides a way to add release notes for a particular project. A GitHub release is done manually by uploading artifacts through the UI. The release version and tag should be the same used for Maven Central. Release notes can be automatically generated from commit messages and then customized.

See the GitHub [Java Release Workflow](https://github.com/eclipse-pass/main/blob/main/.github/workflows/release.yml) for the details on the exact commands that are run.

### Manual Release Steps for Main, Pass-Core, Pass-Support

* Update POM to release version
* Commit release version update
* Tag release version
* Build and deploy to Sonatype
* Push any generated Docker images to GHCR
* Update POM to dev version
* Commit dev version update
* Build and deploy to Sonatype
* Wait for artifacts in Maven Central
* Push any generated Docker images to GHCR
* Push commits to GitHub

## JavaScript Projects

The following projects can be released by performing the following steps when the release needs to be performed manually.

### PASS-UI

Update the version in `package.json` and in `build.sh`, and commit those changes via a PR to the `pass-ui` repo.

Build a new docker image from within the `pass-ui` repo by running:
```
sh build.sh ~/pass-docker/.env
```
Note, you might want to ensure `node_modules` are removed first to ensure a clean build.

Push that image to GHCR. For example: `docker push ghcr.io/eclipse-pass/pass-ui:<your-version-tag-here>`

### PASS-Acceptance Testing

All that's required is to tag a new release in the GitHub UI.

After pushing the images to GHCR, update the appropriate image lines in `docker-compose.yml` and `pass-docker` with the new version. Open a pull request against `pass-docker` with these updates.

Once acceptance-tests successfully run in CI in your `pass-docker` PR, and once you've done some additional manual spot checking while running `pass-docker` locally, go ahead and tag a new release in the GitHub UI for each of the following projects: `pass-ui` and `pass-acceptance-testing`.

## Testing

Manual testing can be done using the newly updated pass-docker to run the release locally. Acceptance testing is run automatically on GitHub against pass-docker/main.

## Post Release

* Update release notes
* Update project documentation

### Update Release Notes

1. Ensure that there is a milestone for the release.
2. Get a list of all issues that are closed and in the `eclipse-pass` project by going to the [main repository issue list](https://github.com/eclipse-pass/main/issues?page=1&q=is%3Aissue+is%3Aclosed+project%3Aeclipse-pass%2F4).
3. Check that the correct tickets are in the release milestone.
4. Archive the release tickets in the Project by going to the [Kanban Board](https://github.com/orgs/eclipse-pass/projects/4/views/2), scrolling to the Done column, verifying that all tickets in the list have the new version tag, then selecting the ellipsis button and "Archive all cards".
5. Include in the Release Notes a link to the issues resolved by the release, for example [this milestone](https://github.com/eclipse-pass/main/milestone/11?closed=1).
