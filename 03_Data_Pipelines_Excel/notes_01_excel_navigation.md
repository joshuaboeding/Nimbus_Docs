# Excel Essentials: Navigation, Data Entry, and the Fill Handle

## 1. The User Interface & Navigation

Excel's interface is designed for high-density data management. Navigating
efficiently without touching the mouse is the first step to becoming a power user.

**Core Terminology**

- **The Ribbon** — main toolbar at the top (Home, Insert, Data, etc.). Logically
  grouped by function. Double-click a tab to collapse it and save screen space.
- **The Formula Bar** — space above the columns showing the true content of a
  cell, not just the displayed result. Edit cell content here.
- **The Status Bar** — grey bar at the bottom. Automatically calculates Average,
  Count, and Sum of any highlighted numeric data.
- **Quick Access Toolbar** — small row of icons above the Ribbon. Right-click any
  Ribbon tool to add it here for one-click access.

**Navigation Shortcuts**

- `Ctrl + Home` — instantly jumps to cell A1
- `Ctrl + Arrow Keys` — jumps to the edge of the current data block
- `Ctrl + A` — selects all contiguous data surrounding the active cell
- `Ctrl + F6` — toggles between different open Excel workbooks

## 2. Viewing Data Effectively

When working with large datasets, the standard view becomes unreadable.

**Freeze Panes**
Keeps headers visible while scrolling. Click the cell that is exactly below the
row you want to freeze AND exactly to the right of the column you want to freeze
before clicking Freeze Panes.

**Split Screen**
Divides the window into four quadrants — view the top and bottom of a spreadsheet
simultaneously.

## 3. Data Entry & Modification

Entering data correctly prevents formula errors downstream.

**Enter vs. Tab Flow**
- `Tab` — commits data and moves Right
- `Enter` — commits data and moves Down

**Editing a Cell**
- `Delete` — removes cell contents only
- `F2` (or double-click) — opens the cell for editing
- `Escape` — cancels an edit in progress without needing Undo

**Copy/Paste Nuance**
- Standard Paste brings formatting with it
- Paste Values — strips formatting, keeps raw data only
- Keep Source Column Widths — preserves original column sizing
- Transpose — flips data 90 degrees, turning rows into columns or columns into rows

## 4. The Fill Handle

The small square at the bottom right of the active cell. The most powerful basic
tool in Excel for pattern recognition and data population.

- **Copying** — dragging a simple number down copies it to each cell
- **Series Creation** — dragging a date or numbered text (e.g., R1001) creates
  a sequential series automatically (Monday, Tuesday, Wednesday etc.)
- **Double-Click Trick** — instead of dragging down 1,000 rows, double-click
  the fill handle and it auto-fills the column to the end of adjacent data
- **Flash Fill** — type a pattern manually once (e.g., John.Smith@company.com
  next to First Name and Last Name columns) and Flash Fill deduces the pattern
  and completes the entire list

## 5. Tethered Wealth Applications

**Transpose for Client Questionnaires**
Google Forms exports questionnaire data horizontally — questions as columns,
answers as rows. Salesforce field mapping often requires vertical orientation.
Copy the row, open a new sheet, use Paste > Transpose to flip the data instantly
before importing via the Data Import Wizard.

**Flash Fill for Household Names**
Legacy spreadsheet contains raw client names ("Jane Miller", "Bob Smith").
Salesforce requires a formatted Account Name for each household. Create a new
column, type "The Miller Household" next to Jane Miller, double-click the Fill
Handle, select Flash Fill — Excel writes "The Smith Household" and every
subsequent entry automatically, eliminating manual typing before the Salesforce
upload.