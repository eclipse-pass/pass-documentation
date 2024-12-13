# Operations/Production - Eclipse Operations

PASS is an Eclipse Foundation project and benefits from the resources and knowledge that the Eclipse Foundation has to 
offer. One of those resources is the Eclipse GH repository configuration.

## Eclipse GitHub Repository Configuration

The [.eclipsefdn](https://github.com/eclipse-pass/.eclipsefdn) repository enables the team committers to
[self-service several aspect of the eclipse organization](https://www.eclipse.org/projects/handbook/#resources-github-self-service)
via a tool called [Otterdog](https://otterdog.readthedocs.io).

These [.eclipsefdn](https://github.com/eclipse-pass/.eclipsefdn) repo / tools gives access to:

* Organization settings
* Organization webhooks
* Repositories and their settings
* Branch protection rules

If a setting is not supplied in the `eclipse-pass.jsonnet` file it will default to a value. The full set of default 
values are on the Eclipse managed [otterdog-defaults.libsonnet](https://github.com/EclipseFdn/otterdog-defaults/blob/main/otterdog-defaults.libsonnet).

Learn more about [Otterdog here](https://otterdog.readthedocs.io/en/latest/).

### Workflow for Updating the Otterdog Configuration 

To make changes to the Otterdog configuration in the [.eclipsefdn](https://github.com/eclipse-pass/.eclipsefdn)
repository, follow these steps:

1. Fork the [.eclipsefdn](https://github.com/eclipse-pass/.eclipsefdn) repository into your own GitHub account.
2. Make changes to the `eclipse-pass.jsonnet` file.
3. Push those changes to the upstream repository.
4. Create a pull request in the `.eclipsefdn` repository. 
5. An automated workflow will run, displaying the changes to be applied and validating that the configuration is 
correctly formatted and structured.
6. Depending on the type of changes one or more Eclipse engineers will review the PR. Additionally, the project lead's 
approval may also be required based on the nature of the changes.

## Eclipse Contributor Agreement and Eclipse Development Process

Contributors of the project must electronically sign appropriate documents in order to become committers. The following
are agreements and policies by Eclipse that a committer must read:

* [Eclipse Contributor Agreement (ECA)](https://www.eclipse.org/legal/eca/)
* [Eclipse Development Process (EDP)](https://www.eclipse.org/projects/dev_process/)

## ECA for Pass Documentation

ECA is not configured as a required check for merging in `pass-documentation`, therefore PRs can be merged with a 
non-committer. In addition, the EDP explicitly states: "you can merge if you know that the user associated with the 
commit has signed an ECA", therefore if a user with a different GitHub account with a different email address from their
Eclipse committer account, is still able to merge PRs with those commits. This applies to GitBot (GitBook GitHub bot), 
and Eclipse recognizes this account for making commits.