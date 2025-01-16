# Latest Release

We publish the latest release of PASS Core, Pass Support (Data Loaders, Deposit Services, Notification Services), PASS UI, and other supporting repositories to [GitHub](https://github.com/eclipse-pass). The artifacts from the Java based components are also published to a [Sonatype Maven Central Repository](https://central.sonatype.com/artifact/org.eclipse.pass/eclipse-pass-parent). Release announcements are made using a [Google Groups](https://groups.google.com/g/pass-general) mailing list, these announcements provide a brief summary highlighting the features, updates, and bug fixes that went into the release.

### GitHub

* [PASS Parent (aka main)](https://github.com/eclipse-pass/main/releases)
* [PASS Core](https://github.com/eclipse-pass/pass-core/releases)
* [PASS Support](https://github.com/eclipse-pass/pass-support/releases)
* [PASS UI](https://github.com/eclipse-pass/pass-ui/releases)
* [PASS Docker](https://github.com/eclipse-pass/pass-docker/releases)
* [Pass Acceptance Testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases)
* [Pass Documentation](https://github.com/eclipse-pass/pass-documentation/releases)

### Sonatype

During our release the Java based component artifacts for PASS are published to Sonatype Maven Central Repository:

* [PASS Parent](https://central.sonatype.com/artifact/org.eclipse.pass/eclipse-pass-parent)
* [PASS Core](https://central.sonatype.com/artifact/org.eclipse.pass/pass-core)
* [PASS Support](https://central.sonatype.com/artifact/org.eclipse.pass/pass-support)

### SBOM

As of release `1.13.0`, a [CycloneDX Software Bill Of Materials (SBOM)](https://cyclonedx.org/specification/overview/) is created and published for the following artifacts:

* [pass-core-main](https://repo1.maven.org/maven2/org/eclipse/pass/pass-core-main/)
* [deposit-core](https://repo1.maven.org/maven2/org/eclipse/pass/deposit/deposit-core/)
* [pass-notification-service](https://repo1.maven.org/maven2/org/eclipse/pass/pass-notification-service/)
* [pass-grant-loader](https://repo1.maven.org/maven2/org/eclipse/pass/pass-grant-loader/)
* [pass-journal-loader-nih](https://repo1.maven.org/maven2/org/eclipse/pass/pass-journal-loader-nih/)
* [nihms-data-harvest](https://repo1.maven.org/maven2/org/eclipse/pass/nihms-data-harvest/)
* [nihms-data-transform-load](https://repo1.maven.org/maven2/org/eclipse/pass/nihms-data-transform-load/)
* [pass-data-client](https://repo1.maven.org/maven2/org/eclipse/pass/pass-data-client/)
* [pass-ui (Located in the / directory of the docker image)](https://github.com/eclipse-pass/pass-ui/pkgs/container/pass-ui)
