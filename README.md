# tszig-stdlib

Standard library mappings for TSZig - TypeScript module APIs mapped to Zig equivalents.

## Overview

`tszig-stdlib` provides implementations of common TypeScript/Node.js standard library modules using native Zig code. This enables TSZig users to write familiar TypeScript-style code that transpiles to efficient Zig.

## Modules

| Module | Description | Status |
|--------|-------------|--------|
| `fs` | File system operations | 🔶 In Progress |
| `path` | Path manipulation | ⏳ Planned |
| `json` | JSON parsing/stringify | ⏳ Planned |
| `math` | Math functions | ⏳ Planned |
| `date` | Date/time utilities | ⏳ Planned |
| `buffer` | Buffer operations | ⏳ Planned |
| `crypto` | Cryptographic utilities | ⏳ Future |

## Installation

### As a Zig Dependency

```zon
.{
    .dependencies = .{
        .tszig_stdlib = .{
            .url = "https://github.com/TSZig/tszig-stdlib/archive/refs/tags/v0.1.0.tar.gz",
            .hash = "...",
        },
    },
}
```

## Usage

### File System (fs)

```typescript
// TypeScript input
import * as fs from "fs";

const content = fs.readFileSync("data.txt", "utf8");
fs.writeFileSync("output.txt", content);
```

```zig
// Generated Zig
const fs = @import("tszig-stdlib").fs;

const content = try fs.readFileSync("data.txt", .utf8);
try fs.writeFileSync("output.txt", content);
```

### Path Operations

```typescript
// TypeScript input
import * as path from "path";

const fullPath = path.join("dir", "subdir", "file.txt");
const ext = path.extname(fullPath);
```

```zig
// Generated Zig
const path = @import("tszig-stdlib").path;

const fullPath = path.join(&.{"dir", "subdir", "file.txt"});
const ext = path.extname(fullPath);
```

## API Reference

### fs Module

```zig
/// Read file contents as string
pub fn readFileSync(path: []const u8, encoding: Encoding) ![]const u8

/// Write string to file
pub fn writeFileSync(path: []const u8, data: []const u8) !void

/// Open file for reading/writing
pub fn openSync(path: []const u8, flags: OpenFlags) !File

/// Check if path exists
pub fn existsSync(path: []const u8) bool

/// Get file statistics
pub fn statSync(path: []const u8) !Stats
```

### path Module

```zig
/// Join path segments
pub fn join(segments: []const []const u8) []const u8

/// Get file extension
pub fn extname(path: []const u8) []const u8

/// Get directory name
pub fn dirname(path: []const u8) []const u8

/// Get base name
pub fn basename(path: []const u8) []const u8
```

## TypeScript to Zig Mapping

| TypeScript | Zig Equivalent |
|------------|----------------|
| `fs.readFileSync(path, 'utf8')` | `std.fs.cwd().readFile(path, ...)` |
| `fs.writeFileSync(path, data)` | `std.fs.cwd().writeFile(path, data)` |
| `fs.existsSync(path)` | `std.fs.cwd().access(path, ...)` |
| `path.join(a, b)` | `std.fs.path.join(...)` |
| `JSON.parse(str)` | `std.json.parseFromSlice(...)` |
| `JSON.stringify(obj)` | `std.json.stringifyAlloc(...)` |

## License

MIT License - see [LICENSE](LICENSE) for details.

## Contributing

See [CONTRIBUTING.md](https://github.com/TSZig/.github/blob/main/CONTRIBUTING.md) for guidelines.
