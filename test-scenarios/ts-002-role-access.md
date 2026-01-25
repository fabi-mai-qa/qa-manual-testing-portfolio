# Test Scenario 002 – Verify User Access Based on User Roles

## ID: TS-002

**Description:**  
Validate that users have access to system functionalities according to their assigned roles (admin and non-admin).

**Preconditions:**  
- Application is available in the test environment.
- Admin user account exists in the system.
- Non-admin user account exists in the system.

**Scenario Flow:**  
- User opens the application.
- User logs in using admin credentials.
- User logs out.
- User logs in using non-admin credentials.

**Expected Result:**  
- Admin users have full access to all system screens and functionalities.
- Non-admin users have restricted access and cannot view or access unauthorized system areas.

**Business Rules:**
- Users with admin roles must have full access to all system screens and functionalities.
- Users with non-admin roles must have access only to features explicitly allowed for their role.
