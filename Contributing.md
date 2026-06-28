# Contributing to angelus_wys_v2 

First off, thank you for considering contributing to aangelus_wys_v2! It's people like you that make angelus_wys_v2 such a great tool.

We welcome contributions of all kinds:
- 🐛 **Bug reports**: Found an issue? Let us know
- 💡 **Feature ideas**: Have an idea? Share it
- 📝 **Documentation**: Improve our docs
- 🔨 **Code**: Submit a fix or feature
- ✅ **Testing**: Help us test

---

## Code of Conduct

We are committed to providing a welcoming and inspiring community for all. Please be respectful and constructive in all interactions.

---

## Getting Started

### 1. Fork and Clone

```bash
# Fork on GitHub (click the Fork button)

# Clone your fork
git clone https://github.com/FernandoSaraiva0/angelus_wys_v2
cd AngelusWys

# Add upstream remote
git remote add upstream https://github.com/FernandoSaraiva0/angelus_wys_v2
```

### 2. Create a Feature Branch

```bash
# Always start from main
git fetch upstream
git checkout -b feat/your-feature-name upstream/main

# Or for bugs
git checkout -b fix/bug-description upstream/main
```

### 3. Make Your Changes

See [GETTING_STARTED.md](./GETTING_STARTED.md) for development setup.

```bash
# Edit files
vim src/editor.rs

# Test locally
cargo test
cargo clippy
cargo fmt
```

### 4. Commit with Care

```bash
# Stage your changes
git add src/

# Commit with clear message
git commit -m "feat(editor): add cursor movement with arrow keys"
```

**Commit Message Format** (Conventional Commits):

```
type(scope): subject

body (optional)

footer (optional)
```

| Type | Scope | Example |
|------|-------|---------|
| `feat` | editor, buffer, input, display | feat(input): add mouse support |
| `fix` | same as above | fix(display): correct cursor offset |
| `docs` | readme, contributing, api | docs(readme): update keybindings |
| `test` | same as code | test(buffer): add insert_line tests |
| `refactor` | same as code | refactor(display): simplify rendering |
| `perf` | same as code | perf(buffer): optimize line search |
| `chore` | build, ci, deps | chore(deps): update crossterm |
| `ci` | github actions | ci: add coverage reporting |

**Rules**:
- ✅ Use imperative mood ("add feature" not "adds feature")
- ✅ Don't capitalize first letter
- ✅ Reference issues: "fix: resolve issue #123"
- ✅ One feature per commit when possible

### 5. Push and Create Pull Request

```bash
# Push to your fork
git push origin feat/your-feature-name

# Go to GitHub and click "Create Pull Request"
```

### 6. Describe Your Pull Request

Provide a clear description:

```markdown
## Description
Brief description of what this PR does.

## Motivation
Why is this change needed?

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Documentation
- [ ] Performance improvement

## Changes Made
- Change 1
- Change 2

## Testing
How did you test this?

## Checklist
- [ ] Code follows style guidelines
- [ ] Tests added/updated
- [ ] Documentation updated
- [ ] No breaking changes
- [ ] All tests pass locally

## Issues
Closes #123
```

---

## Development Guidelines

### Code Style

We follow Rust conventions:

```bash
# Format your code
cargo fmt

# This is required; CI will reject non-formatted code
```

### Naming Conventions

```rust
// Types: PascalCase
struct TextBuffer { }
enum Command { }

// Functions & variables: snake_case
fn insert_character() { }
let current_line = 0;

// Constants: UPPER_SNAKE_CASE
const MAX_BUFFER_SIZE: usize = 1_000_000;

// Private: use `priv` prefix
fn _helper_function() { }
```

### Documentation

All public APIs must have documentation:

```rust
/// Brief description (one line).
///
/// Longer description if needed.
///
/// # Examples
/// ```
/// let buffer = Buffer::new();
/// assert_eq!(buffer.line_count(), 1);
/// ```
///
/// # Errors
/// Returns `Err` if file cannot be read.
///
/// # Panics
/// Panics if index is out of bounds.
pub fn new() -> Self {
    // ...
}
```

### Testing

Write tests for new features:

```rust
#[test]
fn test_feature_works() {
    // Arrange
    let mut buffer = Buffer::new();
    
    // Act
    buffer.insert_line(0, "test".to_string());
    
    // Assert
    assert_eq!(buffer.line_count(), 2);
}
```

**Test naming**: `test_what_it_does`  
**Assertion messages**: `assert_eq!(actual, expected, "reason why they should match")`

### Performance

For performance-critical code:

```bash
# Profile with cargo flamegraph
cargo flamegraph -- file.txt

# Or use perf on Linux
perf record ./target/release/nano
perf report
```

### Error Handling

Use `anyhow::Result` for user-facing code:

```rust
use anyhow::{Result, Context};

pub fn load_file(path: &Path) -> Result<String> {
    std::fs::read_to_string(path)
        .context("failed to read file")
}
```

Never use `.unwrap()` in library code (ok in examples/tests).

---

## PR Review Process

### Automated Checks

Your PR will be checked by:
- ✅ **Build**: Does it compile?
- ✅ **Tests**: Do tests pass?
- ✅ **Clippy**: Any warnings?
- ✅ **Fmt**: Is code formatted?
- ✅ **Docs**: Is API documented?

All must pass before merge.

### Human Review

A maintainer will review:
- ✅ Does it solve the problem?
- ✅ Is the design sound?
- ✅ Are there tests?
- ✅ Is documentation complete?
- ✅ Does it follow guidelines?

### Common Feedback

**"Add a test"**
```bash
# Add test to src/module.rs
#[test]
fn test_your_feature() { ... }

# Run test
cargo test
```

**"Add documentation"**
```rust
/// Describe what this does
/// 
/// # Examples
/// ```
/// your_function()
/// ```
pub fn your_function() { }
```

**"Simplify this"**  
Consider refactoring. We value clear code over clever code.

**"This breaks existing tests"**  
Fix the code or update the tests if the change is intentional.

---

## Types of Contributions

### 🐛 Bug Reports

Create an issue with:
- **Title**: Clear description of the bug
- **Environment**: OS, Rust version, cargo version
- **Steps to reproduce**: Exact steps to trigger the bug
- **Expected behavior**: What should happen
- **Actual behavior**: What actually happens
- **Screenshots/logs**: If applicable

Example:
```markdown
# Bug: Editor crashes on empty file save

## Environment
- OS: Ubuntu 22.04
- Rust: 1.70.0
- AngelusWys: main branch

## Steps
1. Run `cargo run`
2. Press Ctrl+S immediately
3. Editor crashes

## Error
```
thread 'main' panicked at 'called `Option::unwrap()` on a `None` value'
```

## Expected
File is saved successfully
```

### 💡 Feature Requests

Create an issue with:
- **Title**: Short description
- **Motivation**: Why is this needed?
- **Proposal**: How should it work?
- **Alternatives**: Other approaches?

Example:
```markdown
# Feature: Mouse support

## Motivation
Some users prefer mouse for positioning.

## Proposal
- Click to position cursor
- Scroll wheel to move up/down

## Alternatives
Could use other cursor positioning methods.
```

### 📝 Documentation

Improvements to docs are always welcome:
- Typos and clarifications
- Better examples
- Architecture documentation
- API documentation
- Tutorial content

Just edit and submit a PR!

### 🔨 Code Contributions

For larger features:

1. **Discuss first**: Open an issue or discussion
2. **Get approval**: Wait for feedback
3. **Implement**: Create a PR
4. **Review**: Respond to feedback
5. **Merge**: Celebrate! 🎉

For small fixes:
1. **Fix it**: Make the change
2. **Test it**: Verify it works
3. **Submit PR**: Create a pull request

---

## Release Process

We follow [Semantic Versioning](https://semver.org/):

- **Major (X.0.0)**: Breaking changes
- **Minor (0.Y.0)**: New features
- **Patch (0.0.Z)**: Bug fixes

Release timeline: As features are ready (no fixed schedule for MVP)

---

## Questions?

- 📖 Check [GETTING_STARTED.md](./GETTING_STARTED.md)
- 📚 Read [README.md](./README.md)
- 💬 Open a [discussion](https://github.com/FernandoSaraiva0/angelus_wys_v2/discussions)
- 📧 Email maintainers

---

## Recognition

Contributors will be:
- ✅ Listed in [CONTRIBUTORS.md](./CONTRIBUTORS.md) (coming)
- ✅ Credited in release notes
- ✅ Thanked in README

---

## Additional Resources

- [Rust API Guidelines](https://rust-lang.github.io/api-guidelines/)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [Keep a Changelog](https://keepachangelog.com/)
- [Semantic Versioning](https://semver.org/)
- [GitHub PR Best Practices](https://docs.github.com/en/pull-requests)

---

Thank you for contributing! 🙏

---

<div align="center">

Made with ❤️ by the angelus_wys_v2 community

</div>
