# angelus_wys_v2

<div align="center">

[![Rust](https://img.shields.io/badge/rust-1.70%2B-orange.svg)](https://www.rust-lang.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![GitHub Actions](https://github.com/seu-usuario/AngelusWys/workflows/CI/badge.svg)](https://github.com/seu-usuario/AngelusWys/actions)
![Status](https://img.shields.io/badge/status-MVP-blue.svg)

A lightweight, human-friendly text editor inspired by **GNU Nano**, written entirely in **Rust** for performance and safety.

[Features](#features) • [Quick Start](#quick-start) • [Development](#development) • [Roadmap](#roadmap)

</div>

---

## Overview

**AngelusWys** is a minimalist terminal text editor designed for DevOps workflows, scripting, and quick edits. It combines the simplicity of GNU Nano with the performance and memory safety of Rust.

### Why nano-rust?

- **Lightweight**: No bloat, no unnecessary dependencies
- **Memory safe**: Written in Rust, eliminating entire classes of bugs
- **Cross-platform**: Runs on Linux, macOS, and Windows
- **Fast**: Compiled binary with instant startup time
- **Familiar**: Nano-inspired keybindings and UX

---

## Features

### Current (MVP)
- ✅ Create and edit files
- ✅ Save files with `Ctrl+S`
- ✅ Exit cleanly with `Ctrl+Q` or `:q`
- ✅ Display line numbers (optional)
- ✅ Syntax highlighting ready (framework in place)
- ✅ CI/CD pipeline with GitHub Actions

### Planned (Next phases)
- 📋 Text selection (`Ctrl+Shift+Arrows`)
- 📋 Copy/cut/paste (`Ctrl+C`, `Ctrl+X`, `Ctrl+V`)
- 📋 Undo/Redo (`Ctrl+Z`, `Ctrl+Y`)
- 📋 Search and replace (`Ctrl+F`)
- 📋 Multiple buffers
- 📋 Configuration files
- 📋 Syntax highlighting for common formats (Rust, Python, Shell)
- 📋 Plugin system

---

## Quick Start

### Prerequisites

- Rust 1.70 or later ([Install Rust](https://rustup.rs/))
- Cargo (comes with Rust)

### Installation

#### From source
```bash
git clone https://github.com/FernandoSaraiva0/angelus_wys_v2
cd AngelusWysV2
cargo install --path .
```

#### Build locally
```bash
git clone https://github.com/FernandoSaraiva0/angelus_wys_v2
cd AngelusWysV2
cargo build --release
./target/release/angelus
```

### Usage

```bash
# Create a new file
angelus

# Edit an existing file
angelus myfile.txt

# Get help
angelus --help
```

### Keybindings

| Shortcut | Action |
|----------|--------|
| `Ctrl+S` | Save file |
| `Ctrl+Q` | Quit editor |
| `:q` | Quit editor (vim-style) |
| `Arrow keys` | Navigate cursor |
| `Ctrl+C` | Copy (coming soon) |
| `Ctrl+X` | Cut (coming soon) |
| `Ctrl+V` | Paste (coming soon) |
| `Ctrl+Z` | Undo (coming soon) |
| `Ctrl+F` | Find (coming soon) |

---

## Development

### Project Structure

```
AngelusWysV2/
├── src/
│   ├── main.rs        # Entry point, CLI argument parsing
│   ├── editor.rs      # Main editor loop and state management
│   ├── buffer.rs      # Text buffer and file operations
│   ├── input.rs       # Keyboard input handling
│   ├── display.rs     # Terminal rendering
│   └── lib.rs         # Library exports
├── tests/
│   └── integration_tests.rs  # Integration tests
├── Cargo.toml         # Project manifest and dependencies
├── Cargo.lock         # Locked dependency versions
├── .github/
│   └── workflows/
│       └── ci.yml     # CI/CD pipeline configuration
├── README.md          # This file
└── LICENSE            # MIT License
```

### Building from source

```bash
# Build debug version (fast compilation, slower runtime)
cargo build

# Build release version (slow compilation, optimized runtime)
cargo build --release

# Run directly
cargo run -- myfile.txt
```

### Testing

```bash
# Run all tests
cargo test

# Run tests with output
cargo test -- --nocapture

# Run specific test
cargo test test_create_new_buffer
```

### Code Quality

```bash
# Format code (Rust standard)
cargo fmt

# Check formatting
cargo fmt -- --check

# Lint with clippy
cargo clippy -- -D warnings

# Generate and open documentation
cargo doc --open
```

### CI/CD Pipeline

This project uses **GitHub Actions** for continuous integration. Every push runs:
- ✅ Compilation check (`cargo build`)
- ✅ Unit and integration tests (`cargo test`)
- ✅ Linting with Clippy (`cargo clippy`)
- ✅ Code formatting check (`cargo fmt`)
- ✅ Documentation generation (`cargo doc`)

See [`.github/workflows/ci.yml`](.github/workflows/ci.yml) for details.

---

## Architecture

### Core Components

#### `buffer.rs` - Text Buffer
Manages in-memory representation of file content as a vector of lines.

```rust
pub struct Buffer {
    lines: Vec<String>,
}

impl Buffer {
    pub fn new() -> Self { ... }
    pub fn from_file(path: &Path) -> Result<Self> { ... }
    pub fn save_to_file(&self, path: &Path) -> Result<()> { ... }
}
```

#### `editor.rs` - Main Loop
Orchestrates the editor lifecycle: initialization, input/render loop, cleanup.

```rust
pub struct Editor {
    buffer: Buffer,
    file_path: Option<PathBuf>,
    cursor: Position,
}

impl Editor {
    pub fn run(&mut self) -> Result<()> { ... }
}
```

#### `input.rs` - Input Handler
Captures and interprets keyboard events using crossterm.

```rust
pub enum Command {
    Quit,
    Save,
    Move(Direction),
    // ... more commands
}

pub fn handle_key(event: KeyEvent) -> Command { ... }
```

#### `display.rs` - Renderer
Renders buffer content to terminal with line numbers and status bar.

```rust
pub struct Display {
    width: u16,
    height: u16,
}

impl Display {
    pub fn render_file(&self, lines: &[String]) -> Result<()> { ... }
}
```

### Dependency Graph

```
main.rs
    ├── editor.rs (orchestrator)
    │   ├── buffer.rs (data)
    │   ├── input.rs (keyboard events)
    │   └── display.rs (rendering)
    └── CLI args (clap)
```

---

## Dependencies

| Crate | Version | Purpose |
|-------|---------|---------|
| `crossterm` | 0.27 | Terminal control (input, colors, cursor) |
| `anyhow` | 1.0 | Error handling |
| `clap` | 4.4 | CLI argument parsing |
| `assert_cmd` | 2.0 | Integration testing (dev-only) |
| `predicates` | 3.0 | Test assertions (dev-only) |

All dependencies are carefully selected for:
- **Small footprint**: Minimal compilation time
- **Stability**: Mature crates with good track records
- **Active maintenance**: Regular updates and security patches

---

## Contributing

Contributions are welcome! Please follow these guidelines:

### Getting started

1. Fork the repository
2. Create a feature branch: `git checkout -b feat/your-feature`
3. Make changes and write tests
4. Run checks: `cargo fmt`, `cargo clippy`, `cargo test`
5. Commit with clear message: `git commit -m "feat: add your feature"`
6. Push and open a Pull Request

### Commit Message Format

We follow conventional commits:

```
type(scope): description

[optional body]
[optional footer]
```

Examples:
- `feat(input): add copy/paste support`
- `fix(buffer): prevent line overflow on insert`
- `docs(readme): update installation instructions`
- `refactor(display): simplify render logic`
- `test(editor): add cursor movement tests`

### Code Style

- Format with `cargo fmt` (automatic)
- No clippy warnings (run `cargo clippy`)
- Tests for new features
- Documentation comments for public APIs

---

## Roadmap

### Phase 1: MVP (Current)
- [x] Basic file operations (create, open, save)
- [x] Terminal rendering
- [x] Keyboard input handling
- [x] CI/CD pipeline
- [ ] Clean shutdown and error handling

### Phase 2: Core Editing
- [ ] Insert/delete characters
- [ ] Text selection
- [ ] Copy/cut/paste
- [ ] Undo/Redo with history stack
- [ ] Line numbers toggle

### Phase 3: Advanced Features
- [ ] Search and replace
- [ ] Syntax highlighting
- [ ] Multiple files (tabs/buffers)
- [ ] Configuration file support
- [ ] Macro recording

### Phase 4: Polish & Distribution
- [ ] Snap/Brew package
- [ ] Man page
- [ ] Plugin system
- [ ] Performance optimizations
- [ ] Comprehensive documentation

---

## Performance

nano-rust is designed to be fast and memory-efficient:

- **Startup time**: ~5ms (compiled binary)
- **Memory usage**: ~2MB baseline
- **File size support**: Up to system RAM limits

Benchmarks are run on each release. See [benchmarks/](./benchmarks/) for details.

---

## Troubleshooting

### Terminal appears corrupted after exit
Your terminal may not have cleaned up properly. Run:
```bash
reset
```

### Cursor position lost
This is a known edge case. Please file an issue with:
```bash
nano --debug-log debug.log myfile.txt
```

### Can't compile on macOS
Ensure you have the latest Xcode command-line tools:
```bash
xcode-select --install
```

---

## FAQ

**Q: How is this different from Nano or Vi?**  
A: nano-rust combines Nano's simplicity with Rust's performance and safety. It's written from scratch, not a port.

**Q: Will this support plugins?**  
A: Yes, plugin system is planned for Phase 3.

**Q: Can I use this for large files (>100MB)?**  
A: Not yet. Current implementation loads entire file into memory. Streaming support is planned.

**Q: How stable is this?**  
A: MVP is feature-complete but not production-ready. Expect breaking changes until v1.0.

**Q: Can I contribute?**  
A: Absolutely! See [Contributing](#contributing) section.

---

## License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

MIT License allows:
- ✅ Commercial use
- ✅ Modification
- ✅ Distribution
- ✅ Private use

With one condition:
- 📌 Include license and copyright notice

---

## Acknowledgments

This project is inspired by:
- [GNU Nano](https://www.nano-editor.org/) - The original, simple text editor
- [Vim](https://www.vim.org/) - Keyboard-driven philosophy
- [Helix](https://helix-editor.com/) - Modern approach to terminal editors

Special thanks to the Rust community for the excellent tooling and libraries.

---

## Author

**Fernando Saraiva**
- GitHub: [@seu-usuario](https://github.com/FernandoSaraiva0)
- LinkedIn: [fernando-saraiva](https://linkedin.com/in/fernandosaraiva-devops)
- Technical Lead | Systems & DevOps | Rust Enthusiast

---

## Support

- 🐛 **Found a bug?** Open an [Issue](https://github.com/FernandoSaraiva0/angelus_wys_v2/issues)
- 💡 **Have an idea?** Start a [Discussion](https://github.com/FernandoSaraiva0/angelus_wys_v2/discussions)
- ⭐ **Like the project?** Leave a star!

---

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for release notes and version history.

---

<div align="center">

Made with ❤️ in Rust | Built for DevOps | Inspired by Nano

[⬆ back to top](#angelus_wys_v2)

</div>
