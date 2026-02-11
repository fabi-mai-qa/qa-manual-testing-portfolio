# Test Cases – TS-003: Shopping Cart Validation

These test cases validate the behavior of the Shopping Cart feature, focusing on business rules enforcement, price calculation accuracy, and data consistency during cart operations.

The objective is to ensure that the system correctly handles product addition, quantity updates, price recalculation, and cart state integrity before order creation.

At the end of this README, you will find direct links to each individual test case for easy navigation.

## Covered Test Cases
- Add products to the shopping cart
- Update product quantities and validate recalculated totals
- Remove products from the cart
- Validate cart behavior when empty
- Ensure price consistency based on registered product values
- Prevent invalid cart states (e.g. zero or invalid quantities)

## Key Quality Aspects Validated

- Business rules enforcement at cart level  
- Correct total price calculation  
- Data consistency across cart operations 

Each test case is documented individually to improve clarity, traceability, and maintainability.

## Test Cases
Click on a test case below to view its detailed specification.

- [TC-003.01 – Add a product to the shopping cart](tc-003.01.md)

- [TC-003.02 – Increase item quantity](tc-003.02.md)

- [TC-003.03 – Add other items to the shopping cart](tc-003.03.md)

- [TC-003.04 - Decrease item quantity](tc-003.04.md)

- [TC-003.05 - Remove one product from the shopping cart](tc-003.05.md)

- [TC-003.06 - Remove all items from the shopping cart](tc-003.06.md)

- [TC-003.07 - Validate warning message for zero quantity](tc-003.07.md)

- [TC-003.08 - Validate quantity field length](tc-003.08.md)

- [TC-003.09 - Validate quantity field format](tc-003.09.md)

- [TC-003.10 - Verify data consistency after page refresh](tc-003.10.md)

- [TC-003.11 - Verify data consistency after logout and login](tc-003.11.md)
