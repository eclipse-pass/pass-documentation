# Code Coverage

This section details how PASS utilizes JaCoCo for measuring Java code coverage in [PASS Core](https://github.com/eclipse-pass/pass-core)
and [PASS Support](https://github.com/eclipse-pass/pass-support). Unit and Integration tests exist in PASS UI as well, but 
at the moment do not have any code coverage analysis being performed. We anticipate adding code coverage reports to PASS
UI in the future.

## Summary

PASS employs [JaCoCo (Java Code Coverage Library)](https://www.jacoco.org/jacoco/) to measure the extent to which the 
project's Java code is exercised by unit and integration tests.

This process typically runs as part of the standard build cycle managed by our build tool (Maven) within the 
CI/CD pipeline (GitHub Actions). JaCoCo generates reports, which are then consumed by SonarQube Cloud to display 
coverage metrics on the project dashboard and pull request analyses. Tracking code coverage helps ensure that critical 
parts of the application are adequately tested, increasing confidence in code quality and reducing the risk of 
regressions.

## Knowledge Needed / Skills Inventory

* Understanding Code Coverage Concepts
* Java 17+
* Maven build tool

## Technologies Utilized

* [JaCoCo](https://www.jacoco.org/jacoco/)
* Build Tool [Maven](https://maven.apache.org/)
* [GitHub Actions](https://docs.github.com/en/actions)
* [SonarQube Cloud](https://www.sonarsource.com/products/sonarqube/)

## Technical Deep Dive

The PASS project integrates JaCoCo within the CI/CD pipeline. Achieving this involves two main steps: configuring JaCoCo
reports in Maven and integrating the analysis within GitHub Actions.

## Setting up the POM

Both PASS Core and PASS Support are multi-module projects which require a specific setup  

* Agent Preparation: The JaCoCo Java agent is configured to run before the test execution phase. This is done using the
`prepare-agent` goal in the parent `pom.xml`. 
* Aggregate Report Module: A module is designated as the aggregate report module, which collects all the reports from 
the individual modules in the project. This module's `pom.xml` runs the `report-aggregate` goal during the `verify` 
stage. This module is named:
  * for PASS Core: `jacoco-aggregate-report-pass-core`
  * for PASS Support: `jacoco-aggregate-report-pass-support`
* Individual modules must declare the `prepare-agent` goal in their `pom.xml`
* SonarQube
  * The SonarQube Scanner is added to the parent `pom.xml`
  * The following properties are added to the parent `pom.xml`:
    * `sonar.projectName`
    * `sonar.projectKey`
    * `sonar.coverage.jacoco.xmlReportPaths`
* Report Generation: The report is saved in `jacoco-aggregate-report-[project-name]/target/site/jacoco.xml`

## GitHub Actions

The integration with SonarQube also occurs during the CI/CD phase of the build process. To accomplish this integration 
the following steps were implemented in GitHub Actions:

* A `SONAR_TOKEN` secret, obtained from SonarQube Cloud, must be configured in the eclipse-pass GitHub organization
secrets.
* In the `snapshot.yml` and `ci.yml` of `eclipse-pass-parent` the SonarQube Scanner is invoked during the `mvn` `deploy`
and `verify`.
* The `fetch-depth` must have a value of 0, so that the entire Git history is fetched. If this isn't set then incomplete
analysis will be performed.

## Other Configurations to Note

* Using GitHub Actions requires the `Automatic Analysis` to be turned off on the project in SonarQube so that GitHub 
Actions can trigger analysis.
* A SonarQube project was created for `eclipse-pass-parent`. With 'Automatic Analysis' disabled in SonarCloud, all scans
rely on GitHub Actions triggers. Since the primary workflows may focus only on pull request analysis, linking 
`eclipse-pass-parent` is a necessary part of the configuration that enables analysis results for the `main` branch 
(of Core/Support) to be processed and displayed in SonarQube. Additionally, this allows the `eclipse-pass-parent` 
project itself to be analyzed for code quality and dependency vulnerabilities.

## Related Information

* [JaCoCo Official Website](https://www.jacoco.org/jacoco/)
* [JaCoCo Maven Plugin Documentation](https://www.jacoco.org/jacoco/trunk/doc/maven.html)
* [PASS SonarQube Documentation](sonar-qube.md)
* [SonarQube Cloud Code Coverage Integration](https://docs.sonarsource.com/sonarqube-cloud/enriching/test-coverage/java-test-coverage/)