# Test Cases - TS-002: Verify User Access Based on User Roles

### Overview
This document contains all test cases related to validating user accesses based on user roles.
***
### 📍 TC-001 - Access restricted pages and functionalities using admin credentials

**Description:**  
Validate that admin users have full access to the system and its functionalities.

**Preconditions:**  
- Admin user account registered in the system.
- Application is accessible and loads the home screen successfully.

**Test Steps:**  
  - **Step 1**
    - **Action:** Fill in the username and password fields with admin user credentials.
    - **Expected Result:** Admin user is successfully logged in.

  - **Step 2**
    - **Action:** Access all restricted pages and verify their functionalities using admin credentials.
    - **Expected Result:** All restricted pages and their functionalities are available for admin users.

**Test Data:**  
- Admin username.
- Admin user password.

**Expected Result:**  
- All restricted pages and functionalities are available for admin users.

**Status:**  
- Not Executed / Passed / Failed

**Comments:**  
- *Additional notes or observations (optional).*
***

### 📍 TC-002 - Validate restricted pages are not visible using non-admin user credentials

**Description:**  
Validate that restricted pages and functionalities are not visible to non-admin users.

**Preconditions:**  
- Non-admin user account registered in the system.
- Application is accessible and loads the home screen successfully.

**Test Steps:**  
  - **Step 1**
    - **Action:** Fill in the username and password fields with non-admin user credentials.
    - **Expected Result:** Non-admin user is successfully logged in.

  - **Step 2**
    - **Action:** Verify that restricted pages and functionalities are not available for non-admin users.
    - **Expected Result:** Restricted pages and functionalities are not available for non-admin users.

**Test Data:**  
- Non-admin username.
- Non-admin user password.

**Expected Result:**  
- All restricted pages and functionalities are not available for non-admin user.

**Status:**  
- Not Executed / Passed / Failed

**Comments:**  
- *Additional notes or observations (optional).*
***

### 📍 TC-003 - Validate warning message when accessing restricted pages via URL using non-admin user credentials

**Description:**  
Validate that a warning message is returned to the user when attempting to access restricted pages directly via URL using non-admin user credentials.

**Preconditions:**  
- Non-admin user account registered in the system.
- Application is accessible and loads the home screen successfully.

**Test Steps:**  
  - **Step 1**
    - **Action:** Fill in the username and password fields with non-admin user credentials.
    - **Expected Result:** Non-admin user is successfully logged in.

  - **Step 2**
    - **Action:** Manually enter the URL of a restricted page in the browser address bar.
    - **Expected Result:** A warning message is displayed to the user indicating that access is restricted due to insufficient permissions.

**Test Data:**  
- Non-admin username.
- Non-admin user password.

**Expected Result:**  
- Access directly via URL is not available and a warning message is displayed informing it is a restricted area and the user role is non-admin.

**Status:**  
- Not Executed / Passed / Failed

**Comments:**  
- *Additional notes or observations (optional).*
