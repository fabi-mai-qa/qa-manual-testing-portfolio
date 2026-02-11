# Test Cases – TS-002: User Roles Access

This test suite validates access control and information disclosure based on user roles (admin and non-admin), ensuring that restricted features and data are exposed only to authorized users.

At the end of this README, you will find direct links to each individual test case for easy navigation.

## Covered Test Cases
- Visibility of restricted areas for admin users
- Restricted areas not visible for non-admin users
- System behavior when a non-admin user attempts to access restricted pages directly via URL
- Prevention of sensitive information disclosure to non-admin users

These test cases are designed to validate correct access enforcement and secure information exposure according to user role credentials.

## Test Cases
Click on a test case below to view its detailed specification.

- [TC-002.01 – Restricted areas are accessible to admin user](tc-002.01.md)

- [TC-002.02 – Restricted areas are not visible to non-admin user](tc-002.02.md)

- [TC-002.03 – Direct URL access attempt to restricted areas by non-admin users](tc-002.03.md)
