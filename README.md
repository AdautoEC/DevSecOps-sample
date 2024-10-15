# DevSecOps Pipeline - GitHub Actions

DevSecOps Pipeline using free SAST, DAST, and SCA tools for comprehensive security scanning.

## How it works?

This GitHub Action pipeline runs multiple security tools, including **SonarCloud**, **Semgrep**, **Snyk**, **Dependency-Check**, **OWASP ZAP**, and **Dastardly**. The goal is to check for security vulnerabilities both in your codebase and in third-party dependencies, and to identify security issues during dynamic application testing.

### SCA - Software Composition Analysis

Provided by **Snyk** and **Dependency-Check**, these steps analyze third-party dependencies for known vulnerabilities.
- **Snyk**: All you need is a Snyk account, and the Snyk token must be added as a secret (`SNYK_TOKEN`).
- **Dependency-Check**: This tool also helps to identify vulnerabilities in third-party libraries, based on CVSS scores.

### SAST - Static Application Security Testing

This pipeline includes two static analysis tools:
- **SonarCloud**: The SaaS version of SonarQube for analyzing your code's security and quality. You'll need to create a SonarCloud account and add the Sonar token as a secret (`SONAR_TOKEN`). Make sure to add the `sonar-project.properties` file to the repository root.
- **Semgrep**: A fast, customizable static analysis tool that looks for code vulnerabilities. It requires adding the `SEMGREP_APP_TOKEN` secret.

### DAST - Dynamic Application Security Testing

- **OWASP ZAP**: This open-source tool from OWASP performs automated scans of your deployed application to find security issues in web applications. It runs a scan on the application after deployment, leveraging the Automated Scanning feature of ZAP.
- **Dastardly**: Provided by PortSwigger, Dastardly performs dynamic security tests focused on finding common vulnerabilities in web applications.

### Pipeline Workflow

1. **SAST Tools**:
    - **SonarCloud** and **Semgrep** scan your codebase for security vulnerabilities and code quality issues.

2. **SCA Tools**:
    - **Snyk** and **Dependency-Check** perform a Software Composition Analysis to identify vulnerable dependencies.

3. **Build and Deploy**:
    - After the SCA step, a fake vulnerable application is built and deployed.

4. **DAST Tools**:
    - **OWASP ZAP** and **Dastardly** perform a Dynamic Application Security Testing (DAST) scan on the deployed application to identify runtime vulnerabilities.

### How to Set Up?

1. **Secrets Required**:
    - `SONAR_TOKEN`: Your SonarCloud token.
    - `SNYK_TOKEN`: Your Snyk token.
    - `SEMGREP_APP_TOKEN`: Your Semgrep token.

2. **SonarCloud Setup**:
    - Ensure you have the `sonar-project.properties` file in the root of your repository for the SonarCloud scan.

3. **Run**: This pipeline runs on every pull request or when manually triggered (`workflow_dispatch`).

## References:

- [SonarCloud GHA](https://github.com/marketplace/actions/sonarcloud-scan)
- [Snyk GHA](https://github.com/marketplace/actions/snyk)
- [OWASP ZAP GHA](https://github.com/marketplace/actions/owasp-zap-baseline-scan)
- [Semgrep GHA](https://github.com/marketplace/actions/semgrep)
- [Dependency-Check GHA](https://github.com/marketplace/actions/dependency-check-action)
- [Dastardly GHA](https://github.com/PortSwigger/dastardly-github-action)
