# Payment Test Cases

## Scope

This file covers one complete payment path using "Cash on Delivery", payment method field visibility, and payment method reset behavior.

Full successful payment paths for Bank Transfer, Credit Card, Buy Now Pay Later, Gift Card, cart clearing evidence, and email confirmation can be covered in separate payment test cases.

## Traceability Matrix

| Requirement | Covered By | Notes |
| --- | --- | --- |
| Payment AC1 - Payment method dropdown shows available methods | `PAYMENT_TC01` | Checks that the dropdown is available and "Cash on Delivery" can be selected. |
| Payment AC2 - Bank Transfer shows required bank name, account name, and account number fields | `PAYMENT_TC02` | Checks the fields shown after selecting "Bank Transfer". |
| Payment AC3 - Credit Card shows card number, expiration date, CVV, and card holder name fields | `PAYMENT_TC02` | Checks the fields shown after selecting "Credit Card". |
| Payment AC4 - Past credit card expiration date shows "Expiration date must be in the future." | Not covered | Requires separate validation execution with test card data. |
| Payment AC5 - Buy Now Pay Later shows monthly installment options | `PAYMENT_TC02` | Checks that the available installment options are shown. |
| Payment AC6 - Gift Card shows gift card number and validation code fields | `PAYMENT_TC02` | Checks the fields shown after selecting "Gift Card". |
| Payment AC7 - "Cash on Delivery" requires no additional fields | `PAYMENT_TC01`, `PAYMENT_TC02` | Checks that no extra payment details are required for this method. |
| Payment AC8 - Changing payment method resets the form and shows fields for the new method | `PAYMENT_TC03` | Checks that old method fields are replaced after switching method. |
| Payment AC9 - Valid payment places the order, shows invoice confirmation, clears the cart, and sends a checkout confirmation email | `PAYMENT_TC01` | Covers order confirmation, invoice number, and visible cart indicator behavior. Email confirmation needs separate evidence. |

## PAYMENT_TC01 - Verify that the user can place an order with Cash on Delivery

### Description

Verify that the user can select "Cash on Delivery", confirm the payment, and see the final order confirmation with an invoice number.

### Preconditions

The user is already signed in. The cart contains at least one product. The user has completed the cart and billing address steps and is on the "Payment" step.

### Test Steps

| Step | Action | Input Data | Expected Result |
| --- | --- | --- | --- |
| 1 | Check the payment page. | N/A | The "Payment" heading and payment method dropdown are visible. |
| 2 | Open the payment method dropdown. | N/A | The available payment methods are shown. |
| 3 | Select "Cash on Delivery". | Payment method: "Cash on Delivery" | "Cash on Delivery" is selected. No additional payment fields are required. |
| 4 | Click "Confirm". | N/A | The payment is submitted. |
| 5 | Check the final confirmation page. | N/A | A final order confirmation is displayed with the message "Thanks for your order!" and an invoice number. |

### Execution Summary

**Actual Result:** Failed. After selecting "Cash on Delivery" and clicking "Confirm" once, the message "Payment was successful" was displayed, but the user stayed on the "Payment" step, the "Confirm" button was still visible, and the cart icon still showed the added item count. The final order confirmation with "Thanks for your order!" and an invoice number was shown only after clicking "Confirm" a second time. After the second click, the cart icon was removed from the navigation.

| Date | Environment | Status | Tested By | Tags |
| --- | --- | --- | --- | --- |
| 2026-05-27 | Chrome, Windows 11 | Failed | Danica Biljeljanin | Buying, Payment, Cash on Delivery, Positive |

**Notes:** Related bug report: `PAYMENT_BUG01`. Email confirmation needs separate email evidence.

## PAYMENT_TC02 - Verify that payment method fields are shown for each selected payment method

### Description

Verify that the payment form shows the correct fields or options after each payment method is selected.

### Preconditions

The user is already signed in. The cart contains at least one product. The user has completed the cart and billing address steps and is on the "Payment" step.

### Test Steps

| Step | Action | Input Data | Expected Result |
| --- | --- | --- | --- |
| 1 | Open the payment method dropdown. | N/A | The dropdown shows "Bank Transfer", "Cash on Delivery", "Credit Card", "Buy Now Pay Later", and "Gift Card". |
| 2 | Select "Bank Transfer". | Payment method: "Bank Transfer" | The form shows required fields for bank name, account name, and account number. |
| 3 | Select "Credit Card". | Payment method: "Credit Card" | The form shows fields for card number, expiration date, CVV, and card holder name. |
| 4 | Select "Buy Now Pay Later". | Payment method: "Buy Now Pay Later" | The form shows "Monthly installments" options: `3`, `6`, `9`, and `12`. |
| 5 | Select "Gift Card". | Payment method: "Gift Card" | The form shows fields for gift card number and validation code. |
| 6 | Select "Cash on Delivery". | Payment method: "Cash on Delivery" | "Cash on Delivery" is selected and no additional payment fields are required. |

### Execution Summary

**Actual Result:** Passed. The payment method dropdown showed the expected methods. Each selected method displayed the expected fields or options, and "Cash on Delivery" did not require additional payment fields.

| Date | Environment | Status | Tested By | Tags |
| --- | --- | --- | --- | --- |
| 2026-05-27 | Chrome, Windows 11 | Passed | Danica Biljeljanin | Buying, Payment, Field Visibility, Positive |

**Notes:** This case checks payment method field visibility only. It does not place an order for each payment method.

## PAYMENT_TC03 - Verify that changing the payment method resets the payment form

### Description

Verify that switching from one payment method to another removes the previous method's fields and shows the fields for the newly selected method.

### Preconditions

The user is already signed in. The cart contains at least one product. The user has completed the cart and billing address steps and is on the "Payment" step.

### Test Steps

| Step | Action | Input Data | Expected Result |
| --- | --- | --- | --- |
| 1 | Select "Bank Transfer". | Payment method: "Bank Transfer" | The bank transfer fields are shown. |
| 2 | Enter data in the bank transfer fields. | Bank name: `Test Bank`; Account name: `Test User`; Account number: `123456789` | The entered data is shown in the bank transfer fields. |
| 3 | Change the payment method to "Gift Card". | Payment method: "Gift Card" | The bank transfer fields are removed, and the gift card number and validation code fields are shown. |
| 4 | Change the payment method to "Cash on Delivery". | Payment method: "Cash on Delivery" | The gift card fields are removed, and no additional payment fields are required. |

### Execution Summary

**Actual Result:** Passed. After switching payment methods, the fields from the previous method were removed and the fields for the newly selected method were shown.

| Date | Environment | Status | Tested By | Tags |
| --- | --- | --- | --- | --- |
| 2026-05-27 | Chrome, Windows 11 | Passed | Danica Biljeljanin | Buying, Payment, Reset, Positive |

**Notes:** This case covers payment method reset behavior only. Final order confirmation is covered by `PAYMENT_TC01`.
