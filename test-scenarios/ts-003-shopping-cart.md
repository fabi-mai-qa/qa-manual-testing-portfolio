## Test Scenario 003 - Validate Shopping Cart Total Price Calculation

### ID: TS-003

**Description:**  
Validate that the system correctly calculates the shopping cart total price and maintains cart data consistency across user sessions and navigation events such as refresh, logout/login, and page transitions.

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

**Expected Result:**  
- The shopping cart total price is correctly updated whenever products are added, removed, or quantities are changed.
- Cart data is preserved after page refresh, navigation, and user session restart.
- The recalculated total price remains consistent with the cart contents after each action.

**Business Rules:**
- Each product included in the cart must have a registered price.
- The system must correctly calculate the total price when products are added, removed, or when quantities are updated.
- The system must persist cart data across page refresh, navigation, and user session restart.
