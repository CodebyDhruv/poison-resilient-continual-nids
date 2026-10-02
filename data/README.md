# Data directory

Do not commit source datasets or derived feature files.

Expected local layout:

```text
data/
  raw/        Downloaded source files (ignored)
  interim/    Temporary cleaned files (ignored)
  processed/  Model-ready datasets (ignored)
  metadata/   Small, versioned schemas and dataset cards
```

For every dataset, record its source URL, download date, license, checksum if available, feature schema, label mapping, and preprocessing version in `data/metadata/`.
