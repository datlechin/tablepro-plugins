# TablePro Plugin Registry

This repository hosts the plugin registry for [TablePro](https://github.com/datlechin/TablePro). The `plugins.json` manifest is fetched by the app's Browse tab in Settings > Plugins.

## Registry Format

`plugins.json` contains a flat array of available plugins:

```json
{
  "schemaVersion": 1,
  "plugins": [
    {
      "id": "com.example.cassandra-driver",
      "name": "Cassandra Driver",
      "version": "1.0.0",
      "summary": "Apache Cassandra database support for TablePro",
      "author": {
        "name": "Example Corp",
        "url": "https://github.com/example"
      },
      "homepage": "https://github.com/example/tablepro-cassandra",
      "category": "database-driver",
      "downloadURL": "https://github.com/example/tablepro-cassandra/releases/download/v1.0.0/CassandraDriver.zip",
      "sha256": "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855",
      "minAppVersion": "0.16.0",
      "minPluginKitVersion": 1,
      "iconName": "cylinder.fill",
      "isVerified": false
    }
  ]
}
```

## Fields

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `id` | string | yes | Bundle identifier (must match the `.tableplugin` bundle ID) |
| `name` | string | yes | Display name |
| `version` | string | yes | Semantic version |
| `summary` | string | yes | One-line description |
| `author` | object | yes | `name` (required) and `url` (optional) |
| `homepage` | string | no | Project URL |
| `category` | string | yes | One of: `database-driver`, `export-format`, `import-format`, `theme`, `other` |
| `downloadURL` | string | yes | Direct link to the `.zip` archive containing the `.tableplugin` bundle |
| `sha256` | string | yes | SHA-256 hex checksum of the zip file |
| `minAppVersion` | string | no | Minimum TablePro version required |
| `minPluginKitVersion` | int | no | Minimum TableProPluginKit version required |
| `iconName` | string | no | SF Symbol name (defaults to `puzzlepiece`) |
| `isVerified` | bool | yes | `true` if reviewed and signed by the TablePro team |

## Submitting a Plugin

1. Build your `.tableplugin` bundle following the [developer guide](https://github.com/datlechin/TablePro/blob/main/docs/development/plugin-system/developer-guide.md)
2. Code-sign it with a valid Apple Developer certificate
3. Create a `.zip` archive containing the bundle
4. Compute the SHA-256 checksum: `shasum -a 256 YourPlugin.zip`
5. Host the zip on GitHub Releases (or any direct-download URL)
6. Open a PR adding your plugin entry to `plugins.json`

## Verified Plugins

Plugins with `"isVerified": true` have been reviewed and signed by the TablePro team. Only the TablePro maintainers can set this flag.
