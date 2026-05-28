# Checkout Bug Reports

## CHECKOUT_BUG01 - House number is not pre-filled on the billing address step [Open]

| Severity | Priority | Related Test Case |
| --- | --- | --- |
| Medium | Medium | `CHECKOUT_TC01` - Verify that an already signed-in user can continue from cart through billing address to payment. |

### Description

The "House number" value entered during registration is not pre-filled on the checkout "Billing Address" step.

The same value is also not visible on the "Profile" page, although it was entered during registration.

### Steps to Reproduce

| Step | Action | Test Data |
| --- | --- | --- |
| 1 | Register a new user account and fill in the address details. | Include a value in "House number". |
| 2 | Log in with the registered account. | N/A |
| 3 | Open the "Profile" page. | N/A |
| 4 | Check the saved address details. | N/A |
| 5 | Add a product to the cart and proceed to checkout. | N/A |
| 6 | Continue to the "Billing Address" step. | N/A |
| 7 | Check the "House number" field. | N/A |

### Expected Result

The saved "House number" value is shown in the account address details and is pre-filled on the checkout "Billing Address" step.

### Actual Result

The "House number" value is not shown on the "Profile" page. On the checkout "Billing Address" step, the "House number" field is empty and must be entered manually.

### Test Environment

| Date | OS | Browser | Device | App Version | Tested By |
| --- | --- | --- | --- | --- | --- |
| 2026-05-27 | Windows 11 | Chrome | Desktop | N/A | Danica Biljeljanin |

### Attachments

To be added: screenshot or short video showing the missing "House number" value on the "Profile" page and the empty "House number" field on the checkout "Billing Address" step.

## CHECKOUT_BUG02 - Checkout can continue to payment when a required billing address field is empty [Open]

| Severity | Priority | Related Test Case |
| --- | --- | --- |
| Medium | Medium | `CHECKOUT_TC02` - Verify that the user cannot proceed when required billing address fields are empty. |

### Description

The checkout "Billing Address" step does not fully validate empty required billing address fields.

When a required field is empty, the "Proceed to checkout" button becomes disabled, but the empty field is not highlighted as invalid. During testing, removing the `disabled` attribute from the button in the browser HTML allowed the user to click it and continue to the "Payment" step with the required field still empty.

### Steps to Reproduce

| Step | Action | Test Data |
| --- | --- | --- |
| 1 | Log in and add a product to the cart. | N/A |
| 2 | Proceed through checkout until the "Billing Address" step. | N/A |
| 3 | Clear one required billing address field. | Example: clear "Postal code" |
| 4 | Check the empty field and the "Proceed to checkout" button. | N/A |
| 5 | Remove the `disabled` attribute from the "Proceed to checkout" button in the browser HTML. | N/A |
| 6 | Click "Proceed to checkout". | N/A |
| 7 | Check the checkout step. | N/A |

### Expected Result

The empty required field is highlighted as invalid, and checkout cannot continue to the "Payment" step while required billing address data is missing.

### Actual Result

The empty required field is not highlighted as invalid. The button is disabled in the UI, but after the `disabled` attribute is removed from the browser HTML, the user can click "Proceed to checkout" and continue to the "Payment" step with the required field still empty.

### Test Environment

| Date | OS | Browser | Device | App Version | Tested By |
| --- | --- | --- | --- | --- | --- |
| 2026-05-27 | Windows 11 | Chrome | Desktop | N/A | Danica Biljeljanin |

### Attachments

To be added: screenshot or short video showing the empty required field, the disabled button, and the user reaching the "Payment" step after the `disabled` attribute is removed.
