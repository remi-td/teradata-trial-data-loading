---
name: teradata-trial-data-loading
description: >
  Use this skill whenever a user wants to find, explore, or load demo/sample datasets
  into a Teradata Trial or ClearScape Analytics Experience environment. This skill is
  SPECIFIC to Teradata Trial / ClearScape Analytics Experience environments — do NOT
  trigger for generic Teradata environments, other databases, or non-Teradata systems.
  Trigger phrases include: "load demo data", "find a dataset", "hydrate the database",
  "what data is available", "get sample data", "load some data to explore",
  "what datasets can I use", "I have a Teradata Trial", "ClearScape Analytics",
  "ClearScape experience", or any time a user wants to populate a fresh Teradata Trial
  environment before running analytics, demos, or ML pipelines.
  Also triggers when a user asks about demo_user, get_data, or ClearScape/Trial demo datasets.
  Use a connected database MCP (any tool that can execute SQL against Teradata) to run queries.
---

# Teradata Demo Data Hydration

This skill guides the agent through discovering available demo datasets and loading them
into a Teradata Trial (formerly ClearScape Analytics Experience) environment using the
`demo_user.get_data()` stored procedure.

## Overview

**This skill is exclusively for Teradata Trial / ClearScape Analytics Experience environments.**
These are Teradata-hosted cloud trial environments available at
[https://www.teradata.com/getting-started/demos/clearscape-analytics](https://www.teradata.com/getting-started/demos/clearscape-analytics).
This hydration framework does NOT exist in standard Teradata on-prem installations,
customer-managed VantageCloud deployments, or any other database platform.

These environments ship with a `demo_user` database containing a `get_data` stored
procedure that hydrates datasets from Google Cloud Storage on demand. A registry of
all available datasets lives in `gs_tables_db.ddl`.

**Typical use case:** A user has a fresh Teradata Trial environment with a database MCP
connected (e.g. tdsql-dev, teradata-mcp, or any MCP that can execute SQL against Teradata)
and wants to load data before running analytics, demos, or ML pipelines.

**MCP compatibility:** This skill works with any MCP server that can execute SQL against
Teradata — the tool names may vary (execute_query, execute_statement, run_sql, query, etc.).
Use whatever SQL execution tool is available in the current session.

---

## Step 1: Verify This Is a Teradata Trial / ClearScape Environment

**This is a critical gate.** Before doing anything else, confirm two things:

**1a. Confirm the user is on a Teradata Trial / ClearScape Analytics Experience environment.**
If the user hasn't explicitly said so, ask:
> "Just to confirm — are you working in a Teradata Trial or ClearScape Analytics Experience
> environment? This data hydration process is specific to those environments and won't work
> on standard Teradata installations."

If the user says no or is unsure, **stop here** and explain that this skill only applies to
Teradata Trial / ClearScape Analytics Experience environments, available at
teradata.com/getting-started. Do not proceed with any SQL.

**1b. Verify the framework exists in the database:**

```sql
-- Check that demo_user and get_data exist
SELECT DatabaseName, TableName, TableKind
FROM DBC.TablesV
WHERE DatabaseName = 'demo_user' AND TableName = 'get_data';
```

- **If found:** proceed to Step 2.
- **If not found:** The environment may be a freshly provisioned Trial that hasn't fully
  initialized, or it may not be a Trial environment at all. Inform the user and suggest
  they verify their environment type at teradata.com/getting-started.

---

## Step 2: Discover Available Datasets and What's Already Loaded

Run both queries together so you can cross-reference what's available vs. what's already present:

```sql
-- All available datasets in the registry
SELECT DISTINCT databasename
FROM gs_tables_db.ddl
ORDER BY databasename;
```

```sql
-- Datasets already loaded in this environment
SELECT DatabaseName
FROM DBC.DatabasesV
WHERE DatabaseName LIKE 'DEMO_%'
ORDER BY DatabaseName;
```

Use the second result to build a "already loaded" set. When presenting options to the user
in Step 3, note which datasets are already available so they know they can use them immediately.

Each registry name ends in `_local` or `_cloud`:
- **`_local`** — copies data into local Teradata tables (faster queries, uses local perm space)
- **`_cloud`** — creates foreign tables pointing to GCS (no local storage used, slower queries)

Recommend `_local` unless the user has storage constraints or explicitly wants cloud access.

See `references/dataset-catalog.md` for the full categorized catalog to help users browse.

---

## Step 3: Guide the User to the Right Dataset

Ask the user what kind of data or use case they have in mind, then match to a category:

| Domain | Example Datasets |
|--------|-----------------|
| 🏥 Healthcare | HealthcareFWA, HeartFailure, CancerPrediction, DiabetesPrediction, HospitalReadmission |
| 🏦 Financial | BankChurn, CreditCard, CreditRisk, GLM_Fraud, Insurance |
| 🛍️ Retail | Retail, RetailJourney, Grocery_Data, CustomerReviews, MarketingCamp |
| 📡 Telco / IoT | Telco, TelcoNetwork, 5G, IndoorSensor, EVCarBattery |
| 🚕 Transportation | AustinBikeShare, NYCTaxi, TrainDelay, AirPassengers |
| 🤖 ML / AI | BankChurnIVSM, AnomalyDetection, ModelOps, NLP, SLM_RAG |
| 📊 Forecasting | SalesForecasting, DemandForecast, ProphetSTO, UAF |
| 🏭 Manufacturing | GreenManufacturing, PredictiveMaintenance, Secom |
| 🏀 General / Fun | BasketBall, TitanicSurvival, HousingPrices, Car, TPCH_1Gb |

When a user describes their use case, suggest 2-3 relevant datasets and briefly explain
what each contains before asking them to choose.

---

## Step 4: Load the Dataset (if not already present)

Before calling `get_data`, check whether the dataset is already loaded by looking for
its `_db` database. A dataset named `DEMO_AustinBikeShare_local` creates `DEMO_AustinBikeShare_db`:

```sql
SELECT DatabaseName
FROM DBC.DatabasesV
WHERE DatabaseName = 'DEMO_<DatasetName>_db';
```

- **If the database exists:** skip the load — inform the user the dataset is already available
  and proceed directly to Step 5 to show them the tables and schema.
- **If not found:** proceed with the load:

```sql
CALL demo_user.get_data('DEMO_AustinBikeShare_local');
```

**Important notes:**
- The procedure **requires exactly one argument** — calling with no args throws an error.
- A successful call returns `status: success, rowcount: 0` — this is normal.
- The procedure creates **two databases**: `DEMO_<name>` (views) and `DEMO_<name>_db` (raw tables).
- After loading, verify by listing the new databases:

```sql
SELECT DatabaseName, CommentString
FROM DBC.DatabasesV
WHERE DatabaseName LIKE 'DEMO_%'
ORDER BY DatabaseName;
```

---

## Step 5: Confirm What Was Loaded

After hydration, list the tables in the new database so the user can see what's available:

```sql
SELECT TableName, TableKind, CommentString
FROM DBC.TablesV
WHERE DatabaseName = 'DEMO_<DatasetName>_db'
  AND TableKind = 'T'
ORDER BY TableName;
```

Then describe the key tables so the user understands the schema and can get started.
Use `describe_table` (or `DBC.ColumnsV`) to show column details for the most important tables.

---

## Step 6: Suggest Next Steps

After confirming the load, suggest what the user can do next based on the dataset:

- **Run exploratory queries** — row counts, distributions, sample data
- **Join to weather/reference data** (e.g., AustinBikeShare includes Weather table)
- **Apply ML functions** — if the dataset is ML-oriented, point to Teradata analytic functions
- **Build a dashboard or report** — offer to create a visualization

---

## Multiple Datasets

Users can load multiple datasets. Each `CALL get_data(...)` is independent. To load
several at once, call the procedure once per dataset name. There is no batch-load option.

---

## Removing a Dataset

To clean up a loaded dataset:
```sql
CALL demo_user.remove_data('DEMO_AustinBikeShare_local');
```

This drops the databases created by the corresponding `get_data` call.

---

## MCP Tool Compatibility

This skill works with any MCP that can execute SQL against Teradata. Common tool names to look for:
- `execute_query` / `execute_statement` (tdsql-dev, teradata-ce)
- `run_sql` / `query` (other Teradata MCP variants)
- Any tool whose description mentions Teradata SQL execution

Use `list_databases` or equivalent if available to confirm connectivity before running DDL checks.

---

## Reference Files

- `references/dataset-catalog.md` — Full categorized list of all ~180 available datasets
  with brief descriptions. Read this when the user wants to browse all options or needs
  help finding a dataset for a specific use case.
