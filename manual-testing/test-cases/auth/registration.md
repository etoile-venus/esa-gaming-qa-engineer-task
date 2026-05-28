# Registration Test Cases

## Scope

This file contains manual test cases for account registration behavior.

## Traceability Matrix

| Requirement | Covered By | Notes |
| --- | --- | --- |
| AC1 - Registration page is accessible | `REG_TC01` | Checks navigation to the registration page and visibility of the registration form. |
| AC2 - Required registration fields are displayed and validated | `REG_TC02`, `REG_TC03`, `REG_TC10` | `REG_TC02` checks field visibility. `REG_TC03` checks empty required field validation. `REG_TC10` checks the 5-digit "Postal code" requirement. |
| AC3 - Email address must match a valid format | `REG_TC04`, `REG_TC08` | `REG_TC04` checks invalid email values. `REG_TC08` includes successful registration with a valid unique email. |
| AC4 - Password must be 6-40 characters long | `REG_TC05` | Checks invalid password length boundary values. |
| AC5 - Duplicate email shows the expected error message | `REG_TC09` | Checks that registration is blocked when the email is already registered. |
| AC6 - Successful registration with valid data | `REG_TC08` | Checks account creation with valid required data. |
| Additional visible password rules | `REG_TC06` | Checks visible password character-type requirements. |
| Additional password UI behavior | `REG_TC07` | Checks the password visibility toggle. |

## REG_TC01 - Verify that the registration page opens when the user clicks "Register your account"

### Description

Verify that the user can open the customer registration page from the login page.

### Preconditions

The user is on the Home page and is not signed in.

### Test Steps

| Step | Action                                            | Input Data | Expected Result                                                                                                                                    |
| ---- | ------------------------------------------------- | ---------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1    | Click the "Sign in" link in the top navigation.   | N/A        | The login page is opened.                                                                                                                          |
| 2    | Click the "Register your account" link.           | N/A        | The customer registration page is opened.                                                                                                          |
| 3    | Check the registration page URL and form content. | N/A        | The URL is `https://practicesoftwaretesting.com/auth/register`, the form heading is "Customer registration", and the "Register" button is visible. |

### Execution Summary

**Actual Result:** Passed. The registration page opened successfully from the login page.

| Date       | Environment        | Status | Tested By          | Tags                                     |
| ---------- | ------------------ | ------ | ------------------ | ---------------------------------------- |
| 2026-05-24 | Chrome, Windows 11 | Passed | Danica Biljeljanin | Auth, Registration, Navigation, Positive |

**Notes:** The browser title may show `Register`; this test verifies the registration form heading and URL.

## REG_TC02 - Verify that the registration form shows all expected fields when the page is opened

### Description

Verify that the registration form contains the fields needed to create a customer account.

### Preconditions

The user is on the customer registration page.

### Test Steps

| Step | Action                              | Input Data | Expected Result                                                                                                                                                                                                                                                        |
| ---- | ----------------------------------- | ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1    | Check the registration form fields. | N/A        | The form shows:<br>- Personal details fields: "First name", "Last name", "Date of Birth"<br>- Address details fields: "Street", "House number", "Postal code", "City", "State", "Country"<br>- Contact field: "Phone"<br>- Account fields: "Email address", "Password" |
| 2    | Check the password area.            | N/A        | The password visibility toggle, password rules, and password strength indicator are visible.                                                                                                                                                                           |
| 3    | Check the main action button.       | N/A        | The "Register" button is visible.                                                                                                                                                                                                                                      |

### Execution Summary

**Actual Result:** Passed. The registration form showed all expected fields, the password UI elements, and the "Register" button.

| Date       | Environment        | Status | Tested By          | Tags                             |
| ---------- | ------------------ | ------ | ------------------ | -------------------------------- |
| 2026-05-24 | Chrome, Windows 11 | Passed | Danica Biljeljanin | Auth, Registration, UI, Positive |

**Notes:** The "Address" acceptance criterion is represented in the UI by "Street" and "House number".

## REG_TC03 - Verify that the user cannot register when required fields are empty

### Description

Verify that the registration form does not accept an empty submission.

### Preconditions

The user is on the customer registration page.

### Test Steps

| Step | Action                               | Input Data | Expected Result                                                                            |
| ---- | ------------------------------------ | ---------- | ------------------------------------------------------------------------------------------ |
| 1    | Leave all registration fields empty. | N/A        | The form remains empty.                                                                    |
| 2    | Click the "Register" button.         | N/A        | Registration is not completed.                                                             |
| 3    | Check the form validation.           | N/A        | Each required field shows a validation message in the format `"{Field Name} is required"`. |

### Execution Summary

**Actual Result:** Passed. Registration was not completed, and each required field showed a validation message in the format `"{Field Name} is required"`.

| Date       | Environment        | Status | Tested By          | Tags                                     |
| ---------- | ------------------ | ------ | ------------------ | ---------------------------------------- |
| 2026-05-24 | Chrome, Windows 11 | Passed | Danica Biljeljanin | Auth, Registration, Validation, Negative |

**Notes:** This test verifies the empty form behavior and confirms that required field validation is shown for all required fields at the same time.

## REG_TC04 - Verify that the user cannot register when the email address format is invalid

### Description

Verify that the registration form validates the email address format.

### Preconditions

The user is on the customer registration page, and all required fields except "Email address" are filled in with valid data in a valid format.

### Test Steps

| Step | Action                                                          | Input Data                                                                                                                                                                                                                 | Expected Result                                                |
| ---- | --------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| 1    | Enter valid data in all required fields except "Email address". | Valid registration data                                                                                                                                                                                                    | The form accepts the entered values.                           |
| 2    | Enter an invalid email address from the test data set.          | `plainaddress`<br>`@example.com`<br>`email.example.com`<br>`email@example@example.com`<br>`.email@example.com`<br>`email..email@example.com`<br>`email@example`<br>`email@example..com`<br>`Joe Smith <email@example.com>` | The invalid email value is entered.                            |
| 3    | Click the "Register" button for each invalid email value.       | N/A                                                                                                                                                                                                                        | Registration is not completed for each invalid email value.    |
| 4    | Check the email validation for each invalid email value.        | N/A                                                                                                                                                                                                                        | The user is informed that the email address format is invalid. |

### Execution Summary

**Actual Result:** Failed. The message "Email format is invalid" was shown for some invalid email values, but registration was accepted for `.email@example.com`, `email..email@example.com`, `email@example`, and `email@example..com`.

| Date       | Environment        | Status | Tested By          | Tags                                            |
| ---------- | ------------------ | ------ | ------------------ | ----------------------------------------------- |
| 2026-05-24 | Chrome, Windows 11 | Failed | Danica Biljeljanin | Auth, Registration, Email, Validation, Negative |

**Notes:** The selected test data covers missing `@`, missing local part, missing domain separator, multiple `@` symbols, invalid dot placement, missing top-level domain, double dots in the domain, and display-name style input. The invalid email examples are based on the public source list [cjaoude/fd9910626629b53c4d25](https://gist.github.com/cjaoude/fd9910626629b53c4d25). Observed validation message for rejected values: "Email format is invalid". The accepted invalid email values are tracked in `REG_BUG01`.

## REG_TC05 - Verify that the user cannot register when the password length is outside the allowed range

### Description

Verify invalid password length boundary values.

### Preconditions

The user is on the customer registration page, and all required fields except "Password" are filled in with valid data in a valid format.

### Test Steps

| Step | Action                                                      | Input Data                                  | Expected Result                                                                  |
| ---- | ----------------------------------------------------------- | ------------------------------------------- | -------------------------------------------------------------------------------- |
| 1    | Enter a password below the minimum length.                  | `A1!bc`                                     | The 5-character password is entered.                                             |
| 2    | Click the "Register" button.                                | N/A                                         | Registration is not completed because the password is shorter than 6 characters. |
| 3    | Replace the password with a value above the maximum length. | `A1!bcdefghijklmnopqrstuvwxyzABCDEFGHIJKLM` | The 41-character password is entered.                                            |
| 4    | Click the "Register" button.                                | N/A                                         | Registration is not completed because the password is longer than 40 characters. |

### Execution Summary

**Actual Result:** Failed. The 5-character password was rejected with the message "Password must be minimal 6 characters long.", but the 41-character password was accepted and registration was completed.

| Date       | Environment        | Status | Tested By          | Tags                                          |
| ---------- | ------------------ | ------ | ------------------ | --------------------------------------------- |
| 2026-05-24 | Chrome, Windows 11 | Failed | Danica Biljeljanin | Auth, Registration, Password, BVA, Validation |

**Notes:** The acceptance criteria define password length as 6-40 characters. This negative test uses Boundary Value Analysis for invalid boundary values only. Observed validation message for the 5-character password: "Password must be minimal 6 characters long." The 41-character password behavior is tracked in `REG_BUG02`.

## REG_TC06 - Verify that the user cannot register when the password does not meet character type requirements

### Description

Verify that the password validation works when the password is missing an uppercase letter, a lowercase letter, a number, or a special symbol.

### Preconditions

The user is on the customer registration page, and all required fields except "Password" are filled in with valid data in a valid format.

### Test Steps

| Step | Action                                                        | Input Data    | Expected Result                                                                          |
| ---- | ------------------------------------------------------------- | ------------- | ---------------------------------------------------------------------------------------- |
| 1    | Enter a password without an uppercase letter.                 | `lowercase7!` | The password is entered.                                                                 |
| 2    | Click the "Register" button.                                  | N/A           | Registration is not completed because the password does not contain an uppercase letter. |
| 3    | Replace the password with a value without a lowercase letter. | `UPPERCASE7!` | The password is entered.                                                                 |
| 4    | Click the "Register" button.                                  | N/A           | Registration is not completed because the password does not contain a lowercase letter.  |
| 5    | Replace the password with a value without a number.           | `NoNumber!`   | The password is entered.                                                                 |
| 6    | Click the "Register" button.                                  | N/A           | Registration is not completed because the password does not contain a number.            |
| 7    | Replace the password with a value without a special symbol.   | `NoSymbol7`   | The password is entered.                                                                 |
| 8    | Click the "Register" button.                                  | N/A           | Registration is not completed because the password does not contain a special symbol.    |

### Execution Summary

**Actual Result:** Passed. Registration was not completed when the password was missing a required character type.

| Date       | Environment        | Status  | Tested By          | Tags                                               |
| ---------- | ------------------ | ------- | ------------------ | -------------------------------------------------- |
| 2026-05-24 | Chrome, Windows 11 | Passed | Danica Biljeljanin | Auth, Registration, Password, Validation, Negative |

**Notes:** This test checks one password example for each missing character type. Avoid commonly breached passwords when the goal is to test password rules. Password length is covered separately in `REG_TC05`.

## REG_TC07 - Verify that the password visibility changes when the user clicks the visibility icon

### Description

Verify that the user can show and hide the password value on the registration form.

### Preconditions

The user is on the customer registration page.

### Test Steps

| Step | Action                                    | Input Data  | Expected Result                                |
| ---- | ----------------------------------------- | ----------- | ---------------------------------------------- |
| 1    | Enter a password in the "Password" field. | `Qa27!flow` | The password is entered and hidden by default. |
| 2    | Click the password visibility icon.       | N/A         | The password value becomes visible.            |
| 3    | Click the password visibility icon again. | N/A         | The password value is hidden again.            |

### Execution Summary

**Actual Result:** Passed. The password value became visible after clicking the visibility icon and was hidden again after clicking the icon a second time.

| Date       | Environment        | Status  | Tested By          | Tags                             |
| ---------- | ------------------ | ------- | ------------------ | -------------------------------- |
| 2026-05-24 | Chrome, Windows 11 | Passed | Danica Biljeljanin | Auth, Registration, Password, UI |

**Notes:** This checks only the visibility toggle behavior.

## REG_TC08 - Verify that the user can register when all required fields contain valid data

### Description

Verify that a new customer account can be created when all required registration fields contain valid data.

### Preconditions

The user is on the customer registration page and the email address used for this test is not already registered.

### Test Steps

| Step | Action                                   | Input Data                                                                                                                                                                                                                 | Expected Result                                                          |
| ---- | ---------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| 1    | Enter valid personal details.            | "First name": `Test`<br>"Last name": `User`<br>"Date of Birth": `1990-01-01`                                                                                                                                              | The personal details are entered.                                        |
| 2    | Enter valid address details.             | "Country": valid country<br>"Postal code": valid 5-digit postal code<br>"House number": valid house number<br>"Street": valid street<br>"City": valid city<br>"State": valid state                                      | The address details are entered or filled automatically where supported. |
| 3    | Enter valid contact and account details. | "Phone": valid phone number<br>"Email address": unique valid email<br>"Password": `Qa27!flow`                                                                                                                            | The contact and account details are entered.                             |
| 4    | Click the "Register" button.             | N/A                                                                                                                                                                                                                        | The account is created and the user is redirected to the login page.     |

### Execution Summary

**Actual Result:** Passed. The account was created successfully when all required fields contained valid data.

| Date       | Environment        | Status  | Tested By          | Tags                         |
| ---------- | ------------------ | ------- | ------------------ | ---------------------------- |
| 2026-05-24 | Chrome, Windows 11 | Passed | Danica Biljeljanin | Auth, Registration, Positive |

**Notes:** Use a new unique email address for each execution. Confirm the exact post-registration redirect during testing.

## REG_TC09 - Verify that the user cannot register with an email address that is already in use

### Description

Verify that the registration form prevents account creation when the entered email address is already registered.

### Preconditions

The user is on the customer registration page and a registered email address is available for testing.

### Test Steps

| Step | Action                                                                  | Input Data                | Expected Result                                            |
| ---- | ----------------------------------------------------------------------- | ------------------------- | ---------------------------------------------------------- |
| 1    | Enter valid data in all required fields.                                | Valid registration data   | The form accepts the entered values.                       |
| 2    | Enter an already registered email address in the "Email address" field. | Existing registered email | The existing email address is entered.                     |
| 3    | Click the "Register" button.                                            | N/A                       | Registration is not completed.                             |
| 4    | Check the email validation message.                                     | N/A                       | The error message "Email is already in use." is displayed. |

### Execution Summary

**Actual Result:** Failed. Registration was not completed, but the displayed message was "A customer with this email address already exists." instead of the expected message "Email is already in use."

| Date       | Environment        | Status  | Tested By          | Tags                                |
| ---------- | ------------------ | ------- | ------------------ | ----------------------------------- |
| 2026-05-24 | Chrome, Windows 11 | Failed | Danica Biljeljanin | Auth, Registration, Email, Negative |

**Notes:** The exact message is defined by the acceptance criteria. The observed duplicate email message is tracked in `REG_BUG04`.

## REG_TC10 - Verify that the user cannot register when "Postal code" does not contain exactly 5 digits

### Description

Verify that the registration form validates the "Postal code" field against the 5-digit postcode requirement.

### Preconditions

The user is on the customer registration page.

### Test Steps

| Step | Action                                                        | Input Data              | Expected Result                                                                                          |
| ---- | ------------------------------------------------------------- | ----------------------- | -------------------------------------------------------------------------------------------------------- |
| 1    | Enter valid data in all required fields except "Postal code". | Valid registration data | The form accepts the entered values.                                                                     |
| 2    | Enter a "Postal code" value with fewer than 5 digits.         | `1234`                  | The value is entered.                                                                                    |
| 3    | Click the "Register" button.                                  | N/A                     | Registration is not completed and the user is informed that "Postal code" must contain exactly 5 digits. |
| 4    | Replace the "Postal code" value with more than 5 digits.      | `123456`                | The value is entered.                                                                                    |
| 5    | Click the "Register" button.                                  | N/A                     | Registration is not completed and the user is informed that "Postal code" must contain exactly 5 digits. |

### Execution Summary

**Actual Result:** Failed. Registration was accepted when "Postal code" contained fewer than 5 digits and when it contained more than 5 digits.

| Date       | Environment        | Status  | Tested By          | Tags                                                  |
| ---------- | ------------------ | ------- | ------------------ | ----------------------------------------------------- |
| 2026-05-24 | Chrome, Windows 11 | Failed | Danica Biljeljanin | Auth, Registration, Postal Code, Validation, Negative |

**Notes:** The acceptance criteria use "Postcode"; the UI label appears as "Postal code". The observed behavior is tracked in `REG_BUG05`.
