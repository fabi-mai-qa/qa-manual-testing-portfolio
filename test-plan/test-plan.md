# Test Plan 

## Introduction
This Test Plan describes the testing activities for the software product.
It defines the scope, approach, resources and schedule for manual functional and API testing to ensure the system meets the acceptance criteria and business requirements.

## Test Objectives
- Validate functional requirements.
- Ensure the final product meets customer expectations and defined acceptance criteria.
- Identify defects before production.
- Support release decision-making.

## Scope of Testing

### In Scope:
- Manual functional testing for the desktop application.
- API testing (REST and SOAP).
- Database validation using SQL.
- Smoke and exploratory testing.
- Validation against acceptance criteria.

### Out of Scope:
- Automated testing.
- Performance and load testing.
- Security testing.
- Infrastructure testing.
- Third-party systems not controlled by the team.

## Test Approach:
- Tests are designed and planned based on a balance between the acceptance criteria and the business requirements.
- Black box testing is applied for functional validation.
- Gray box testing is applied when technical knowledge is required to support functional validation.
- Risk-based testing is used to prioritize critical scenarios, especially when time is limited.
- Exploratory testing is performed to identify unexpected issues and potential risks.

## Test Environment

### Environments:
- Dedicated QA/Test environment for the desktop application.
- APIs available for testing in the QA environment.
- Dedicated test databases.

### Test Data:
- Existing test data available in test databases.
- Test data created manually by QA team when required.

## Test Schedule
- Test activities start after the build is available for the test environment.
- Smoke testing is performed to validate build stability.
- Database scripts and data setup are applied when required.
- Functional and API tests are executed after the necessary documentation is provided.
- Defect fixes are re-tested as new builds are delivered.
- A final test summary report is prepared at the end of the testing cycle.

## Entry and Exit Criteria

### Entry Criteria:
- Build deployed to the test environment.
- Stable test environment.
- Defined and clear acceptance criteria for the functionalities to be tested.
- Access to APIs and test databases.

### Exit Criteria:
- Planned test cases and test scenarios are executed.
- Critical defects are fixed.
- All test results are documented.
- Release decision is supported by the QA team.

## Roles and Responsibilities

### QA Analyst:
- Execute manual functional, exploratory, smoke, and API tests according to this Test Plan.
- Validate acceptance criteria during the test execution.
- Identify, document, and track defects during the test cycle.
- Perform database validation using SQL when required.
- Re-test fixes delivered by the development team.
- Support the release decision with test results and reports.

### Developers:
- Fix defects reported during test execution.
- Support defect investigation and root cause analysis.
- Provide new builds for re-testing when needed.

### Product Owner / Business:
- Clarify the acceptance criteria during the test cycle.
- Support validation of delivered functionality.
- Participate in release decision when required.

## Defect Reporting and Tracking
- Defects identified during test execution are logged in the defect tracking tool.
- Each defect includes clear reproduction steps, expected and actual results, and supporting evidence.
- Defects are followed up until resolution.
- Fixes are re-tested and validated by the QA team.

## Test Deliverables and Reporting

### Test Deliverables:
- Test cases and/or test scenarios.
- Defect reports.
- Test summary reports.
- Test execution evidence.

### Test Reporting:
- Test results are reported through test summary reports and test execution documentation, in a way that both technical and non-technical stakeholders can understand.
- Defects are communicated through defect reports.
- The test summary report is shared as part of the test documentation.

## Risks, Assumptions and Constraints

### Risks:
- Build delays during the test cycle.
- Test environment instability during execution.
- Acceptance criteria incomplete or not clear.

### Assumptions:
- Build will be available on time.
- Test environment will be ready for testing.

### Constraints:
- Limited testing time.
- Limited resources.
