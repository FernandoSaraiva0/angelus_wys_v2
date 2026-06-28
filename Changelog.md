# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Initial project structure with modular design
- GitHub Actions CI/CD pipeline
  - Automated build and test on every push
  - Code formatting check (cargo fmt)
  - Linting with Clippy
  - Documentation generation
- Core modules:
  - `buffer.rs`: Text buffer management with file I/O
  - `editor.rs`: Main editor loop and state management
  - `input.rs`: Keyboard event handling
  - `display.rs`: Terminal rendering with crossterm
  - `main.rs`: CLI entry point with argument parsing
- Basic keybindings:
  - `Ctrl+S`: Save file
  - `Ctrl+Q`: Quit editor
  - `:q`: Vim-style quit
- Integration tests framework
- Comprehensive README with project overview
- Initial architecture documentation

### Planned
- Text editing operations (insert, delete, select)
- Copy/cut/paste functionality
- Undo/Redo stack
- Search and replace
- Syntax highlighting
- Configuration support

---

## [0.1.0] - 2024-01-XX

### Added (Initial MVP Release)

#### Core Features
- ✅ Create new files
- ✅ Open existing files
- ✅ Save files to disk
- ✅ Navigate with arrow keys
- ✅ Graceful exit handling

#### User Interface
- ✅ Terminal-based interface using crossterm
- ✅ Status bar with file info and shortcuts
- ✅ Line numbers (foundational)
- ✅ Raw terminal mode for better control

#### Development Infrastructure
- ✅ GitHub Actions workflow
  - Build check
  - Test suite
  - Code quality (clippy, fmt)
- ✅ Modular Rust code structure
- ✅ Error handling with anyhow
- ✅ CLI parsing with clap

#### Documentation
- ✅ Comprehensive README
- ✅ Code comments and documentation
- ✅ Contributing guidelines
- ✅ Architecture overview

#### Testing
- ✅ Unit test framework
- ✅ Integration test setup
- ✅ CI automation

### Known Issues
- Large file support limited to available RAM
- No syntax highlighting yet
- Basic error messages only

### Technical Details
- **Rust Edition**: 2021
- **MSRV**: 1.70
- **Dependencies**: 3 production, 2 development
- **Binary Size**: ~5MB (release build)

---

## Release Notes Format

For future releases, follow this template:

```markdown
## [X.Y.Z] - YYYY-MM-DD

### Added
- Feature one
- Feature two

### Changed
- Behavior change one
- Behavior change two

### Deprecated
- Deprecated feature X (will be removed in 2.0)

### Removed
- Removed feature Y

### Fixed
- Fixed bug A
- Fixed bug B

### Security
- Security fix for issue #XXX
```

---

## Versioning Strategy

This project follows [Semantic Versioning](https://semver.org/):

- **Major (X.y.z)**: Breaking changes, significant rewrites
- **Minor (x.Y.z)**: New features, backward compatible
- **Patch (x.y.Z)**: Bug fixes, performance improvements

### Release Cycle

- **Alpha** (0.1.x): MVP, initial development
- **Beta** (0.2.x to 0.9.x): Feature complete, testing phase
- **Stable** (1.0+): Production-ready, API stable

---

## Upgrading

### From 0.1.0 to 0.2.0 (Planned)

When released, upgrade with:
```bash
cargo install angelus_wys_v2 --version 0.2.0
```

Breaking changes (if any) will be clearly documented.

---

## Archive

### Previous Versions
- No previous releases yet (initial development)

---

For more detailed version history, check the [Git commit log](https://github.com/FernandoSaraiva0/angelus_wys_v2/commits/main).
