# code_action
The AppSec CodeQL GitHub Action is tailored for performing CodeQL scans on repositories with the capability of using custom rule sets and configurations. It supports flexible configurations for different repositories, stored in the repo-configs directory, and utilizes custom CodeQL query suites from the query-suites directory.

Inputs
repo: (Required) The full name of the repository to be scanned.
paths_ignored: Comma delimited paths to be ignored by the scan.
rules_excluded: Comma delimited CodeQl rule ids to be excluded.
Usage
To integrate this action into your workflow, create a .yml file in the .github/workflows directory of your repository and follow the steps below:

Workflow Setup: Add the following content to your workflow file:

name: CodeQL Analysis

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  codeql-analysis:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout Code
      uses: actions/checkout@v4
      with:
        repository: ${{ github.repository }}

    - name: Run AppSec CodeQL Analysis
      uses: <username>/codeql-action@v1.0.0
      with:
        repo: ${{ github.repository }}
        paths_ignored: |
         test/
         data/
        rules_excluded: |
         js/foo
         js/bar
Configurations: Place your custom configurations for repositories in the repo-configs directory and your CodeQL query suites in the query-suites directory. These will be utilized by the action to tailor the scan according to your specific requirements.

Features
Customized CodeQL Scans: Ability to run scans with custom configurations and query suites.
Flexible Setup: Supports multiple repositories with different configurations.
SARIF File Upload: Automated process for uploading SARIF files for analysis reporting.
