# Test Scenarios 

## Introduction
This document describes the high-level test scenarios based on business requirements and acceptance criteria.
Test scenarios represent end-to-end flows and critical functionalities to be validated during the testing cycle.
***
### 📍TS-001 – Validate User Access to the System

**Description:**  
Validate that the user can access the system using valid credentials and that access is denied when invalid credentials are provided.

**Preconditions:**  
- Application is available in the test environment.
- User account is registered in the system.  

**Scenario Flow:**  
- User opens the application.
- User enters login credentials.
- System validates the provided credentials.
- System allows or denies access based on validation.  

**Expected Result:**  
- User gains access to the system when valid credentials are used.
- An appropriate error message is displayed when invalid credentials are used.  
***

### 📍TS-002 – Verify User Access Based on User Roles

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
***

### 📍TS-003 – Validate Shopping Cart Total Price Calculation

**Description:**  
Validate that the system correctly calculates the shopping cart total price based on the quantity of selected products.

**Preconditions:**  
- Application is available in the test environment.
- User account is registered in the system.
- Products and their prices are registered in the system.

**Scenario Flow:**  
- User accesses the application.
- User selects one or more products to add them to the shopping cart.
- User updates the quantity of products in the cart.
- System recalculates the total price accordingly.

**Expected Result:**  
- The shopping cart total price is updated correctly when products are added, removed, or when quantities are changed.
