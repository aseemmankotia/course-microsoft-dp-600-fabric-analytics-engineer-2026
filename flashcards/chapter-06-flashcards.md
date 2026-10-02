## Chapter 6: Transforming Data with Notebooks and PySpark — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Default Spark session idle timeout for Starter pools in Fabric? | 20 minutes. Exam tip: configurable via an Environment item's Spark compute settings, not notebook properties. |
| 2 | Fabric custom Spark pool node sizes (vCores/RAM)? | Small 4/32GB, Medium 8/64GB, Large 16/128GB, X-Large 32/256GB, XX-Large 64/512GB. Exam tip: bigger nodes consume more Capacity Units per hour. |
| 3 | Minimum Fabric capacity SKU to use Copilot in notebooks? | F64 (or a Fabric trial capacity). Below F64, Copilot options are unavailable. |
| 4 | Read a Delta table from the default lakehouse without a full path? | spark.read.table("TableName"). Relative-name access only works when a lakehouse is attached as default. |
| 5 | Write a DataFrame as a managed Delta table to the default lakehouse? | df.write.format("delta").mode("overwrite").saveAsTable("TableName") |
| 6 | How does a notebook return a value to a pipeline Notebook activity? | notebookutils.notebook.exit(value) — surfaces as the activity's output.result.exitValue in the pipeline. |
| 7 | Magic command to run SQL in one cell against the attached lakehouse? | %%sql — runs Spark SQL for that cell only; rest of notebook stays PySpark. |
| 8 | notebookutils replaces which older Synapse-era library? | mssparkutils. notebookutils is Fabric-native, with fs, credentials, notebook, and session submodules. |
| 9 | Starter pool vs custom pool — when to choose custom? | Choose custom pools for shuffle-heavy/large jobs needing bigger node sizes or autoscale control; Starter pools are for quick, small, ad hoc sessions with fast startup. |
| 10 | How to pass parameters into a notebook from a pipeline Notebook activity? | Mark a cell as the 'parameters cell' (toggle via cell menu), then set matching variable names in the activity's Base parameters. |
| 11 | Can a notebook have more than one default lakehouse? | No — only one default lakehouse at a time. Additional lakehouses can be added as non-default and referenced via full path or explicit context switch. |
| 12 | What determines Spark Capacity Unit (CU) consumption for a notebook run? | Node size × number of nodes × session duration. Exam tip: an idle session still consumes CUs until the timeout releases it. |
