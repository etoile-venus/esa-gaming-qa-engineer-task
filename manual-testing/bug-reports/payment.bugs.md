# Payment Bug Reports

## PAYMENT_BUG01 - Cash on Delivery order confirmation requires clicking Confirm twice [Open]

| Severity | Priority | Related Test Case |
| --- | --- | --- |
| Medium | Medium | `PAYMENT_TC01` - Verify that the user can place an order with Cash on Delivery. |

### Description

When "Cash on Delivery" is selected, the first click on "Confirm" shows the message "Payment was successful", but the user remains on the "Payment" step and the cart icon still shows the added item count.

The final order confirmation with "Thanks for your order!" and an invoice number is shown only after clicking "Confirm" a second time. The cart icon is removed from the navigation only after the second click.

### Steps to Reproduce

| Step | Action | Test Data |
| --- | --- | --- |
| 1 | Log in and add a product to the cart. | N/A |
| 2 | Proceed through checkout until the "Payment" step. | N/A |
| 3 | Select "Cash on Delivery" from the payment method dropdown. | "Cash on Delivery" |
| 4 | Click "Confirm" once. | N/A |
| 5 | Check the page state and cart icon. | N/A |
| 6 | Click "Confirm" a second time. | N/A |
| 7 | Check the final order confirmation and cart icon. | N/A |

### Expected Result

After one valid click on "Confirm", the order is placed, the final order confirmation is displayed with "Thanks for your order!" and an invoice number, and the cart no longer shows the ordered item.

### Actual Result

After the first click on "Confirm", the message "Payment was successful" is displayed, but the user remains on the "Payment" step, the "Confirm" button is still visible, and the cart icon still shows the added item count. The final order confirmation appears only after clicking "Confirm" again. After the second click, the cart icon is removed from the navigation.

### Test Environment

| Date | OS | Browser | Device | App Version | Tested By |
| --- | --- | --- | --- | --- | --- |
| 2026-05-27 | Windows 11 | Chrome | Desktop | N/A | Danica Biljeljanin |

### Attachments

Screenshot attached in the test notes: "Payment was successful" message is shown while the user is still on the "Payment" step, the "Confirm" button remains visible, and the cart icon still shows the added item count.
