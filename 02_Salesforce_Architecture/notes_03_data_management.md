# Salesforce: Data Management (Import & Export)

## 1. Data Import Architecture

Two primary mechanisms for ingesting CSV data. Choice depends on volume,
automation requirements, and target objects.

**Data Import Wizard**
- Native in-browser tool accessed via Setup
- Capacity: up to 50,000 records per import
- Supported objects: standard objects (Accounts, Contacts, Leads, Solutions,
  Campaign Members) and all custom objects
- Best use case: ad-hoc, manual imports of clean data with no complex automation

**Data Loader**
- Standalone client application — interacts directly with Salesforce API (SOAP or Bulk API)
- Capacity: up to 150 million records
- Supported objects: all standard and custom objects
- Best use case: massive data migrations, automated nightly syncs via command line,
  complex or unsupported objects

## 2. Pre-Flight Data Preparation & Mapping Rules

Importing uncleaned data corrupts the database. Required steps before any import:

- **Data Cleansing:** Remove duplicates, enforce naming conventions, correct typos in source CSV
- **System Preparation:** Add new picklist values, build necessary custom fields before import
- **Validation Rules:** Active validation rules run during import — records that fail are rejected.
  Standard practice is to temporarily deactivate highly restrictive rules during bulk loads.

**Data Type Formatting Requirements**
- `Checkboxes` — must be `1` (True) or `0` (False)
- `Multi-Select Picklists` — values separated by semicolon (`;`)
- `Restricted Picklists` — CSV values not present in the picklist will cause that record to fail
- `Formula Fields` — cannot be mapped or imported; read-only, system-calculated

## 3. Data Export Architecture

**Data Export Service**
- Native in-browser tool via Setup
- Can be run manually or scheduled weekly/monthly depending on Salesforce Edition
- Output: ZIP archive of CSVs — optionally includes images, documents, attachments
- Download link expires 48 hours after generation

**Data Loader**
- Used for exports requiring external system integration
- Supports automated, command-line driven data extraction

## 4. Tethered Wealth Applications

**Import Wizard for Client Onboarding**
New partnership acquires 400 HNW leads under 50,000 records — clean CSV in Excel,
use Data Import Wizard to load into `Lead` object. Map "Net Worth" column to
custom `Estimated_Asset_Value__c` field manually.

**Data Loader for Transactional Volume**
Trade log integration for offshore accounts (potentially hundreds of thousands of
rows/month) exceeds Import Wizard capacity. Data Loader + Bulk API configured to
ingest into custom `Trade_Log__c` object.

**Pre-Flight Cleansing — The Checkbox Rule**
Source spreadsheet uses "Yes"/"No" for FATCA reporting field. Must use Excel
Find and Replace to convert to `1`/`0` before import — otherwise Salesforce
rejects all checkbox-mapped records.

**Automated Backups for SEC/FINRA Compliance**
Data Export Service scheduled every Friday night — "Include all data" with
attachments (PDF tax returns). ZIP downloaded before 48-hour expiration and
stored on encrypted offline drive to satisfy data retention regulations.