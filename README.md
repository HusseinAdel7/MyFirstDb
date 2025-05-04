# Sales Tax Program: Technical Interview Documentation

## Objective

To fix, enhance, and extend a basic sales tax calculation program according to the provided rules and expectations. The code takes user input representing sale items, calculates applicable taxes, and prints a receipt. The task was part of a technical interview.

---

## Original Issues & Errors

The initial implementation of the system contained both **functional** and **design-level** issues. Below is a categorized breakdown:

### 1. Functional Errors

| Error Type          | Description                                             | Impact                           | Fix Implemented                      |
| ------------------- | ------------------------------------------------------- | -------------------------------- | ------------------------------------ |
| Incorrect Parsing   | Logic incorrectly assumed a maximum of 4 words in input | Parsing failed for valid entries | Improved input parsing logic         |
| Invalid Indexing    | Product name included `at` and price in some edge cases | Incorrect product names          | Used position of `at` keyword safely |
| Tax Overwriting Bug | Imported tax overwrote base tax rather than adding      | Incorrect tax for imported items | Accumulated both base and import tax |

### 2. Code Design Problems

| Issue                      | Description                                                   | Fix                                                 |
| -------------------------- | ------------------------------------------------------------- | --------------------------------------------------- |
| Magic Strings              | Product type detection relied on hardcoded keywords           | Encapsulated in `IsExemptProduct` method            |
| Mixed Responsibilities     | `SaleLine` calculated, formatted, and managed tax logic       | Separated rounding and logic into methods           |
| No Error Feedback          | `Add()` returned false but did not clarify the failure        | Added user messages for invalid inputs              |
| Inefficient Rounding Logic | Rounding was per-line instead of on total (extra credit task) | Implemented raw tax accumulation and total rounding |

---

## Enhancements & Improvements

| Area              | Improvement                                                                                |
| ----------------- | ------------------------------------------------------------------------------------------ |
| Input Parsing     | Now supports flexible length product names with reliable detection of `at` and price token |
| Tax Calculation   | Modular tax calculation with precise rounding and handling of both base and import taxes   |
| Code Organization | Clear separation of concerns via dedicated methods and refactoring                         |
| Error Handling    | Resilient against malformed input without crashing                                         |
| Readability       | Added meaningful method names, comments, and consistent formatting                         |
| Performance       | Reduced unnecessary object instantiations and string manipulations                         |

---

## Extra Credit Task: Rounding at Sale Level

### Problem:

The specification suggested that tax rounding be done on a **per-sale** basis rather than **per-line**, and that the receipt includes a “rounding adjustment”.

### Solution:

* Tracked **raw tax** (unrounded) and **rounded tax** at the line level.
* Summed raw tax across all lines.
* Calculated final tax using rounding on the **total tax amount**.
* Added a `Rounding Adjustment` line to the receipt.

### Example Receipt Output:

```
1 book: 12.49
1 music CD: 16.49
1 packet of chips: 0.85
Sales Taxes: 1.50
Rounding Adjustment: +0.01
Total: 29.83
```

---

## Final Result: All Tests Passed

| Test # | Description                             | Status                |
| ------ | --------------------------------------- | --------------------- |
| 1      | Basic products + tax exempt             | ✅ Passed              |
| 2      | Imported exempt and general goods       | ✅ Passed              |
| 3      | Mixed items including imported & exempt | ✅ Passed              |
| 4      | High quantity mix with all tax rules    | ✅ Passed              |
| 5      | Invalid input string                    | ✅ Handled Gracefully  |
| 6      | Empty input                             | ✅ Returns 0.00 totals |

---

## Summary

The final program is robust, accurate, readable, and extensible. It adheres to all functional and non-functional requirements given in the interview task, including the bonus extra-credit improvement. This reflects a good understanding of object-oriented design, input validation, tax logic abstraction, and user interaction handling.
