---
title: "Command Line"
linkTitle: "Command Line"
weight: 10
---

{{% pageinfo %}}
More documentation for the CLI app will be coming in the future, including getting started guides.
{{% /pageinfo %}}

In addition to the "mainline" API, this project includes a simple command-line to perform local-only basic operations. The CLI must have its index populated before use, but is then able to run completely offline and provides basic ship listing functionality.

Since it uses the excellent `Spectre.Cli`, you can always check the usage by running with `--help`.

```bash
azurite --help
azurite list -h
azurite index --help
azurite list by-name --help
```

---

The CLI also supports "passthrough" so that requests will still work if you haven't built an index (by directly polling the upstream source), but with warnings displayed.