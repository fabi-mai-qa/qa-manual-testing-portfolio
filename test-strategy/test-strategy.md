# Test Strategy 

## Introduction
This document defines the overall test strategy to ensure the quality of a software product.

It outlines the general testing approach and quality assurance principles that guide the testing process.

The strategy focuses on functional testing and API validation, with quality activities aligned with business requirements and prioritized through a risk-based approach.

## Purpose
The purpose of this test strategy is to establish consistent testing practices and techniques to ensure that the software product meets its quality goals and business expectations throughout the development process.

## Objectives
- Support the test planning and execution process through a structured testing approach.
- Ensure that the final product meets customer and business requirements.
- Identify defects early to reduce risks before the product reaches end users.
- Increase customer confidence in the quality and reliability of the software product.

## Scope of Testing

### In Scope:
- Desktop functional testing.
- API testing (REST and SOAP).
- Manual test execution.
- Database validation using SQL.
- Smoke and exploratory testing (manual).
- Validation against defined acceptance criteria.

### Out of Scope:
- Automated testing.
- Performance and load testing.
- Security penetration testing.
- Infrastructure testing.
- Third-party systems not controlled by the team.

## Test Types, Levels and Approach

### Test Types:
- Functional testing.
- Exploratory testing.
- Smoke testing.
- API testing.

### Test Levels:
- System testing.
- Integration testing.

### Test Approach:
- Black box testing.
- Gray box testing.
- Prioritize risk scenarios when planning test cases, especially when time is limited.

## Test Environment

### Environments:
- Dedicated QA/Test environment for desktop application and APIs.

### Test Data:
- Dedicated test databases.
- Manually created test data.

## Entry and Exit Criteria

### Entry Criteria:
- Available test environment.
- Executable build available for testing.
- Defined and clear acceptance criteria.
- Access to QA/Test databases and APIs.

### Exit Criteria:
- Test cases executed according to the defined test scope.
- Critical defects fixed.
- Acceptance criteria validated through test results.
- Release decision supported by the QA team.

## Roles and Responsibilities

### QA Analyst:
- Define and maintain the test strategy, test plans, and test cases.
- Execute manual functional, exploratory, smoke, and API tests.
- Validate acceptance criteria and business requirements.
- Identify, document, and track defects.
- Support root cause analysis in collaboration with developers.
- Validate fixes and support release decisions.
- Perform database validation using SQL.
- Collect and validate data to support API testing when required.

### Developers:
- Develop features according to defined requirements and acceptance criteria.
- Perform unit testing and support integration testing.
- Fix reported defects and support defect analysis.
- Collaborate with QA during issue investigation and resolution.

### Product Owner / Business:
- Define and clarify business requirements and acceptance criteria.
- Prioritize features and defect fixes.
- Support validation of delivered functionality.


## Defect Management and Reporting

- Defects are identified during test execution and documented with clear and detailed information.
- Each defect includes steps to reproduce, expected and actual results, screenshots, videos and/or logs when applicable, and environment details.
- Defects are classified by severity and priority to support decision-making.
- Reported defects are tracked until resolution and verified after fixes are applied.
- QA collaborates with developers to support defect investigation and root cause analysis.


## Test Deliverables and Metrics

### Test Deliverables:
- Test planning documentation.
- Test scenarios and test cases.
- Test summary report.
- Bug reports.

### Metrics:
- Passed test cases.
- Failed test cases.
- Number of reported defects.

## Risks, Assumptions and Constraints

### Risks:
- Limited time for test execution.
- Test environment instability.
- Acceptance criteria not clear or well defined.

### Assumptions:
- Build executable available in time for testing.
- The test environment will be available for test execution.

### Constraints:
- Limited resources.


## Test Tools

### Test Management & Documentation:
- Jira
- Notion
- Microsoft Excel
- Microsoft Word

### API Testing:
- Postman

### Database Validation:
- SQL Server Management Studio
- Oracle SQL Developer
