[![](https://img.shields.io/nuget/v/soenneker.clamav.definitions.svg?style=for-the-badge)](https://www.nuget.org/packages/soenneker.clamav.definitions/)

# Soenneker.Clamav.Definitions

A current, platform-neutral ClamAV virus-definition seed for ephemeral and offline .NET workloads.

## Installation

```bash
dotnet add package Soenneker.Clamav.Definitions
```

The package copies the official `main`, `daily`, and `bytecode` databases beneath the application output directory:

```text
Resources/clamav-database/
```

`Soenneker.Clamav.Util` discovers this location by default. For an ephemeral container, call `UpdateDefinitions()` during startup so `freshclam` can apply the smaller incremental updates published after this package was built:

```csharp
string databaseDirectory = Path.Combine(AppContext.BaseDirectory, "Resources", "clamav-database");
await clamav.UpdateDefinitions(databaseDirectory, cancellationToken);
```

The package is maintained automatically from the official [ClamAV database service](https://database.clamav.net/) and is published only when the packaged database content changes.

## Licensing

The package scaffolding is MIT-licensed. The packaged ClamAV database payload retains its upstream terms and provenance; see `COPYING.txt` and `SOURCE.txt` beside the database files.
