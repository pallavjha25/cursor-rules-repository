# Cursor Rules Repository

A collection of shareable Cursor rules for enforcing coding standards and best practices across multiple projects.

## 📋 What's Included

This repository contains rules for:

- **Python** - PEP 8 standards, type hints, error handling, docstrings
- **TypeScript** - Type safety, async/await patterns, naming conventions
- **React** - Component patterns, hooks best practices, performance optimization
- **Docker/Kubernetes** - Multi-stage builds, security, resource management
- **General Standards** - Universal coding principles that apply to all languages

## 🚀 Quick Start

### Option 1: Clone into Your Project

```bash
# In your project root
git clone https://github.com/yourusername/cursor-rules-repository .cursor-rules
cp -r .cursor-rules/.cursor .
rm -rf .cursor-rules
```

### Option 2: Git Submodule (Recommended)

```bash
# Add as submodule
git submodule add https://github.com/yourusername/cursor-rules-repository .cursor-rules

# Copy rules to your project
cp -r .cursor-rules/.cursor .

# Update later with
git submodule update --remote
```

### Option 3: Manual Copy

1. Download this repository
2. Copy the `.cursor/rules/` directory to your project root
3. The rules will automatically activate in Cursor

## 📚 Rules Overview

### General Standards (Always Active)

**File:** `general-standards.mdc`  
**Applies:** To all files in every session

Core principles including:
- Code quality and readability
- Error handling patterns
- Testing practices
- Security guidelines
- Git commit conventions

### Python Standards

**File:** `python-standards.mdc`  
**Applies:** `**/*.py`

Standards for:
- PEP 8 compliance
- Type hints and annotations
- Exception handling
- Import organization
- Google-style docstrings

### TypeScript Standards

**File:** `typescript-standards.mdc`  
**Applies:** `**/*.ts`

Best practices for:
- Type safety and avoiding `any`
- Custom error classes
- Async/await patterns
- Naming conventions

### React Patterns

**File:** `react-patterns.mdc`  
**Applies:** `**/*.tsx`, `**/*.jsx`

React-specific guidance on:
- Functional components with TypeScript
- Custom hooks extraction
- Performance optimization with memoization
- State management principles

### Docker & Kubernetes

**File:** `docker-kubernetes.mdc`  
**Applies:** Dockerfiles, docker-compose.yml, k8s manifests

Container and orchestration best practices:
- Multi-stage builds
- Layer optimization
- Security (non-root users)
- Resource limits and health checks

## 🛠️ Customization

### Modifying Rules

1. Edit any `.mdc` file in `.cursor/rules/`
2. Rules update automatically in Cursor
3. Keep rules under 500 lines for best performance

### Adding New Rules

Create a new `.mdc` file in `.cursor/rules/`:

```markdown
---
description: Brief description of the rule
globs: **/*.ext  # File pattern or omit for alwaysApply
alwaysApply: false  # Set to true for universal rules
---

# Rule Title

Your rule content here...
```

### File Patterns (globs)

Common patterns:
- `**/*.py` - All Python files
- `**/*.{ts,tsx}` - All TypeScript files
- `**/test/**/*.py` - Python files in test directories
- `src/**/*.tsx` - React files in src directory

## 🎯 Rule Structure

Each rule file follows this structure:

```markdown
---
description: What this rule enforces
globs: File pattern(s) this rule applies to
alwaysApply: true/false
---

# Rule Title

## Section 1

Content with examples...

✅ GOOD: Best practice example
❌ BAD: Anti-pattern to avoid
```

## 💡 Best Practices for Rule Creation

1. **Keep it Concise** - Under 50 lines per section
2. **Show Examples** - Use ✅/❌ patterns
3. **Be Specific** - Actionable guidance over theory
4. **One Concern** - Focus each rule on a single topic
5. **Update Regularly** - Keep rules current with evolving practices

## 🔄 Keeping Rules Updated

If you're using this as a submodule:

```bash
# Update to latest rules
cd .cursor-rules
git pull origin main
cd ..
cp -r .cursor-rules/.cursor .
```

## 🤝 Contributing

Want to improve these rules?

1. Fork this repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

### Contribution Guidelines

- Keep rules language-agnostic where possible
- Include concrete examples
- Test rules in a real project
- Follow the existing format

## 📖 Usage Tips

### In Cursor

Rules are automatically applied based on:
- **alwaysApply: true** - Active in every session
- **globs pattern** - Active when matching files are open

### Checking Active Rules

In Cursor, you can see which rules are active by:
1. Opening the command palette (Cmd/Ctrl + Shift + P)
2. Searching for "Cursor Rules"

### Disabling Rules Temporarily

To temporarily disable a rule, rename it with a `.disabled` extension:

```bash
mv .cursor/rules/python-standards.mdc .cursor/rules/python-standards.mdc.disabled
```

## 📄 License

MIT License - Feel free to use, modify, and share these rules.

## 🙋 Support

- **Issues**: Report bugs or suggest improvements
- **Discussions**: Share your custom rules or ask questions
- **Wiki**: Additional documentation and examples

## 🌟 Acknowledgments

Created to help teams maintain consistent code quality across projects using Cursor's AI-powered development environment.

---

**Made with ❤️ for better code quality**
