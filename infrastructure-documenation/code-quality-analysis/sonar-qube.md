# PASS Code Quality

PASS uses the code quality and security tool [SonarQube Cloud](https://www.sonarsource.com/products/sonarqube/) to 
ensure a high-quality code base. SonarSource graciously allows open source projects to use a free tier of SonarQube 
Cloud, which integrates directly with our GitHub repositories.

## Summary

SonarQube performs static analysis on the PASS codebase to detect bugs, vulnerabilities, code smells, and security 
hotspots. By integrating SonarQube with our GitHub repositories, we are able to get code quality checks on our pull 
requests and promote clean code. Analysis is triggered automatically on pull requests and merges to the main branch via
GitHub Actions. In addition, a [plugin](https://docs.sonarsource.com/sonarqube-for-ide/intellij/) can be added to 
various IDEs, catching code quality issues before submitting a pull request.

### List of Repositories on SonarQube

* [PASS Main](https://sonarcloud.io/project/overview?id=eclipse-pass_main)
* [PASS Core](https://sonarcloud.io/project/overview?id=eclipse-pass_pass-core)
* [PASS Support](https://sonarcloud.io/project/overview?id=eclipse-pass_pass-support)
* [PASS UI](https://sonarcloud.io/project/overview?id=eclipse-pass_pass-ui)

## Knowledge Needed / Skills Inventory

* Understanding code quality concepts
* Git/GitHub

## Technologies Utilized

* [SonarQube Cloud](https://www.sonarsource.com/products/sonarqube/): The cloud-based platform hosting the analysis 
engine and results dashboard.
* [GitHub Actions](https://docs.github.com/en/actions): publishes results to SonarQube Cloud via workflows.
* [SonarScanner](https://docs.sonarsource.com/sonarqube-cloud/advanced-setup/ci-based-analysis/sonarscanner-for-maven/):
The analysis tool that scans the code.
  * [SonarScanner GitHub](https://github.com/SonarSource/sonar-scanner-cli)

## Technical Deep Dive

### SonarQube Configuration

The full documentation to getting starting with SonarQube Cloud is available on their [documentation site](https://docs.sonarsource.com/sonarqube-cloud/getting-started/sign-up/).

### Reading the Reports

Access the SonarQube reports using the links in the [Summary](#list-of-repository-on-sonarqube) section. Analyzing the
reports [documentation](https://docs.sonarsource.com/sonarqube-cloud/digging-deeper/overview/) is on the SonarQube Cloud
documentation site.

Key areas to examine include:

* Project Overview: The main dashboard page shows:
    * Quality Gate status (Passed/Failed) – this is the primary indicator of code health.
    * The main **Ratings** (A-E) for Reliability, Security, Maintainability, and the **Coverage** percentage for
    a quick code coverage assessment.
* Pull Request Analysis (via GitHub):
    * When analysis runs on a pull request, SonarCloud adds a status check to the PR in GitHub.
* On a specific project:
  * Issues Tab:
      * Provides a detailed, filterable list of all identified issues.
      * Filter by type (Bug, Vulnerability, Smell, Hotspot), severity (Blocker, Critical, Major, Minor, Info), 
      status (Open, Confirmed, False Positive, Won't Fix), assignment, creation date, etc.
  * Measures Tab:
      * Explore metrics in more detail. View graphs showing trends over time for size, complexity, coverage, technical 
      debt, and issue counts.
      * Useful for understanding the overall health trends of the codebase.
  * Code Tab:
      * Browse the source code directly within SonarCloud.
      * Issues are highlighted inline, making it easy to see problems in context.

### Integration with JaCoCo

SonarQube does not provide code coverage out-of-the-box, but does integrate with it. In a simple project, the [setup](https://docs.sonarsource.com/sonarqube-cloud/enriching/test-coverage/java-test-coverage/)
is trivial, but with the PASS project there are a few extra configuration steps that are necessary in order for 
SonarQube to be integrated with our CI/CD pipeline. Those extra steps are detailed in the [JaCoCo page](jacoco.md) of 
the code quality analysis.

### Known Limitations using Free Tier Subscription

* Can only analyze the `main` branch and pull requests (only if `main` is the target branch) of a repository.
* Can only use the default [Sonar way quality gate](https://docs.sonarsource.com/sonarqube-cloud/standards/managing-quality-gates/)
for code quality analysis
* Maximum number of organization members is 5. 

The full set of limitations for SonarQube Cloud can be found on their [subscription comparison table](https://docs.sonarsource.com/sonarqube-cloud/administering-sonarcloud/managing-subscription/subscription-plans/).

## Related Information

* [SonarQube Cloud Homepage](https://www.sonarsource.com/products/sonarqube/)
* [SonarQube Cloud Documentation](https://docs.sonarsource.com/sonarqube-cloud/)