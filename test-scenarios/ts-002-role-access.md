## Test Scenario 002 - Verify User Access Based on User Roles

### ID: TS-002

**Description:**  
Validate that role-based authorization is correctly enforced, ensuring users can access only the system features allowed for their assigned role and are prevented from accessing restricted areas and resources.

**Preconditions:**  
- Application is available in the test environment.
- Admin user account exists in the system.
- Non-admin user account exists in the system.

**Scenario Flow:**  
- User opens the application.
- User logs in using admin credentials and verifies accessible system areas and actions.
- User logs out.
- User logs in using non-admin credentials and verifies restricted access behavior.

**Expected Result:**  
- Admin users can access all system areas and perform privileged actions.
- Non-admin users can access only allowed features and are prevented from viewing or interacting with system restricted areas.
- Unauthorized access attempts are blocked by the system.

**Business Rules:**
- Role-based authorization must be enforced for all protected system resources.
- Admin users must have access to all system screens and functionalities.
- Non-admin users must be restricted to explicitly permitted features.
- The system must prevent unauthorized access to restricted screens and actions.
