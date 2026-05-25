# Search and Filter Test Cases

## Scope

This file covers product search and filtering on the Home page.

Product detail navigation and standalone pagination checks are outside this scope. Pagination can still be checked as part of the result list when search or filters update the product grid.

## Traceability Matrix

| Requirement | Covered By | Notes |
| --- | --- | --- |
| AC5 - Search input is displayed | `SEARCH_FILTER_TC01` | Search field and search actions are checked with the main sidebar controls. |
| AC6 - Minimum search length | `SEARCH_FILTER_TC02` | Checks that fewer than 3 characters cannot be submitted. |
| AC7 - Maximum search length | `SEARCH_FILTER_TC03` | Checks the 40-character input limit. |
| AC8 - Search results displayed | `SEARCH_FILTER_TC04` | Checks that a valid search updates the product grid. |
| AC9 - Search resets filters | `SEARCH_FILTER_TC05` | Checks category, brand, and sorting reset after search. |
| AC10 - Category filter is displayed | `SEARCH_FILTER_TC01` | Covered with the sidebar controls check. |
| AC11 - Hierarchical categories | `SEARCH_FILTER_TC01` | Covered with parent and child category visibility. |
| AC12 - Selecting a parent category | `SEARCH_FILTER_TC06` | Checks parent category selection and child checkbox behavior. |
| AC13 - Deselecting child categories | `SEARCH_FILTER_TC07` | Checks that the parent category follows the child category selection state. |
| AC14 - Brand filter is displayed | `SEARCH_FILTER_TC01` | Covered with the sidebar controls check. |
| AC15 - Selecting a brand | `SEARCH_FILTER_TC08` | Checks brand filtering. |
| AC16 - Combining filters | `SEARCH_FILTER_TC09` | Checks category and brand filtering together. |
| AC17 - Sort dropdown is displayed | `SEARCH_FILTER_TC01` | Covered with the sidebar controls check. |
| AC18 - Sort options | `SEARCH_FILTER_TC10` | Checks the expected sort options. |
| AC19 - Applying a sort | `SEARCH_FILTER_TC11` | Checks that the selected sort order is applied to the product grid. |
| Visible price range filter | `SEARCH_FILTER_TC12` | Added because "Price Range" is a visible filter in the sidebar. |
| Visible sustainability filter | `SEARCH_FILTER_TC01`, `SEARCH_FILTER_TC13` | Added because "Show only eco-friendly products" is a visible filter in the sidebar. |

## SEARCH_FILTER_TC01 - Verify that search, filter, and sort controls are displayed on the Home page

### Description

Verify that the Home page shows the main controls needed for searching, filtering, and sorting products.

### Preconditions

The user is on the Home page.

### Test Steps

| Step | Action | Input Data | Expected Result |
| --- | --- | --- | --- |
| 1 | Check the Home page. | N/A | A product grid is displayed. |
| 2 | Check the "Search" section. | N/A | The search input, "X" button, and "Search" button are visible. |
| 3 | Check the "Filters" section. | N/A | Category checkboxes are visible in the sidebar. |
| 4 | Check the category structure. | N/A | Parent categories and child categories are shown in a tree structure. |
| 5 | Check the brand section. | N/A | Brand checkboxes are visible. |
| 6 | Check the "Price Range" section. | N/A | The price range slider is visible. |
| 7 | Check the "Sustainability" section. | N/A | The "Show only eco-friendly products" checkbox is visible. |
| 8 | Check the "Sort" section. | N/A | The sort dropdown is visible. |

### Execution Summary

**Actual Result:** Passed. The Home page displayed the product grid and all main search, filter, and sort controls. The "Search" section, category tree, brand filters, "Price Range" slider, "Show only eco-friendly products" checkbox, and "Sort" dropdown were visible.

| Date | Environment | Status | Tested By | Tags |
| --- | --- | --- | --- | --- |
| 2026-05-25 | Chrome, Windows 11 | Passed | Danica Biljeljanin | Catalog, Search, Filter, UI |

**Notes:** Covers AC5, AC10, AC11, AC14, and AC17. The price range and sustainability checks are added because they are visible product filters.

## SEARCH_FILTER_TC02 - Verify that search is not executed when the query has fewer than 3 characters

### Description

Verify that the search field validates the minimum search length before submitting the search.

### Preconditions

The user is on the Home page.

### Test Steps

| Step | Action | Input Data | Expected Result |
| --- | --- | --- | --- |
| 1 | Enter fewer than 3 characters in the search input. | `ha` | The value is entered in the search input. |
| 2 | Click the "Search" button. | N/A | The search is not executed. |
| 3 | Check the page. | N/A | A validation message is displayed, and the product grid is not filtered by the short query. |

### Execution Summary

**Actual Result:** Failed. The search was not executed when `ha` was submitted, but no validation message was displayed.

| Date | Environment | Status | Tested By | Tags |
| --- | --- | --- | --- | --- |
| 2026-05-25 | Chrome, Windows 11 | Failed | Danica Biljeljanin | Catalog, Search, Validation, Negative |

**Notes:** Covers AC6. The search blocking behavior worked, but the missing validation message does not match the expected result.

## SEARCH_FILTER_TC03 - Verify that the search input accepts a maximum of 40 characters

### Description

Verify that the search field does not accept more than 40 characters.

### Preconditions

The user is on the Home page.

### Test Steps

| Step | Action | Input Data | Expected Result |
| --- | --- | --- | --- |
| 1 | Enter a 40-character value in the search input. | `combinationplierscombinationpliers123456` | The full 40-character value is accepted. |
| 2 | Try to enter one more character. | `X` | The search input does not accept more than 40 characters. |

### Execution Summary

**Actual Result:** Passed. A 40-character search value was accepted and the page displayed the "Searched for:" text with the submitted value. When more than 40 characters were entered, the "Searched for:" text did not change or was not displayed.

| Date | Environment | Status | Tested By | Tags |
| --- | --- | --- | --- | --- |
| 2026-05-25 | Chrome, Windows 11 | Passed | Danica Biljeljanin | Catalog, Search, Validation, Boundary |

**Notes:** Covers AC7. The accepted 40-character value was `combinationplierscombinationpliers123456`.

## SEARCH_FILTER_TC04 - Verify that matching products are displayed when a valid search query is submitted

### Description

Verify that a valid search query updates the product grid and shows matching products only.

### Preconditions

The user is on the Home page.

### Test Steps

| Step | Action | Input Data | Expected Result |
| --- | --- | --- | --- |
| 1 | Enter a valid search query in the search input. | `pliers` | The search query is entered. |
| 2 | Click the "Search" button. | N/A | The product grid is updated. |
| 3 | Check the visible product cards. | N/A | The visible products match the search query. |

### Execution Summary

**Actual Result:** Passed. After submitting `pliers`, the product grid showed only products that have `pliers` in the product name.

| Date | Environment | Status | Tested By | Tags |
| --- | --- | --- | --- | --- |
| 2026-05-25 | Chrome, Windows 11 | Passed | Danica Biljeljanin | Catalog, Search, Positive |

**Notes:** Covers AC8.

## SEARCH_FILTER_TC05 - Verify that active filters are reset when a search query is submitted

### Description

Verify that submitting a search resets active category, brand, and sorting filters to their default state.

### Preconditions

The user is on the Home page.

### Test Steps

| Step | Action | Input Data | Expected Result |
| --- | --- | --- | --- |
| 1 | Select a category filter. | "Hand Tools" | The selected category filter is applied. |
| 2 | Select a brand filter. | Any visible brand | The selected brand filter is applied. |
| 3 | Select a sort option. | "Name (A - Z)" | The selected sort option is applied. |
| 4 | Enter a valid search query in the search input. | `hammer` | The search query is entered. |
| 5 | Click the "Search" button. | N/A | The search is submitted. |
| 6 | Check the filters and sort dropdown. | N/A | Category, brand, and sorting filters are reset to their default state. |
| 7 | Check the product grid. | N/A | The product grid shows products matching the search query. |

### Execution Summary

**Actual Result:** Failed. The category and brand filters were reset after submitting `hammer`, and the product grid showed matching search results. The sorting was no longer applied based on the product grid, but the sort dropdown still displayed the previously selected sort option.

| Date | Environment | Status | Tested By | Tags |
| --- | --- | --- | --- | --- |
| 2026-05-25 | Chrome, Windows 11 | Failed | Danica Biljeljanin | Catalog, Search, Filter, Reset |

**Notes:** Covers AC9. The result list reset behavior worked, but the sort dropdown did not return to its default state.

## SEARCH_FILTER_TC06 - Verify that child categories are selected when a parent category is selected

### Description

Verify that selecting a parent category also selects its child categories and updates the product grid.

### Preconditions

The user is on the Home page.

### Test Steps

| Step | Action | Input Data | Expected Result |
| --- | --- | --- | --- |
| 1 | Check the category filter tree. | N/A | A parent category with child categories is visible. |
| 2 | Select a parent category checkbox. | "Hand Tools" | All child category checkboxes under "Hand Tools" are checked. |
| 3 | Check the product grid. | N/A | The product grid updates to show products from the selected parent category and its child categories. |

### Execution Summary

**Actual Result:** Passed. Selecting "Hand Tools" selected all child category checkboxes under that parent category, and the product grid was updated.

| Date | Environment | Status | Tested By | Tags |
| --- | --- | --- | --- | --- |
| 2026-05-25 | Chrome, Windows 11 | Passed | Danica Biljeljanin | Catalog, Filter, Category, Positive |

**Notes:** Covers AC12.

## SEARCH_FILTER_TC07 - Verify that the parent category updates when child category selection changes

### Description

Verify that the parent category checkbox is checked when all child categories are checked, and unchecked when all child categories are cleared.

### Preconditions

The user is on the Home page.

### Test Steps

| Step | Action | Input Data | Expected Result |
| --- | --- | --- | --- |
| 1 | Check the category filter tree. | N/A | A parent category with child categories is visible. |
| 2 | Select each child category under one parent category. | Child categories under "Hand Tools" | Each selected child category is checked. |
| 3 | Check the parent category checkbox. | "Hand Tools" | The parent category checkbox is automatically checked. |
| 4 | Uncheck each selected child category under the same parent category. | Child categories under "Hand Tools" | Each selected child category is unchecked. |
| 5 | Check the parent category checkbox. | "Hand Tools" | The parent category checkbox is also unchecked. |
| 6 | Check the product grid. | N/A | The product grid updates according to the remaining active filters, or returns to the default product list if no filters are active. |

### Execution Summary

**Actual Result:** Passed. When all child categories under "Hand Tools" were selected, the parent category checkbox was automatically checked. After all child categories were unchecked, the parent category checkbox was also unchecked, and the product grid updated.

| Date | Environment | Status | Tested By | Tags |
| --- | --- | --- | --- | --- |
| 2026-05-25 | Chrome, Windows 11 | Passed | Danica Biljeljanin | Catalog, Filter, Category |

**Notes:** Covers AC13 and the observed child-to-parent checkbox behavior.

## SEARCH_FILTER_TC08 - Verify that products are filtered when a brand is selected

### Description

Verify that selecting a brand checkbox updates the product grid to show products from that brand.

### Preconditions

The user is on the Home page.

### Test Steps

| Step | Action | Input Data | Expected Result |
| --- | --- | --- | --- |
| 1 | Select one visible brand checkbox. | "ForgeFlex Tools" | The brand checkbox is checked. |
| 2 | Check the product grid. | N/A | The product grid updates to show only products from the selected brand. |
| 3 | Select another visible brand checkbox. | "MightyCraft Hardware" | Both selected brand checkboxes are checked. |
| 4 | Check the product grid. | N/A | The product grid shows products from the selected brands only. |

### Execution Summary

**Actual Result:** Passed. Selecting "ForgeFlex Tools" filtered the product grid to products from that brand. Selecting "MightyCraft Hardware" as an additional brand showed products from the selected brands only.

| Date | Environment | Status | Tested By | Tags |
| --- | --- | --- | --- | --- |
| 2026-05-25 | Chrome, Windows 11 | Passed | Danica Biljeljanin | Catalog, Filter, Brand, Positive |

**Notes:** Covers AC15.

## SEARCH_FILTER_TC09 - Verify that category and brand filters can be combined

### Description

Verify that the product grid shows only products matching both the selected category and selected brand filters.

### Preconditions

The user is on the Home page.

### Test Steps

| Step | Action | Input Data | Expected Result |
| --- | --- | --- | --- |
| 1 | Select a category filter. | "Pliers" | The category checkbox is checked. |
| 2 | Select a brand filter. | Any visible brand | The brand checkbox is checked. |
| 3 | Check the product grid. | N/A | The product grid shows only products that match both the selected category and the selected brand. |

### Execution Summary

**Actual Result:** Passed. After selecting the "Pliers" category and a visible brand filter, the product grid showed products matching both selected filters.

| Date | Environment | Status | Tested By | Tags |
| --- | --- | --- | --- | --- |
| 2026-05-25 | Chrome, Windows 11 | Passed | Danica Biljeljanin | Catalog, Filter, Category, Brand |

**Notes:** Covers AC16.

## SEARCH_FILTER_TC10 - Verify that the sort dropdown contains the expected options

### Description

Verify that the sort dropdown includes all expected sorting options.

### Preconditions

The user is on the Home page.

### Test Steps

| Step | Action | Input Data | Expected Result |
| --- | --- | --- | --- |
| 1 | Open the "Sort" dropdown. | N/A | The sort options are displayed. |
| 2 | Check the available sort options. | N/A | The dropdown includes "Name (A - Z)", "Name (Z - A)", "Price (High - Low)", and "Price (Low - High)". |

### Execution Summary

**Actual Result:** Passed. The sort dropdown included "Name (A - Z)", "Name (Z - A)", "Price (High - Low)", and "Price (Low - High)". It also included additional CO2 rating sort options from A to E and from E to A.

| Date | Environment | Status | Tested By | Tags |
| --- | --- | --- | --- | --- |
| 2026-05-25 | Chrome, Windows 11 | Passed | Danica Biljeljanin | Catalog, Sort, UI |

**Notes:** Covers AC18. Additional CO2 rating sort options are present, but the expected AC18 options are also available.

## SEARCH_FILTER_TC11 - Verify that products are sorted when a sort option is selected

### Description

Verify that selecting a sort option reloads the product grid in the selected order.

### Preconditions

The user is on the Home page.

### Test Steps

| Step | Action | Input Data | Expected Result |
| --- | --- | --- | --- |
| 1 | Open the "Sort" dropdown. | N/A | The sort options are displayed. |
| 2 | Select a price sort option. | "Price (Low - High)" | The selected sort option is applied. |
| 3 | Check the visible product prices. | N/A | Products are ordered from the lowest visible price to the highest visible price. |
| 4 | Select a name sort option. | "Name (A - Z)" | The selected sort option is applied. |
| 5 | Check the visible product names. | N/A | Products are ordered alphabetically by name. |

### Execution Summary

**Actual Result:** Passed. The selected price sort option ordered the visible products from the lowest price to the highest price. The selected name sort option ordered the visible products alphabetically by name.

| Date | Environment | Status | Tested By | Tags |
| --- | --- | --- | --- | --- |
| 2026-05-26 | Chrome, Windows 11 | Passed | Danica Biljeljanin | Catalog, Sort, Positive |

**Notes:** Covers AC19.

## SEARCH_FILTER_TC12 - Verify that products are filtered by the selected price range

### Description

Verify that changing the "Price Range" filter updates the product grid to show products within the selected price range.

### Preconditions

The user is on the Home page.

### Test Steps

| Step | Action | Input Data | Expected Result |
| --- | --- | --- | --- |
| 1 | Check the "Price Range" section. | N/A | The price range slider is visible. |
| 2 | Move the price range slider to a value that excludes at least one visible product. | Any lower price range value | The selected price range is applied. |
| 3 | Check the visible product prices. | N/A | Products outside the selected price range are not shown in the product grid. |

### Execution Summary

**Actual Result:** Passed. Changing the "Price Range" slider updated the product grid, and products outside the selected price range were not shown.

| Date | Environment | Status | Tested By | Tags |
| --- | --- | --- | --- | --- |
| 2026-05-26 | Chrome, Windows 11 | Passed | Danica Biljeljanin | Catalog, Filter, Price |

**Notes:** Price range is included because it is a visible product filter in the sidebar. Resetting the price range is not covered here because no separate reset control was confirmed for this filter.

## SEARCH_FILTER_TC13 - Verify that products are filtered when only eco-friendly products are selected

### Description

Verify that the sustainability filter updates the product grid to show only eco-friendly products.

### Preconditions

The user is on the Home page.

### Test Steps

| Step | Action | Input Data | Expected Result |
| --- | --- | --- | --- |
| 1 | Check the "Sustainability" section. | N/A | The "Show only eco-friendly products" checkbox is visible. |
| 2 | Select the "Show only eco-friendly products" checkbox. | N/A | The checkbox is checked and the product grid is updated. |
| 3 | Check the visible product cards. | N/A | Only products that match the eco-friendly filter are shown. |
| 4 | Clear the "Show only eco-friendly products" checkbox. | N/A | The checkbox is unchecked and the product grid returns to the wider product list. |

### Execution Summary

**Actual Result:** Passed. Selecting "Show only eco-friendly products" updated the product grid to show only products matching the eco-friendly filter. Clearing the checkbox returned the product grid to the wider product list.

| Date | Environment | Status | Tested By | Tags |
| --- | --- | --- | --- | --- |
| 2026-05-26 | Chrome, Windows 11 | Passed | Danica Biljeljanin | Catalog, Filter, Sustainability |

**Notes:** Added because "Show only eco-friendly products" is a visible filter in the sidebar.
