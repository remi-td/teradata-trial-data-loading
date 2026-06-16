# Teradata Demo Data Discovery & Hydration Prompt

**Prompt name:** `load-demo-data`
**Use this prompt** by pasting it into your conversation with Claude when you have a
**Teradata Trial or ClearScape Analytics Experience** environment with a database MCP
connected, and want to find and load a demo dataset.

> ⚠️ **Environment note:** This process is exclusive to Teradata Trial / ClearScape Analytics
> Experience environments. It will not work on standard Teradata installations, customer-managed
> VantageCloud deployments, or other database platforms. Get a free trial at
> [teradata.com/getting-started](https://www.teradata.com/getting-started).

---

## The Prompt

```
I have a Teradata Trial (ClearScape Analytics Experience) environment connected via a
database MCP and I'd like to find and load a demo dataset to work with.

Please help me:
1. First verify this is a Teradata Trial environment and that the demo data framework
   is available (check for demo_user.get_data)
2. Query the dataset registry in gs_tables_db.ddl to see what's available
3. Ask me what kind of use case or domain I'm interested in (e.g. healthcare, retail,
   financial, ML/AI, transportation, etc.)
4. Based on my answer, suggest 2-3 relevant datasets and briefly describe what each contains
5. Once I choose, load it using: CALL demo_user.get_data('<dataset_name>_local');
6. After loading, show me what tables were created and describe the key ones
7. Suggest some initial queries or analyses I could run to get started

Let's begin!
```

---

## Alternative: Domain-Specific Variants

If you already know what domain you want, use one of these targeted variants:

### Healthcare / Life Sciences
```
I have a Teradata Trial (ClearScape Analytics Experience) environment connected via a
database MCP. Please verify the demo data framework is available (demo_user.get_data),
then help me find and load a healthcare or life sciences demo dataset. I'm interested in
[patient outcomes / fraud detection / clinical prediction / survival analysis — pick one].
Suggest the most relevant option, load it, and walk me through the schema.
```

### Financial Services
```
I have a Teradata Trial (ClearScape Analytics Experience) environment connected via a
database MCP. Please check for demo_user.get_data, then find and load a financial services
demo dataset suitable for [churn prediction / fraud detection / credit risk / general banking
analytics — pick one]. Load it locally and show me what's available.
```

### ML / AI Pipeline
```
I have a Teradata Trial (ClearScape Analytics Experience) environment connected via a
database MCP. I want to run a machine learning demo end-to-end. Check for demo_user.get_data,
then find a dataset appropriate for [classification / anomaly detection / NLP / time series
forecasting / RAG — pick one]. Load it and describe the features so I can start building a model.
```

### Retail / Marketing
```
I have a Teradata Trial (ClearScape Analytics Experience) environment connected via a
database MCP. Help me load a retail or marketing demo dataset. Check for demo_user.get_data,
suggest options for [customer churn / recommendation / journey analytics / campaign analysis
— pick one], load the best match, and show me the schema.
```

---

## Tips for Users

- **`_local` vs `_cloud`:** Always prefer `_local` — data is copied into Teradata for
  fast query performance. Use `_cloud` only if you want to avoid consuming storage space.

- **Any database MCP works:** The skill works with any MCP that can execute SQL against
  Teradata — tdsql-dev, teradata-ce, or any other Teradata-connected MCP tool.

- **Multiple datasets:** You can load more than one. Just ask Claude to run
  `get_data` again with a different dataset name.

- **Cleanup:** To remove a dataset later, ask Claude to run:
  `CALL demo_user.remove_data('<dataset_name>_local');`

- **Only for Teradata Trial / ClearScape:** This framework is pre-installed on
  Teradata Trial environments. It is not available on standard or customer-managed
  Teradata deployments. Get a trial at teradata.com/getting-started.

---

## What Happens Under the Hood

When Claude runs `CALL demo_user.get_data('DEMO_XYZ_local')`:

1. The procedure reads DDL scripts from `gs_tables_db.ddl` for the requested dataset
2. It creates two databases: `DEMO_XYZ` (views) and `DEMO_XYZ_db` (base tables)
3. Data is loaded from Google Cloud Storage (`clearscape_analytics_demo_data` bucket)
4. You're ready to query — usually completes in seconds to a few minutes depending on size
