# Login Test Cases

## Scope

This file contains manual test cases for user login with email and password.

## LOGIN_TC01 - Verify that the login form is displayed when the user opens the login page

### Description

Verify that the login page shows the fields required for email and password login.

### Preconditions

The user is on the Home page and is not signed in.

### Test Steps

| Step | Action                       | Input Data | Expected Result                                                    |
| ---- | ---------------------------- | ---------- | ------------------------------------------------------------------ |
| 1    | Check the top navigation.     | N/A        | The "Sign in" link is visible.                                     |
| 2    | Click the "Sign in" link.    | N/A        | The login page is opened.                                          |
| 3    | Check the login form fields. | N/A        | The form shows the "Email address" field and the "Password" field. |
| 4    | Check the main action button. | N/A        | The "Login" button is visible.                                     |

### Execution Summary

**Actual Result:** Passed. The login page opened from the Home page after clicking "Sign in", and the "Email address" field, "Password" field, and "Login" button were visible.

| Date       | Environment        | Status  | Tested By          | Tags                      |
| ---------- | ------------------ | ------- | ------------------ | ------------------------- |
| 2026-05-25 | Chrome, Windows 11 | Passed | Danica Biljeljanin | Auth, Login, UI, Positive |

**Notes:** Covers AC1.

## LOGIN_TC02 - Verify that the user cannot log in when the email field is empty

### Description

Verify that the login form requires an email address before submission.

### Preconditions

The user is on the login page, is not signed in, and is already registered.

### Test Steps

| Step | Action                                 | Input Data     | Expected Result                                                           |
| ---- | -------------------------------------- | -------------- | ------------------------------------------------------------------------- |
| 1    | Leave the "Email address" field empty. | N/A            | The "Email address" field remains empty.                                  |
| 2    | Enter a value in the "Password" field. | Valid password | The password is entered.                                                  |
| 3    | Click the "Login" button.              | N/A            | The user is not logged in.                                                |
| 4    | Check the email validation.            | N/A            | The validation message "Email is required" is displayed. |

### Execution Summary

**Actual Result:** Passed. The user was not logged in, and the validation message "Email is required" was displayed.

| Date       | Environment        | Status  | Tested By          | Tags                                     |
| ---------- | ------------------ | ------- | ------------------ | ---------------------------------------- |
| 2026-05-25 | Chrome, Windows 11 | Passed | Danica Biljeljanin | Auth, Login, Email, Validation, Negative |

**Notes:** Covers AC2.

## LOGIN_TC03 - Verify that the user cannot log in when the email format is invalid

### Description

Verify that the login form validates the format of the email address.

### Preconditions

The user is on the login page, is not signed in, and is already registered.

### Test Steps

| Step | Action                                                       | Input Data                                                                                                     | Expected Result                                               |
| ---- | ------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| 1    | Enter an invalid email address in the "Email address" field. | `invalid-email`<br>`.email@example.com`<br>`email..email@example.com`<br>`email@example`<br>`name@email`<br>`email@example..com` | The invalid email value is entered.                           |
| 2    | Enter a value in the "Password" field.                       | Valid password                                                                                                | The password is entered.                                      |
| 3    | Click the "Login" button for each invalid email value.       | N/A                                                                                                            | The user is not logged in.                                    |
| 4    | Check the email validation for each invalid email value.      | N/A                                                                                                            | The validation message "Email format is invalid" is displayed. |

### Execution Summary

**Actual Result:** Failed. The validation message "Email format is invalid" was displayed for the tested invalid email values except email values without a valid top-level domain. A user could register with `name@email` and then log in with `name@email`.

| Date       | Environment        | Status  | Tested By          | Tags                                     |
| ---------- | ------------------ | ------- | ------------------ | ---------------------------------------- |
| 2026-05-25 | Chrome, Windows 11 | Failed | Danica Biljeljanin | Auth, Login, Email, Validation, Negative |

**Notes:** Covers AC2. Values such as `email@example` and `name@email` should be treated as invalid email formats because they do not contain a valid top-level domain. See `LOGIN_BUG01`.

## LOGIN_TC04 - Verify that the user cannot log in when the password field is empty

### Description

Verify that the login form requires a password before submission.

### Preconditions

The user is on the login page, is not signed in, and is already registered.

### Test Steps

| Step | Action                                                   | Input Data         | Expected Result                                                      |
| ---- | -------------------------------------------------------- | ------------------ | -------------------------------------------------------------------- |
| 1    | Enter a valid email format in the "Email address" field. | `user@example.com` | The email address is entered.                                        |
| 2    | Leave the "Password" field empty.                        | N/A                | The "Password" field remains empty.                                  |
| 3    | Click the "Login" button.                                | N/A                | The user is not logged in.                                           |
| 4    | Check the password validation.                           | N/A                | The validation message "Password is required" is displayed.          |

### Execution Summary

**Actual Result:** Passed. The user was not logged in, and the validation message "Password is required" was displayed.

| Date       | Environment        | Status  | Tested By          | Tags                                        |
| ---------- | ------------------ | ------- | ------------------ | ------------------------------------------- |
| 2026-05-25 | Chrome, Windows 11 | Passed | Danica Biljeljanin | Auth, Login, Password, Validation, Negative |

**Notes:** Covers AC3.

## LOGIN_TC05 - Verify that the user is successfully logged in when valid credentials are submitted

### Description

Verify that a registered user can log in with a valid email address and password.

### Preconditions

The user is on the login page, is not signed in, and is already registered.

### Test Steps

| Step | Action                                                           | Input Data               | Expected Result                                  |
| ---- | ---------------------------------------------------------------- | ------------------------ | ------------------------------------------------ |
| 1    | Enter a valid email address in the "Email address" field. | Valid email address | The email address is entered.                    |
| 2    | Enter the matching password in the "Password" field.             | Valid password           | The password is entered.                         |
| 3    | Click the "Login" button.                                        | N/A                      | The user is authenticated.                       |
| 4    | Check the page after login.                                      | N/A                      | The user is redirected to the account dashboard. |

### Execution Summary

**Actual Result:** Passed. The user was logged in and redirected to the account dashboard.

| Date       | Environment        | Status  | Tested By          | Tags                  |
| ---------- | ------------------ | ------- | ------------------ | --------------------- |
| 2026-05-25 | Chrome, Windows 11 | Passed | Danica Biljeljanin | Auth, Login, Positive |

**Notes:** Covers AC4.

## LOGIN_TC06 - Verify that the user cannot log in when an incorrect email or password is submitted

### Description

Verify that the login form rejects invalid credentials and shows the correct error message.

### Preconditions

The user is on the login page, is not signed in, and is already registered.

### Test Steps

| Step | Action                                               | Input Data                              | Expected Result                                             |
| ---- | ---------------------------------------------------- | --------------------------------------- | ----------------------------------------------------------- |
| 1    | Enter an email address in the "Email address" field. | Incorrect or unregistered email address | The email address is entered.                               |
| 2    | Enter a password in the "Password" field.            | Incorrect password                      | The password is entered.                                    |
| 3    | Click the "Login" button.                            | N/A                                     | The user is not logged in.                                  |
| 4    | Check the login error message.                       | N/A                                     | The error message "Invalid email or password" is displayed. |

### Execution Summary

**Actual Result:** Passed. The user was not logged in, and the message "Invalid email or password" was displayed.

| Date       | Environment        | Status  | Tested By          | Tags                               |
| ---------- | ------------------ | ------- | ------------------ | ---------------------------------- |
| 2026-05-25 | Chrome, Windows 11 | Passed | Danica Biljeljanin | Auth, Login, Credentials, Negative |

**Notes:** Covers AC5.
