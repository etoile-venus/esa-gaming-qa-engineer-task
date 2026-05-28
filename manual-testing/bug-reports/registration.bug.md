# Registration Bug Reports

## REG_BUG01 - Registration accepts invalid email address formats [Open]

| Severity | Priority | Related Test Case                                                                           |
| -------- | -------- | ------------------------------------------------------------------------------------------- |
| Medium   | Medium   | `REG_TC04` - Verify that the user cannot register when the email address format is invalid. |

### Description

The registration form accepts some invalid email address formats and allows account creation.

Test data accepted during testing:

- `.email@example.com`
- `email..email@example.com`
- `email@example`
- `email@example..com`

### Steps to Reproduce

| Step | Action                                                                       | Test Data                                                                               |
| ---- | ---------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| 1    | Enter valid data in all required registration fields except "Email address". | Valid registration data                                                                 |
| 2    | Enter one of the invalid email values.                                       | `.email@example.com`, `email..email@example.com`, `email@example`, `email@example..com` |
| 3    | Click the "Register" button.                                                 | N/A                                                                                     |

### Expected Result

Registration is not completed, and the message "Email format is invalid" is displayed.

### Actual Result

Registration is completed for the invalid email values listed in the description.

### Test Environment

| Date       | OS         | Browser | Device  | App Version | Tested By          |
| ---------- | ---------- | ------- | ------- | ----------- | ------------------ |
| 2026-05-24 | Windows 11 | Chrome  | Desktop | N/A         | Danica Biljeljanin |

### Attachments

To be added: screenshot or short video showing that registration is completed with one invalid email value.

### Notes

The invalid email examples are based on the public source list [cjaoude/fd9910626629b53c4d25](https://gist.github.com/cjaoude/fd9910626629b53c4d25).

## REG_BUG02 - Registration accepts a password longer than 40 characters [Open]

| Severity | Priority | Related Test Case                                                                                        |
| -------- | -------- | -------------------------------------------------------------------------------------------------------- |
| Medium   | Medium   | `REG_TC05` - Verify that the user cannot register when the password length is outside the allowed range. |

### Description

The registration form accepts a password that is longer than the maximum length defined in the acceptance criteria.

The acceptance criteria define the allowed password length as 6-40 characters. During testing, a 41-character password was accepted and registration was completed.

### Steps to Reproduce

| Step | Action                                                                  | Test Data                                   |
| ---- | ----------------------------------------------------------------------- | ------------------------------------------- |
| 1    | Enter valid data in all required registration fields except "Password". | Valid registration data                     |
| 2    | Enter a password longer than 40 characters.                             | `A1!bcdefghijklmnopqrstuvwxyzABCDEFGHIJKLM` |
| 3    | Click the "Register" button.                                            | N/A                                         |

### Expected Result

Registration is not completed because the password is longer than 40 characters.

### Actual Result

Registration is completed with the 41-character password.

### Test Environment

| Date       | OS         | Browser | Device  | App Version | Tested By          |
| ---------- | ---------- | ------- | ------- | ----------- | ------------------ |
| 2026-05-24 | Windows 11 | Chrome  | Desktop | N/A         | Danica Biljeljanin |

### Attachments

To be added: screenshot or short video showing registration completed with the 41-character password.

### Notes

The 5-character password boundary was rejected with the message "Password must be minimal 6 characters long.", but the 41-character password boundary was accepted.

## REG_BUG03 - Password strength indicator shows inconsistent strength after repeated password changes [Open]

| Severity | Priority | Related Test Case |
| -------- | -------- | ----------------- |
| Low      | Low      | N/A               |

### Description

The password strength indicator on the registration form does not always match the current "Password" field value after the user repeatedly enters, clears, and re-enters password values.

During testing, the indicator sometimes showed a strong password state when the "Password" field was empty. In other cases, it showed weak strength for a password that matched the visible password rules.

### Preconditions

The user is on the customer registration page.

### Steps to Reproduce

| Step | Action                                                                                                   | Test Data             |
| ---- | -------------------------------------------------------------------------------------------------------- | --------------------- |
| 1    | Enter a valid password in the "Password" field.                                                          | `Qa27!flow`           |
| 2    | Clear the "Password" field.                                                                              | N/A                   |
| 3    | Enter another valid password in the "Password" field.                                                    | `A1!bcdef`            |
| 4    | Repeat clearing and re-entering password values several times.                                           | Valid password values |
| 5    | Check the password strength indicator after the field is cleared and after each new password is entered. | N/A                   |

### Expected Result

The password strength indicator resets when the "Password" field is empty and recalculates the strength based only on the current field value.

### Actual Result

The password strength indicator does not always match the current "Password" field value. It can show a strong password state when the field is empty, or show weak strength for a password that matches the visible password rules.

### Test Environment

| Date       | OS         | Browser | Device  | App Version | Tested By          |
| ---------- | ---------- | ------- | ------- | ----------- | ------------------ |
| 2026-05-27 | Windows 11 | Chrome  | Desktop | N/A         | Danica Biljeljanin |

### Attachments

To be added: short video showing the password field being cleared and re-entered while the strength indicator shows an incorrect state.

### Notes

This issue is easier to show with video because the incorrect indicator state appears after repeated field changes.

## REG_BUG04 - Duplicate email validation shows a different error message than expected [Open]

| Severity | Priority | Related Test Case                                                                               |
| -------- | -------- | ----------------------------------------------------------------------------------------------- |
| Low      | Low      | `REG_TC09` - Verify that the user cannot register with an email address that is already in use. |

### Description

The registration form prevents registration with an already registered email address, but it shows a different error message than the one defined in the acceptance criteria.

### Steps to Reproduce

| Step | Action                                                                  | Test Data                 |
| ---- | ----------------------------------------------------------------------- | ------------------------- |
| 1    | Enter valid data in all required registration fields.                   | Valid registration data   |
| 2    | Enter an already registered email address in the "Email address" field. | Existing registered email |
| 3    | Click the "Register" button.                                            | N/A                       |

### Expected Result

Registration is not completed, and the error message "Email is already in use." is displayed.

### Actual Result

Registration is not completed, but the message "A customer with this email address already exists." is displayed.

### Test Environment

| Date       | OS         | Browser | Device  | App Version | Tested By          |
| ---------- | ---------- | ------- | ------- | ----------- | ------------------ |
| 2026-05-24 | Windows 11 | Chrome  | Desktop | N/A         | Danica Biljeljanin |

### Attachments

To be added: screenshot showing the actual duplicate email validation message.

### Notes

The validation behavior works, but the displayed message does not match the acceptance criteria.

## REG_BUG05 - Registration accepts postal code values that do not contain exactly 5 digits [Open]

| Severity | Priority | Related Test Case                                                                                       |
| -------- | -------- | ------------------------------------------------------------------------------------------------------- |
| Medium   | Medium   | `REG_TC10` - Verify that the user cannot register when "Postal code" does not contain exactly 5 digits. |

### Description

The registration form accepts "Postal code" values with fewer than 5 digits and more than 5 digits, even though the acceptance criteria require exactly 5 digits.

Test data accepted during testing:

- `1234`
- `123456`

### Steps to Reproduce

| Step | Action                                                                     | Test Data               |
| ---- | -------------------------------------------------------------------------- | ----------------------- |
| 1    | Enter valid data in all required registration fields except "Postal code". | Valid registration data |
| 2    | Enter a "Postal code" value with fewer than 5 digits.                      | `1234`                  |
| 3    | Click the "Register" button.                                               | N/A                     |
| 4    | Repeat the test with a "Postal code" value with more than 5 digits.        | `123456`                |
| 5    | Click the "Register" button.                                               | N/A                     |

### Expected Result

Registration is not completed, and the user is informed that "Postal code" must contain exactly 5 digits.

### Actual Result

Registration is accepted with both invalid "Postal code" values listed in the description.

### Test Environment

| Date       | OS         | Browser | Device  | App Version | Tested By          |
| ---------- | ---------- | ------- | ------- | ----------- | ------------------ |
| 2026-05-24 | Windows 11 | Chrome  | Desktop | N/A         | Danica Biljeljanin |

### Attachments

To be added: screenshot or short video showing registration accepted with an invalid "Postal code" value.

### Notes

The acceptance criteria use "Postcode", while the UI label appears as "Postal code". This report treats them as the same field.
