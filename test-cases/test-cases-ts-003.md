# Test Cases - TS-003: Validate Shopping Cart Total Price Calculation

### Overview
This document contains all test cases related to the validation of shopping cart total price calculation.
***

### 📍 TC-001 - Verify total price calculation when adding a product in the shopping cart

**Description:**  
Verify the total price calculation when user adds a product in the shopping cart.

**Preconditions:**  
- User account registered in the system.
- Products and their prices are registered in the system.
- User is logged into the system.

**Test Steps:**  
>**Step 1**
- **Action:** Add one item of product A to the shopping cart.
- **Expected Result:** Total price calculation matches the price of the product added.

**Test Data:**  
- User credentials.
- Products and their prices.

**Expected Result:**  
- The total price calculation of the shopping cart matches the item added.

**Status:**  
- Not Executed / Passed / Failed

**Comments:**  
- *Additional notes or observations (optional).*
***

### 📍 TC-002 - Verify total price calculation when increasing item's quantity in the shopping cart

**Description:**  
Verify the total price calculation when user increases the quantity of the product A in the shopping cart.

**Preconditions:**  
- User account registered in the system.
- Products and their prices are registered in the system.
- User is logged into the system.

**Test Steps:**  
>**Step 1**
- **Action:** Increase the quantity of the product A in the shopping cart.
- **Expected Result:** Total price calculation matches the quantity of the product A.

**Test Data:**  
- User credentials.
- Products and their prices.

**Expected Result:**  
- The total price calculation of the shopping cart matches the quantity of the product A.

**Status:**  
- Not Executed / Passed / Failed

**Comments:**  
- *Additional notes or observations (optional).*
***

### 📍 TC-003 - Verify total price calculation when adding other items in the shopping cart

**Description:**  
Verify the total price calculation when user adds other products in the shopping cart.

**Preconditions:**  
- User account registered in the system.
- Products and their prices are registered in the system.
- User is logged into the system.

**Test Steps:**  
>**Step 1**
- **Action:** Add product B in the shopping cart.
- **Expected Result:** Total price calculation matches the quantity of the product A and product B just added now.

**Test Data:**  
- User credentials.
- Products and their prices.

**Expected Result:**  
- The total price calculation of the shopping cart matches the quantity of the product A and product B.

**Status:**  
- Not Executed / Passed / Failed

**Comments:**  
- *Additional notes or observations (optional).*
***

### 📍 TC-004 - Verify total price calculation when decreasing item's quantity in the shopping cart

**Description:**  
Verify the total price calculation when user decreases the quantity of the product A in the shopping cart.

**Preconditions:**  
- User account registered in the system.
- Products and their prices are registered in the system.
- User is logged into the system.

**Test Steps:**  
>**Step 1**
- **Action:** Decrease the quantity of the product A in the shopping cart.
- **Expected Result:** Total price calculation matches the updated quantity of the product A and product B.

**Test Data:**  
- User credentials.
- Products and their prices.

**Expected Result:**  
- The total price calculation of the shopping cart matches the updated quantity of the product A and product B.

**Status:**  
- Not Executed / Passed / Failed

**Comments:**  
- *Additional notes or observations (optional).*
***


### 📍 TC-005 - Verify total price calculation when removing a product from the shopping cart

**Description:**  
Verify the total price calculation when user removes product A from the shopping cart.

**Preconditions:**  
- User account registered in the system.
- Products and their prices are registered in the system.
- User is logged into the system.

**Test Steps:**  
>**Step 1**
- **Action:** Remove product A from the shopping cart.
- **Expected Result:** Total price calculation matches the price of the product B only.

**Test Data:**  
- User credentials.
- Products and their prices.

**Expected Result:**  
- The total price calculation of the shopping cart matches the product B only.

**Status:**  
- Not Executed / Passed / Failed

**Comments:**  
- *Additional notes or observations (optional).*
***

### 📍 TC-006 - Verify total price calculation when removing all items from the shopping cart

**Description:**  
Verify the total price calculation when user removes all products from the shopping cart.

**Preconditions:**  
- User account registered in the system.
- Products and their prices are registered in the system.
- User is logged into the system.

**Test Steps:**  
>**Step 1**
- **Action:** Remove all products from the shopping cart.
- **Expected Result:** Total price calculation matches the empty shopping cart.

**Test Data:**  
- User credentials.
- Products and their prices.

**Expected Result:**  
- The total price calculation matches the empty shopping cart.

**Status:**  
- Not Executed / Passed / Failed

**Comments:**  
- *Additional notes or observations (optional).*
***

### 📍 TC-007 - Validate warning message when enter zero as quantity

**Description:**  
Validate the warning message displayed when the user types zero in the quantity field referred to the product in the shopping cart.

**Preconditions:**  
- User account registered in the system.
- Products and their prices are registered in the system.
- User is logged into the system.

**Test Steps:**  
>**Step 1**
- **Action:** Add a product to the shopping cart.
- **Expected Result:** Total price calculation matches the price of the product added.

>**Step 2**
- **Action:** Type the number 0 (zero) in the quantity field of the product in the shopping cart.
- **Expected Result:** A warning message is displayed informing the user that quantity value is invalid.

**Test Data:**  
- User credentials.
- Products and their prices.

**Expected Result:**  
- The warning message is displayed on the screen informing the user the quantity value is invalid.

**Status:**  
- Not Executed / Passed / Failed

**Comments:**  
- *Additional notes or observations (optional).*
***

### 📍 TC-008 - Validate length of the quantity field in the shopping cart page

**Description:**  
Validate the length of the quantity field in the shopping cart page.

**Preconditions:**  
- User account registered in the system.
- Products and their prices are registered in the system.
- User is logged into the system.

**Test Steps:**  
>**Step 1**
- **Action:** Add a product to the shopping cart.
- **Expected Result:** Total price calculation matches the price of the product added.

>**Step 2**
- **Action:** Type a huge number in the quantity field of the product in the shopping cart.
- **Expected Result:** Only the number of digits allowed will be accepted in the quantity field and a warning message pops up in the screen informing the user about the field's length.

**Test Data:**  
- User credentials.
- Products and their prices.

**Expected Result:**  
- Only the allowed length will be accepted in the quantity field and a warning message pops up informing the user about the maximum length of this field.

**Status:**  
- Not Executed / Passed / Failed

**Comments:**  
- How many digits the quantity field in the shopping cart page should accept?
***

### 📍 TC-009 - Validate format of the quantity field in the shopping cart page

**Description:**  
Validate whether the quantity field in the shopping cart page accepts non-numeric characters.

**Preconditions:**  
- User account registered in the system.
- Products and their prices are registered in the system.
- User is logged into the system.

**Test Steps:**  
>**Step 1**
- **Action:** Add a product to the shopping cart.
- **Expected Result:** Total price calculation matches the price of the product added.

>**Step 2**
- **Action:** Type a letter (e.g., 'a') in the quantity field of the product in the shopping cart.
- **Expected Result:** A warning message is displayed informing the user that quantity field accepts only numeric characters.

**Test Data:**  
- User credentials.
- Products and their prices.

**Expected Result:**  
- The warning message is displayed on the screen informing the user the quantity field accepts only numeric characters.

**Status:**  
- Not Executed / Passed / Failed

**Comments:**  
- *Additional notes or observations (optional).*
***

### 📍 TC-010 - Verify total price calculation in the shopping cart when refreshing the page

**Description:**  
Verify data and total price calculation in the shopping cart whenever user refreshes the page.

**Preconditions:**  
- User account registered in the system.
- Products and their prices are registered in the system.
- User is logged into the system.

**Test Steps:**  
>**Step 1**
- **Action:** Add some products to the shopping cart.
- **Expected Result:** Total price calculation matches the price of the products added.

>**Step 2**
- **Action:** Refresh the shopping cart page.
- **Expected Result:** All products data remain correctly as well as the total price calculation of the shopping cart.

**Test Data:**  
- User credentials.
- Products and their prices.

**Expected Result:**  
- The products data previously added to the cart and the total price calculation are shown accordingly after refreshing the shopping cart page.

**Status:**  
- Not Executed / Passed / Failed

**Comments:**  
- *Additional notes or observations (optional).*
***

### 📍 TC-011 - Verify total price calculation in the shopping cart when logout and login back to the system

**Description:**  
Verify data and total price calculation in the shopping cart whenever user logs out and logs back into the system.

**Preconditions:**  
- User account registered in the system.
- Products and their prices are registered in the system.
- User is logged into the system.

**Test Steps:**  
>**Step 1**
- **Action:** Add some products to the shopping cart.
- **Expected Result:** Total price calculation matches the price of the products added.

>**Step 2**
- **Action:** Log out from the system.
- **Expected Result:** User is successfully logged out.

>**Step 3**
- **Action:** Log in again using the same user credentials.
- **Expected Result:** User is successfully logged in.

>**Step 4**
- **Action:** Access the shopping cart page.
- **Expected Result:** All products data remain correctly as well as the total price calculation of the shopping cart.

**Test Data:**  
- User credentials.
- Products and their prices.

**Expected Result:**  
- The products data previously added to the cart and the total price calculation are shown accordingly in the shopping cart page after user log out and log in back to the system.

**Status:**  
- Not Executed / Passed / Failed

**Comments:**  
- *Additional notes or observations (optional).*
