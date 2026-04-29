# Excel Essentials: Data Management

## 1. Core Concept

Data management covers structural control, manipulation, and exception
handling within large datasets. These tools form the first line of defense
against dirty data before it enters any downstream system.

## 2. Data Management Tools

**Managing Rows and Columns**
Insert, Delete, and Hide operations should be executed via the column and
row headers (the lettered and numbered interface borders) to ensure the
action applies uniformly across the entire dataset rather than a single cell.

**Find and Replace**
Used for bulk data correction. Advanced functionality includes searching
by specific formatting — for example, finding the number 18 only when
formatted as General Text, ignoring currency values like $18.00.

**Filtering**
Temporarily hides rows that do not meet specific criteria. Relies on
native arguments (e.g., "Tomorrow", "Does not equal"). Complex queries
such as filtering for weekdays only require helper columns using functions
like WEEKDAY().

**Sorting**
Reorders data chronologically, alphabetically, or numerically. Used to
establish rank (e.g., top-performing accounts) or group similar categories
for bulk review.

**Conditional Formatting**
Applies dynamic visual indicators based on Boolean logic rules — if a
cell value exceeds a threshold, apply a color fill automatically.
Transitions a static sheet into an automated alerting system. Rule scope
must be applied to the correct data range, not just a single cell.

**Keyboard Shortcuts**
ALT key sequences navigate the ribbon without a mouse. Reduces navigational
friction in high-volume data environments.

## 3. Tethered Wealth Applications

**Compliance Auditing**
Filter large client lists to isolate accounts missing required compliance
documentation. Conditional formatting flags accounts whose asset allocations
have drifted outside target risk parameters — prompting immediate advisor
intervention without manual review of every row.

**SaaS RevOps Applications**
Find and Replace corrects dirty CRM data exported from Salesforce before
it enters reporting. Sorting and filtering segment thousands of leads by
territory or industry. Conditional formatting serves as an automated
pipeline monitor — highlighting deals where Days in Stage exceeds the
standard sales cycle, or flagging contract renewals approaching within
30 days.