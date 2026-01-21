# Test Cases - TS-001: Validate User Access to the System 

### Overview
This document contains all test cases related to the validation of the user access to the system.
***

### 📍 TC-001 - Access the system using valid user credentials

**Description:**  
Validate access to the system using a previously registered user.

**Preconditions:**  
- User account registered in the system.

**Test Steps:**  
>**Step 1**
- **Action:** Open the application.
- **Expected Result:** Application home screen is displayed.

>**Step 2**
- **Action:** Fill in the username and password fields with valid user credentials.
- **Expected Result:** User is successfully logged in.

**Test Data:**  
- Valid username.
- Valid password.

**Expected Result:**  
- Existing user successfully logged in.

**Status:**  
- Not Executed / Passed / Failed

**Comments:**  
- *Additional notes or observations (optional).*
***

### 📍 TC-002 - Access the system using an invalid password

**Description:**  
Validate the warning message returned to the user.

**Preconditions:**  
- User account registered in the system.

**Test Steps:**  
>**Step 1**
- **Action:** Open the application.
- **Expected Result:** Application home screen is displayed.

>**Step 2**
- **Action:** Fill in the username with valid user credentials and then an invalid password.
- **Expected Result:** User is not logged in and a warning message is displayed indicating that the password is incorrect.

**Test Data:**  
- Valid username.
- Invalid password.

**Expected Result:**  
- A warning message is returned to the user to inform the password is wrong and the existing user is not logged in.

**Status:**  
- Not Executed / Passed / Failed

**Comments:**  
- *Additional notes or observations (optional).*
***

### 📍 TC-003 - Verify whether the username field is case-sensitive

**Description:**  
Validate whether the username field  is case-sensitive by using uppercase and lowercase characters.

**Preconditions:**  
- User account registered in the system.

**Test Steps:**  
>**Step 1**
- **Action:** Open the application.
- **Expected Result:** Application home screen is displayed.

>**Step 2**
- **Action:** Fill in the username with the correct user credentials but typing uppercase and lowercase characters and then the correct password.
- **Expected Result:** System behavior complies with the defined business rule for username case sensitivity.

**Test Data:**  
- Username of the existing user alternating between uppercase and lowercase caracteres.
- Password of the existing user.

**Expected Result:**  
- The system enforces or ignores username case sensitivity according to the defined requirements.

**Status:**  
- Not Executed / Passed / Failed

**Comments:**  
- Is it supposed to be or not to be a case-sensitive field?.
***

### 📍 TC-004 - Access the system using non-registered user credentials

**Description:**  
Validate the warning message returned to the user.

**Preconditions:**  
- No active user account exists with the provided credentials.

**Test Steps:**  
>**Step 1**
- **Action:** Open the application.
- **Expected Result:** Application home screen is displayed.

>**Step 2**
- **Action:** Fill in the username and password fields with non-registered user credentials.
- **Expected Result:** User is not logged in and a warning message is displayed indicating that the user does not exist.

**Test Data:**  
- Username of a non registered user.
- Password of a non registered user.

**Expected Result:**  
- A warning message is returned to the user informing this user is not registered in the system and not logged in.

**Status:**  
- Not Executed / Passed / Failed

**Comments:**  
- *Additional notes or observations (optional).*
