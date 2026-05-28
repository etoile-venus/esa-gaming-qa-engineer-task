# Checkout Test Cases

## Scope

This file covers checkout for an already signed-in user: moving from cart review to sign-in confirmation, billing address, billing address validation, and the payment step.

Guest checkout login, full login validation, and TOTP checkout login can be covered in separate checkout test cases.

## Traceability Matrix

| Requirement                                                                      | Covered By      | Notes                                                                |
| -------------------------------------------------------------------------------- | --------------- | -------------------------------------------------------------------- |
| Sign In AC5 - Already logged-in users can proceed to billing address             | `CHECKOUT_TC01` | Checks the signed-in confirmation message and checkout continuation. |
| Billing Address AC1 - Required address fields are shown                          | `CHECKOUT_TC01` | Checks the visible billing address fields.                           |
| Billing Address AC2 - Empty required fields are highlighted as invalid and "Proceed" is disabled | `CHECKOUT_TC02` | Checks that checkout cannot continue when required billing address fields are empty. |
| Billing Address AC3 - Filled address fields allow the user to advance to payment | `CHECKOUT_TC01` | Checks that checkout can continue when the address is filled.        |
| Billing Address AC4 - Logged-in users see pre-filled address details             | `CHECKOUT_TC01` | Checks the saved account address values.                             |

## CHECKOUT_TC01 - Verify that an already signed-in user can continue from cart through billing address to payment

### Description

Verify that an already signed-in user can continue checkout from the cart, review the signed-in message, confirm the billing address, and reach the payment step.

### Preconditions

The user is already signed in. The cart contains at least one product. The user account has billing address details saved.

### Test Steps

| Step | Action                           | Input Data | Expected Result                                                                                 |
| ---- | -------------------------------- | ---------- | ----------------------------------------------------------------------------------------------- |
| 1    | Open the Cart page.              | N/A        | The cart contains at least one item and the checkout progress steps are visible.                |
| 2    | Click "Proceed to checkout".     | N/A        | The "Sign in" step is opened.                                                                   |
| 3    | Check the "Sign in" step.        | N/A        | A message is shown that the user is already logged in and can proceed to checkout.              |
| 4    | Click "Proceed to checkout".     | N/A        | The "Billing Address" step is opened.                                                           |
| 5    | Check the billing address form.  | N/A        | The "Country", "Postal code", "House number", "Street", "City", and "State" fields are visible. |
| 6    | Check the saved address details. | N/A        | The billing address fields are filled with the user's saved address values.                     |
| 7    | Click "Proceed to checkout".     | N/A        | The checkout flow continues to the "Payment" step.                                              |

### Execution Summary

**Actual Result:** Failed. The user could continue from the signed-in step to "Billing Address", and most saved address fields were shown. However, the "House number" field was empty and had to be entered manually, even though the value was provided during registration. The "Profile" page also did not show the saved house number.

| Date | Environment        | Status  | Tested By          | Tags                                        |
| ---- | ------------------ | ------- | ------------------ | ------------------------------------------- |
| 2026-05-27 | Chrome, Windows 11 | Failed | Danica Biljeljanin | Buying, Checkout, Billing Address, Positive |

**Notes:** Related bug report: `CHECKOUT_BUG01`. Login validation is covered in the Auth test cases, so this case focuses on checkout continuity for a signed-in user.

## CHECKOUT_TC02 - Verify that the user cannot proceed when required billing address fields are empty

### Description

Verify that the checkout flow blocks progress from the "Billing Address" step when required address fields are empty.

### Preconditions

The user is already signed in. The cart contains at least one product. The user has reached the "Billing Address" step during checkout.

### Test Steps

| Step | Action | Input Data | Expected Result |
| --- | --- | --- | --- |
| 1 | Check the billing address form. | N/A | The "Country", "Postal code", "Street", "City", and "State" fields are visible. |
| 2 | Clear one required billing address field. | Example: clear "Postal code" | The field is empty and is highlighted as invalid. |
| 3 | Check the checkout action. | N/A | The "Proceed to checkout" button is disabled. |
| 4 | Check the checkout progress step. | N/A | The user remains on the "Billing Address" step and cannot continue to the "Payment" step. |

### Execution Summary

**Actual Result:** Failed. When one required billing address field was empty, the "Proceed to checkout" button was disabled and the user could not continue to the "Payment" step. However, the empty required field was not highlighted as invalid.

| Date | Environment | Status | Tested By | Tags |
| --- | --- | --- | --- | --- |
| 2026-05-27 | Chrome, Windows 11 | Failed | Danica Biljeljanin | Buying, Checkout, Billing Address, Negative |

**Notes:** Related bug report: `CHECKOUT_BUG02`. The empty required field was not highlighted as invalid. The "Proceed to checkout" button was disabled in the UI, but after the `disabled` attribute was removed from the browser HTML, checkout could continue to the "Payment" step. "House number" is visible in the UI, but the acceptance criteria list "Street", "City", "State", "Country", and "Postal code" as required address fields.
