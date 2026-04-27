# Excel Essentials: Performing Calculations & Relational Logic

## 1. Formula Fundamentals

Formulas are the engines that turn static numbers into dynamic data. Every formula in Excel begins with the equals sign (`=`).

**Core Terminology**
- **Operators** — The mathematical instructions: `+` (Addition), `-` (Subtraction), `*` (Multiplication), and `/` (Division).
- **Cell Reference** — Using a cell address (e.g., `B3`) instead of a hard-coded number. This ensures the formula updates automatically when the source data changes.
- **Order of Operations** — Excel follows standard mathematical priority (PEMDAS/BODMAS): Parentheses first, then Exponents, Multiplication/Division, and finally Addition/Subtraction.

## 2. Basic Functions: SUM, MIN, MAX, and AVERAGE

Functions are pre-built formulas that handle complex math with a single word.

- **SUM & AutoSum** — Quickly totals a range. Shortcut: `Alt + =` automatically identifies and highlights the most likely range of numbers to sum.
- **AVERAGE** — Calculates the arithmetic mean. Ideal for finding "Expected Value" in financial models.
- **MIN & MAX** — Identify the "Floor" (lowest value) and the "Ceiling" (highest value) in a dataset. Useful for identifying best and worst-performing assets.

## 3. The "Anchor": Absolute Cell References

By default, Excel uses **Relative References**. If you copy a formula down one row, the cell addresses in the formula also move down one row. Absolute references "lock" a specific cell in place.

- **The Syntax** — Adding a dollar sign (`$`) before the column and row (e.g., `$B$3`) prevents that reference from moving when the formula is copied or filled.
- **The Shortcut** — Highlight the cell reference in the formula bar and press **`F4`** to toggle through absolute options:
  - `$A$1` (Total Lock)
  - `A$1` (Row Lock)
  - `$A1` (Column Lock)

## 4. Multi-Sheet Architecture

Data and calculations don't have to live on the same page. Linking sheets allows for a "clean" interface where data entry happens in one place and calculations happen in another.

- **Syntax** — To reference a cell on another sheet, use the sheet name followed by an exclamation point: `= 'Sheet Name'!A1`.
- **Best Practice** — If a sheet name contains spaces, it must be enclosed in single quotes. Clicking the target cell while writing the formula handles this syntax automatically.

## 5. Master Ranges (Named Ranges)

Named Ranges replace coordinate-based math (like `$B$3`) with descriptive labels. 

- **The Benefit** — Formulas become readable: `=Total_Assets * Management_Fee` is easier to audit than `=D14 * $B$1`.
- **Creation** — Select a cell or range and type the name directly into the **Name Box** (to the left of the formula bar). 
- **Scope** — Once named, that range can be accessed from any sheet in the entire workbook without needing the `'Sheet Name'!` prefix.

---

## 6. Project Nimbus / RevOps Applications

**Dynamic Wealth Simulations**
Use an **"Inputs" Sheet** for variables like `Annual_Contribution`, `Expected_Growth_Rate`, and `Tax_Bracket`. Link these to a **"Projections" Sheet** using Absolute References or Named Ranges. This allows a Wealth Advisor to sit with a client and change one "Input" to watch the entire 30-year projection "ripple" and update instantly.

**Cross-Object Auditing**
When preparing data for Salesforce, you often have a "Leads" export on Sheet 1 and a "Campaign Costs" export on Sheet 2. Use **Calculations Across Sheets** to subtract Campaign Costs from Lead Revenue to calculate your **Return on Ad Spend (ROAS)** before importing the final results into a GTM Analytics dashboard.

**Governance Validation**
Use **MAX and MIN** to create "Safety Guardrails" in your financial models. For example, if a boutique firm has a policy that management fees cannot exceed 2%, use a formula like `=MIN(Calculated_Fee, 0.02)` to ensure the output stays within the firm's governance limits regardless of user input.
