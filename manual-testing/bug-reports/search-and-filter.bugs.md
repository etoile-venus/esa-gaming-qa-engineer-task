# Search and Filter Bug Reports

## SEARCH_FILTER_BUG01 - No validation message is displayed when search query has fewer than 3 characters [Open]

| Severity | Priority | Related Test Case |
| --- | --- | --- |
| Low | Medium | `SEARCH_FILTER_TC02` - Verify that search is not executed when the query has fewer than 3 characters. |

### Description

The Home page search does not run when the search query has fewer than 3 characters, but no validation message is displayed.

According to AC6, the search should not be executed for fewer than 3 characters, and a validation error should be shown.

### Steps to Reproduce

| Step | Action | Test Data |
| --- | --- | --- |
| 1 | Open the Home page. | N/A |
| 2 | Enter fewer than 3 characters in the "Search" input. | `ha` |
| 3 | Click the "Search" button. | N/A |

### Expected Result

The search is not executed, and a validation message is displayed.

### Actual Result

The search is not executed, but no validation message is displayed.

### Test Environment

| Date | OS | Browser | Device | App Version | Tested By |
| --- | --- | --- | --- | --- | --- |
| 2026-05-25 | Windows 11 | Chrome | Desktop | N/A | Danica Biljeljanin |

### Attachments

To be added: screenshot or short video showing that no validation message is displayed after submitting `ha`.

## SEARCH_FILTER_BUG02 - Sort dropdown keeps the previous selected option after search resets sorting [Open]

| Severity | Priority | Related Test Case |
| --- | --- | --- |
| Low | Medium | `SEARCH_FILTER_TC05` - Verify that active filters are reset when a search query is submitted. |

### Description

Submitting a search query resets the applied sorting in the product grid, but the "Sort" dropdown still shows the previously selected sort option.

This creates an inconsistent UI state because the product grid no longer appears to use the selected sorting, while the dropdown suggests that the sorting option is still active.

### Steps to Reproduce

| Step | Action | Test Data |
| --- | --- | --- |
| 1 | Open the Home page. | N/A |
| 2 | Select a category filter. | "Hand Tools" |
| 3 | Select a brand filter. | Any visible brand |
| 4 | Select a sort option. | "Name (A - Z)" |
| 5 | Enter a valid search query in the "Search" input. | `hammer` |
| 6 | Click the "Search" button. | N/A |
| 7 | Check the product grid and the "Sort" dropdown. | N/A |

### Expected Result

Category, brand, and sorting filters are reset to their default state. The "Sort" dropdown shows the default value.

### Actual Result

The category and brand filters are reset, and the product grid no longer appears to use the previously selected sorting. However, the "Sort" dropdown still displays the previously selected sort option.

### Test Environment

| Date | OS | Browser | Device | App Version | Tested By |
| --- | --- | --- | --- | --- | --- |
| 2026-05-25 | Windows 11 | Chrome | Desktop | N/A | Danica Biljeljanin |

### Attachments

To be added: screenshot or short video showing the product grid after search and the "Sort" dropdown still showing the previous selected option.
