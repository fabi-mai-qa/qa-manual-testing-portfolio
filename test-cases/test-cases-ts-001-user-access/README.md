# Test Cases – TS-001: User Access to the System

This test suite validates the authentication flow, ensuring that access to the system is granted only when valid credentials are provided and correctly denied otherwise.
The focus is on credential validation, access control enforcement, authentication behavior, and proper error handling when login data is invalid or missing.

At the end of this README, you will find direct links to each individual test case for easy navigation.

## Covered Test Cases
- Successful login with valid credentials
- Access denial for invalid credentials
- Proper error messages for failed login attempts
- Authentication restricted to registered users

These test cases ensure that the authentication mechanism is reliable, secure, and aligned with expected system behavior.

## Test Cases
Click on a test case below to view its detailed specification.

- [TC-001.01 – Access the system using valid credentials](tc-001.01.md)

- [TC-001.02 – Access the system using invalid password](tc-001.02.md)

- [TC-001.03 – Validate whether username field is case-sensitive](tc-001.03.md)

- [TC-001.04 – Access the system using non-registered credentials](tc-001.04.md)
