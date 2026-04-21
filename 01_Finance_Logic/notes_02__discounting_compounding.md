# Wharton Finance: Compounding, Discounting, and the Timeline

## 1. Core Concept

Money has a "time unit" exactly like a physical currency. You cannot add a dollar from Year 1 to a dollar from Year 4 any more than you can add a Euro to a Yen. To aggregate money, you must convert it to a common base year using an "exchange rate for time" (the discount factor). **Discounting** pulls future cash flows backward to find their Present Value, while **Compounding** pushes current cash flows forward to find their Future Value.

## 2. Technical Variables

- **Cash Flow ($CF_t$):** The specific amount of money moving in or out during period $t$.
- **The Discount Factor:** $(1 + R)^t$. This is the mathematical "exchange rate" used to move money through time.
- **Time Period ($t$):** The exponent dictates the direction. A positive exponent (e.g., $t = 3$) moves money *forward* (compounding). A negative exponent (e.g., $t = -3$) moves money *backward* (discounting).
- **Present Value ($PV$):** The value of future cash flows converted into today's units (Period 0).
- **Future Value ($FV$):** The value of today's cash flows converted into a future period's units.

## 3. The Nimbus Application

For Tethered Wealth, this directly drives the dual-engine of expat financial planning: Goals and Growth.

- **The Discounting Engine (Funding Goals):** If an expat client wants to know exactly how much they must deposit *today* to fund a $100,000 European university tuition in 4 years, we use discounting. We pull that future liability back to Year 0.
- **The Compounding Engine (Wealth Projection):** If a client is saving $1,000 a month, we use compounding to project the Future Value of that portfolio at their retirement date. This proves the value of the advisory fee.

## 4. Architecture Decision

**The "Never Add Different Time Units" Rule:** In Salesforce, standard Roll-Up Summary fields blindly add numbers together. If we build a `Total_Portfolio_Value` field that just adds up cash flows from 2026, 2028, and 2030, the database is mathematically compromised.

**Solution:** The Salesforce `Client_Assets__c` object must use a custom Apex trigger or a Snowflake data pipeline to multiply future projected cash flows by their specific discount factor $(1 + R)^{-t}$ before summing them into a Net Present Value dashboard metric.