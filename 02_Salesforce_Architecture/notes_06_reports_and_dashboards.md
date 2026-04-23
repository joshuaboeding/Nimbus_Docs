# Reports & Dashboards for Lightning Experience

## 1. Core Architecture
- **Reports:** A structured list of records meeting defined criteria. Allows filtering, grouping, and basic mathematical operations. Reports are the underlying data queries of the CRM.
- **Report Types:** The foundational template. Dictates which objects and fields are available to query.
  - **Standard:** Pre-built by Salesforce (e.g., Accounts, Leads).
  - **Custom:** User-defined relationships (e.g., Leads WITH Activities). Essential for reporting on customized data models and related objects.
- **Dashboards:** A visual interface compiling multiple report metrics into a single layout. Built using widgets.
- **Folders:** The security and access layer. Reports and Dashboards inherit visibility from their enclosing folders. Can be Public, Hidden, or Shared based on Roles, Permissions, or Public Groups.

## 2. The Report Builder Interface
- **Outline Tab:** Controls the structural display. Used to group data by rows or columns and toggle detail rows.
- **Filters Tab:** Controls the data logic. Dictates exactly which records are allowed into the report.
- **Fields Panel:** The data dictionary. Displays all fields available based on the chosen Report Type.

## 3. Advanced Filtering Logic
- **Standard Filters:** Default object filters included automatically (e.g., Show Me, Created Date).
- **Field Filters:** Specific criteria placed on individual fields (e.g., Amount greater than 100000).
- **Cross Filters:** Relational filtering without writing code. Uses WITH or WITHOUT logic between parent and child objects.
  - *Example:* Accounts WITH Opportunities.
  - *Sub-filters:* Allows further refinement on the child object (e.g., Accounts WITH Opportunities where Stage equals Prospecting).
- **Filter Logic:** Boolean logic applied to field filters using AND, OR, NOT operators. Example: (1 OR 2) AND 3.
- **Locked Filters:** Security feature that prevents end-users from altering specific filter criteria at runtime, preserving the integrity of the data view.

## 4. Report Formats
- **Tabular:** A raw list. An ordered set of columns. Used for data exports, auditing, and dashboard data tables (requires a row limit).
- **Summary:** Grouped by rows. Allows subtotals and charts. The standard format for operational analysis and dashboard charts.
- **Matrix:** Grouped by both rows and columns. Provides high-level aggregated overviews. Ideal for financial trends and dense data comparisons.

## 5. Data Visualization (Dashboards)
- **Widgets:** The visual components (Chart, Gauge, Metric, Table). Each widget requires a single source report. Note: Joined and Historical Trend reports cannot be used as sources.
- **The Running User:** The security setting dictating which data populates the dashboard widgets.
  - **Static Dashboard:** Set to a specific user. All viewers see exactly what that specific user has access to see, overriding their own personal permissions.
  - **Dynamic Dashboard:** Set to "The dashboard viewer." The dashboard automatically filters data based on the logged-in user's security permissions. Highly scalable for large teams.
- **Report Charts:** A lightweight visualization option allowing a single chart to be embedded directly at the top of a report view.

## 6. Application: Tethered Wealth Context
- **Custom Report Types:** Essential for the Expat data model. A custom report type for "Households WITH Foreign Bank Accounts" will be necessary to track offshore capital effectively.
- **Cross Filter Implementation:** Building exception and diagnostic reports. For example, creating a report for "Households WITHOUT Active Tax Strategy" to identify compliance gaps before year-end tax deadlines.
- **Matrix Reporting:** Tracking firm-wide Assets Under Management (AUM). Group rows by "Country of Residence" and columns by "Asset Class" (Equities, Fixed Income, Real Estate) to visualize exactly where client capital is concentrated globally.
- **Dynamic Dashboards for Scalability:** Building a single "Advisor Productivity Dashboard." When a junior advisor logs in, they see only their own client pipeline and tasks. When the managing partner logs in to the exact same dashboard, they see the aggregate pipeline for the entire firm. This eliminates the need to build and maintain separate dashboards for every employee.