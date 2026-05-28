# Cart Test Cases

## Scope

This file covers the cart flow for the main buying path: opening a product, choosing quantity, adding it to the cart, and checking the cart review page.

Discounts, out-of-stock products, empty cart state, rental and non-rental combined discounts, and full quantity boundary testing can be covered in separate cart test cases.

## Traceability Matrix

| Requirement | Covered By | Notes |
| --- | --- | --- |
| Product Detail AC1 - Product details are shown | `CART_TC01` | Checks the main details needed before adding a product to the cart. |
| Product Detail AC3 - Quantity input and plus/minus buttons are shown | `CART_TC01` | Checks the quantity controls on the Product Detail page. |
| Product Detail AC4 - Plus button increases quantity by 1 | `CART_TC01` | Checks the quantity increase before adding the product. |
| Product Detail AC8 - "Add to Cart" adds the selected product and quantity | `CART_TC01` | Checks the success message and cart badge update. |
| Cart Review AC1 - Cart table shows item, quantity, price, total, and actions | `CART_TC02` | Checks the visible cart review table. |
| Cart Review AC5 - "Proceed" advances to the next checkout step | `CART_TC02` | Checks that checkout can continue when the cart has an item. |

## CART_TC01 - Verify that a user can review a product, set quantity, and add it to the cart

### Description

Verify that a user can open a product from the Home page, review key product details, increase the quantity, and add the product to the cart.

### Preconditions

The user is on the Home page. A product such as "Pliers" or "Combination Pliers" is visible in the product list.

### Test Steps

| Step | Action | Input Data | Expected Result |
| --- | --- | --- | --- |
| 1 | Open a product from the product list. | Product: "Pliers" or "Combination Pliers" | The Product Detail page is opened. |
| 2 | Check the product details. | N/A | The product image, name, category label, brand label, price, CO2 rating, and description are visible. |
| 3 | Check the quantity controls. | N/A | The quantity input is visible with default value `1`, and the minus and plus buttons are visible. |
| 4 | Click the plus button once. | N/A | The quantity changes from `1` to `2`. |
| 5 | Click "Add to cart". | N/A | The product is added to the cart, and the message "Product added to shopping cart" is displayed. |
| 6 | Check the cart icon in the top navigation. | N/A | The cart icon shows the updated item count. |

### Execution Summary

**Actual Result:** Passed. The product detail page showed the expected product information and quantity controls. After increasing the quantity to `2` and clicking "Add to cart", the product was added and the message "Product added to shopping cart" was displayed.

| Date | Environment | Status | Tested By | Tags |
| --- | --- | --- | --- | --- |
| 2026-05-27 | Chrome, Windows 11 | Passed | Danica Biljeljanin | Buying, Cart, Product Detail, Positive |

**Notes:** Covers the product-to-cart path with quantity increase before adding the product.

## CART_TC02 - Verify that the cart shows the correct product, quantity, price, total, and checkout action

### Description

Verify that the cart review page shows the product added to the cart, the selected quantity, the item price, the line total, and the checkout action.

### Preconditions

The cart contains one product added with quantity `2`. The user is on the Cart page.

### Test Steps

| Step | Action | Input Data | Expected Result |
| --- | --- | --- | --- |
| 1 | Check the checkout progress steps. | N/A | The steps "Cart", "Sign in", "Billing Address", and "Payment" are visible. |
| 2 | Check the cart table. | N/A | The table shows the item name, quantity input, price, line total, and remove action. |
| 3 | Check the product quantity. | Quantity: `2` | The cart shows quantity `2` for the added product. |
| 4 | Check the line total and cart total. | Example: unit price `$12.01`, quantity `2` | The line total and cart total match the selected quantity and unit price, for example `$24.02`. |
| 5 | Check the available cart actions. | N/A | "Continue Shopping" and "Proceed to checkout" are visible. |
| 6 | Click "Proceed to checkout". | N/A | The checkout flow continues to the next step. |

### Execution Summary

**Actual Result:** Passed. The cart showed the added product with quantity `2`, the item price, the calculated line total, the cart total, and the available checkout action.

| Date | Environment | Status | Tested By | Tags |
| --- | --- | --- | --- | --- |
| 2026-05-27 | Chrome, Windows 11 | Passed | Danica Biljeljanin | Buying, Cart, Checkout, Positive |

**Notes:** The total calculation uses the actual product price shown during execution. Cart item update and delete checks can be covered in separate cart test cases.
