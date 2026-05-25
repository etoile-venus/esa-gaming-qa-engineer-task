# Login Bug Reports

## LOGIN_BUG01 - Login accepts an invalid email address without a valid top-level domain [Open]

| Severity | Priority | Related Test Case |
| --- | --- | --- |
| Medium | Medium | `LOGIN_TC03` - Verify that the user cannot log in when the email format is invalid. |

### Description

The login form allows authentication with an invalid email address format when the account was previously registered with the same invalid email value.

During testing, an account was registered with `name@email`. After that, the user could log in with `name@email`, even though this value does not contain a valid top-level domain.

### Steps to Reproduce

| Step | Action | Test Data |
| --- | --- | --- |
| 1 | Register a user account with an invalid email address format. | `name@email` |
| 2 | Open the login page. | N/A |
| 3 | Enter the same invalid email address in the "Email address" field. | `name@email` |
| 4 | Enter the matching password in the "Password" field. | Valid password for the registered account |
| 5 | Click the "Login" button. | N/A |

### Expected Result

The user is not logged in, and the message "Email format is invalid" is displayed.

### Actual Result

The user is logged in with `name@email`.

### Test Environment

| Date | OS | Browser | Device | App Version | Tested By |
| --- | --- | --- | --- | --- | --- |
| 2026-05-25 | Windows 11 | Chrome | Desktop | N/A | Danica Biljeljanin |

### Attachments

To be added: screenshot or short video showing login completed with `name@email`.

### Notes

This issue is related to the Registration email validation issue because the invalid email address can first be accepted during registration.
