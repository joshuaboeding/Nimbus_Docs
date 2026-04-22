# Corporate Finance: Taxes and the After-Tax Discount Rate

## 1. Core Concept: Taxes as a Return Reducer

In a vacuum, earning 5% interest grows your money by exactly 5%. In reality,
the government treats interest income as taxable — you only keep a portion of
the return your capital generates.

Key observation: if you do not account for taxes in your initial calculation,
you will run out of money before your time horizon ends.

## 2. The After-Tax Discount Rate

To calculate how much you truly need to save today to meet a future goal, you
must adjust your discount rate to reflect what you actually keep after tax.

**Formula:**

Rt = R x (1 - t)

- R = pre-tax (nominal) discount rate
- t = marginal tax rate (expressed as a decimal)
- Rt = after-tax discount rate (the effective growth rate you actually keep)

**Numerical Example**

- Pre-tax return (R): 5% (0.05)
- Tax rate (t): 35% (0.35)
- Calculation: 0.05 x (1 - 0.35) = 0.0325
- Result: effective growth rate is 3.25%, not 5%

## 3. Impact on Present Value

Because the effective growth rate is lower after tax, the Present Value required
to reach the same future goal must be higher.

- **Tax-free world** — less money needed today because 100% of interest compounds
- **Taxed world** — more money needed today to compensate for the leakage caused
  by ongoing tax payments

The difference between the PV calculated at the pre-tax rate and the PV
calculated at the after-tax rate is exactly equal to the Present Value of all
future tax payments.

## 4. RevOps Connection

**Net Revenue Tracking**
In RevOps, Gross Revenue vs. Net Revenue (after discounts, rebates, and taxes)
follows the same logic — the effective number is always lower than the headline.

**Cost of Capital and WACC**
When a company borrows money to grow, the interest paid is often tax-deductible.
This is the inverse of the video example — it makes the effective cost of debt
lower: R x (1 - t). This is a core input in calculating a company's WACC
(Weighted Average Cost of Capital).

## 5. Tethered Wealth Applications

**Location Optimization**
An expat moving from a high-tax country (Japan) to a zero-tax country (UAE)
sees their Rt increase significantly without changing their investments at all.
Build a Salesforce tool that compares Rt across different client jurisdictions
to quantify the tax efficiency gain of relocation.

**Account Selection — Roth vs. Traditional IRA**
- Traditional IRA: taxes applied at withdrawal — PV calculated pre-tax but
  future cash flows are reduced by the tax rate at distribution
- Roth IRA: taxes applied today — initial capital is reduced but all future
  cash flows are completely tax-free

Use the Rt formula to show a client exactly which account type produces a higher
terminal value by their target date, given their current and expected future
tax rates.