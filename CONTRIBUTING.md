# Contributing to Cursor Rules Repository

Thank you for your interest in contributing! This guide will help you add or improve rules.

## 📋 What Makes a Good Rule

A good rule should be:

1. **Actionable** - Clear guidance that can be immediately applied
2. **Concise** - Under 500 lines, ideally under 50 lines per section
3. **Example-Driven** - Shows both good (✅) and bad (❌) patterns
4. **Focused** - Addresses one concern or topic area
5. **Universal** - Applicable across most projects (unless language-specific)

## 🔧 Rule Structure

Each rule file should follow this template:

```markdown
---
description: Brief one-line description (shown in rule picker)
globs: **/*.ext  # Optional: file pattern for when to apply this rule
alwaysApply: false  # true if rule should always be active
---

# Rule Title

Brief introduction to what this rule covers.

## Section 1: Topic Area

### Subsection (if needed)

Description of the best practice...

\`\`\`language
# ✅ GOOD
good_example()

# ❌ BAD
bad_example()
\`\`\`

## Section 2: Another Topic

Continue with more sections as needed...
```

## 📝 Adding a New Rule

1. **Create the file** in `.cursor/rules/` with `.mdc` extension
2. **Name it descriptively** - `technology-aspect.mdc` (e.g., `go-error-handling.mdc`)
3. **Add frontmatter** with proper metadata
4. **Write content** following the structure above
5. **Test it** in a real project
6. **Update README.md** to list the new rule

### Example: Adding a Go Rule

```bash
# Create the file
touch .cursor/rules/go-standards.mdc
```

```markdown
---
description: Go coding standards and idioms
globs: **/*.go
alwaysApply: false
---

# Go Standards

## Error Handling

Always check errors explicitly:

\`\`\`go
// ✅ GOOD
data, err := fetchData()
if err != nil {
    return fmt.Errorf("failed to fetch data: %w", err)
}

// ❌ BAD
data, _ := fetchData()
\`\`\`
```

## ✏️ Improving Existing Rules

1. **Keep the structure** - Don't change frontmatter unless necessary
2. **Add examples** - More examples are usually better
3. **Update incrementally** - Small, focused changes are easier to review
4. **Test your changes** - Ensure the rule works as expected

## 🧪 Testing Rules

Before submitting, test your rule:

1. Copy the rule to a test project's `.cursor/rules/`
2. Open relevant files to activate the rule
3. Ask Cursor to perform tasks that should trigger the rule
4. Verify the AI follows your guidance

## 📤 Submitting Changes

### For Small Changes

1. Fork the repository
2. Create a branch: `git checkout -b improve-python-rules`
3. Make your changes
4. Commit with clear message: `docs: improve Python error handling examples`
5. Push and create a Pull Request

### For New Rules

1. Fork and create a branch: `git checkout -b add-rust-rules`
2. Add your rule file(s)
3. Update `README.md` to document the new rule
4. Test thoroughly
5. Submit PR with description of what the rule covers

## 📋 Pull Request Checklist

- [ ] Rule file is in `.mdc` format
- [ ] Frontmatter is complete and correct
- [ ] Content is under 500 lines
- [ ] Includes concrete examples with ✅/❌ patterns
- [ ] Tested in a real project
- [ ] README.md updated (if adding new rule)
- [ ] No trailing whitespace or unnecessary formatting
- [ ] Commit messages follow conventional commits format

## 🎨 Style Guide

### Formatting

- Use markdown headers (# ## ###)
- Use code blocks with language tags
- Use ✅ for good examples, ❌ for bad examples
- Keep lines under 100 characters when possible

### Language

- Be direct and clear
- Use imperative mood ("Use X" not "You should use X")
- Avoid jargon unless necessary
- Explain the "why" behind rules

### Code Examples

```markdown
## Good Example Structure

\`\`\`python
# ✅ GOOD: Explain why this is good
def clear_function_name(typed_param: str) -> str:
    """Docstring explaining purpose."""
    return typed_param.upper()

# ❌ BAD: Explain why this is bad
def func(x):
    return x.upper()
\`\`\`
```

## 🔍 Review Process

1. **Automated checks** - CI validates file format and structure
2. **Maintainer review** - Content review for quality and accuracy
3. **Community feedback** - Others may test and provide input
4. **Merge** - Once approved, merged to main

## 💬 Getting Help

- **Questions**: Open a Discussion
- **Bugs**: Open an Issue
- **Ideas**: Open an Issue with "enhancement" label

## 📜 Code of Conduct

- Be respectful and constructive
- Focus on what's best for the community
- Accept feedback gracefully
- Help others learn and grow

## 🎯 Priority Areas

Currently looking for contributions in:

- [ ] Go standards and idioms
- [ ] Rust best practices
- [ ] Java/Kotlin conventions
- [ ] Security-focused rules
- [ ] Accessibility guidelines
- [ ] Performance optimization patterns

## 📚 Resources

- [Cursor Documentation](https://cursor.sh/docs)
- [Markdown Guide](https://www.markdownguide.org/)
- [Conventional Commits](https://www.conventionalcommits.org/)

---

Thank you for contributing to better code quality! 🚀
