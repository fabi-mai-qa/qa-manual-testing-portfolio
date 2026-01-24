# Test Scenario 003 – Validate Shopping Cart Total Price Calculation

## ID: TS-003

**Description:**  
Validate that the system correctly calculates the shopping cart total price based on the quantity of selected products.

**Preconditions:**  
- Application is available in the test environment.
- User account is registered in the system.
- Products and their prices are registered in the system.

**Scenario Flow:**  
- User accesses the application.
- User selects one or more products and adds them to the shopping cart.
- User updates the quantity of products in the cart.
- User removes one of the products from the cart.
- User empties the shopping cart.
- User adds one product again to the shopping cart.
- User refreshes the page.
- User logs out and logs back into the system.
- User accesses the shopping cart page again.
- System maintains data and recalculates the total price accordingly.

**Expected Result:**  
- The shopping cart total price is updated correctly when products are added, removed, or when quantities are changed.

**Business Rules:**
- Each product included in the order must have a registered price.
- The system must correctly calculate the total price when products are added, removed, or when quantities are updated.
- The system must persist cart data when the user refreshes the page, logs out, and logs back into the system. 
