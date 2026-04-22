# Corporate Finance: Time Value of Money Shortcuts

## 1. Core Principles of Cash Flow Shortcuts

To avoid discounting dozens of individual cash flows one by one, finance uses
shortcut formulas for recurring cash flow patterns.

**Two Strict Rules for Application**

Both conditions must be met before using any shortcut formula:

- **Equal Spacing** — the time interval between every cash flow must be exactly
  the same (e.g., exactly one year, one month)
- **The One Period Rule** — formulas assume the first cash flow arrives exactly
  one period from today. If a cash flow occurs at Time 0 (today), it must be
  added separately outside the formula

## 2. The Four Primary Cash Flow Streams

### A. The Annuity

A finite stream of cash flows of identical magnitude and equal spacing in time.

**Examples:** home mortgages, auto leases, amortizing loans, insurance payouts

**Present Value Formula:**

PV = (CF / R) x (1 - 1 / (1 + R)^T)

- CF = Cash Flow per period
- R = Discount Rate
- T = Number of Periods

---

### B. The Growing Annuity

A finite stream of equally spaced cash flows that grows at a constant rate (g)
each period.

**Examples:** multi-year salary contracts, inflation-adjusted savings strategies,
project revenue streams

**Present Value Formula:**

PV = (CF1 / (R - g)) x (1 - ((1 + g) / (1 + R))^T)

- CF1 = Cash flow at period 1
- R = Discount Rate
- g = Growth Rate
- T = Number of Periods

---

### C. The Perpetuity

An infinite stream of cash flows of identical magnitude and equal spacing in time.

**Examples:** UK Consol bonds, certain preferred stocks

**Present Value Formula:**

PV = CF / R

Note: An infinite stream does not require an infinite amount of money to fund.
The present value of cash flows received 100+ years from now approaches zero,
so the total sum converges to a finite number.

---

### D. The Growing Perpetuity

An infinite stream of equally spaced cash flows that grows at a constant rate (g)
forever.

**Examples:** stock valuation via dividend discount models — assumes a company
operates indefinitely and grows its dividend at a constant rate

**Present Value Formula:**

PV = CF1 / (R - g)

- CF1 = Cash flow at period 1
- R = Discount Rate
- g = Growth Rate (must be less than R or the formula breaks)

---

## 3. Tethered Wealth Applications

**Retirement Drawdown — Annuity**
An expat client wants to know how much they need in their brokerage account today
to safely withdraw $100,000 every year for a 30-year retirement. Use the standard
Annuity formula. Build a custom Salesforce formula field that automatically
calculates this target number based on the client's stated retirement duration
and expected portfolio return rate.

**Inflation-Adjusted Lifestyle — Growing Annuity**
A flat $100,000 annual withdrawal loses purchasing power over 30 years. The client
needs withdrawals to grow by 3% per year to maintain lifestyle. Use the Growing
Annuity formula (g = 0.03). This significantly increases the present value required
today compared to the flat annuity calculation.

**Endowment Creation — Growing Perpetuity**
An ultra-high-net-worth client wants to establish a permanent charitable trust
paying a growing amount every year, forever. Use the Growing Perpetuity formula
to calculate the exact lump sum needed to seed the trust today.