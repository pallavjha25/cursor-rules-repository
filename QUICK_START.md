# Quick Start Guide

Get up and running with Cursor Rules in under 5 minutes.

## 🎯 What You Get

This repository provides **5 comprehensive rule files** (654 lines total) that automatically guide Cursor's AI agent:

| Rule File | Applies To | Lines | Purpose |
|-----------|-----------|-------|---------|
| `general-standards.mdc` | All files (always) | 156 | Universal coding principles |
| `docker-kubernetes.mdc` | Docker/K8s files | 165 | Container best practices |
| `react-patterns.mdc` | `.tsx`, `.jsx` files | 130 | React component patterns |
| `typescript-standards.mdc` | `.ts` files | 109 | TypeScript conventions |
| `python-standards.mdc` | `.py` files | 94 | Python PEP 8 & best practices |

## 📦 Installation

### Option 1: Quick Copy (Simplest)

```bash
# Clone this repo
git clone https://github.com/YOUR_USERNAME/cursor-rules-repository.git

# Copy rules to your project
cd your-project
cp -r path/to/cursor-rules-repository/.cursor .

# Done! Rules are now active
```

### Option 2: Git Submodule (Best for Updates)

```bash
# In your project root
git submodule add https://github.com/YOUR_USERNAME/cursor-rules-repository .cursor-rules

# Copy rules
cp -r .cursor-rules/.cursor .

# Commit
git add .cursor .gitmodules .cursor-rules
git commit -m "chore: add Cursor rules"

# Later: update to latest rules
git submodule update --remote .cursor-rules
cp -r .cursor-rules/.cursor .
```

### Option 3: Direct Download

1. Download this repository as ZIP
2. Extract it
3. Copy the `.cursor` folder to your project root
4. Done!

## ✅ Verify Installation

1. Open your project in Cursor
2. Open a Python file (`.py`) - Python rules should activate
3. Ask Cursor: "Review this code"
4. Cursor should follow the guidelines from `python-standards.mdc`

Check active rules:
- Open Command Palette (Cmd/Ctrl + Shift + P)
- Search for "Cursor Rules"
- View which rules are currently active

## 🎨 Try It Out

### Test Python Rules

Create `test.py`:

```python
def get_data(id):
    try:
        return fetch(id)
    except:
        return None
```

Ask Cursor: "Improve this function"

Expected improvements:
- Add type hints
- Better exception handling
- Add docstring
- Improve parameter naming

### Test React Rules

Create `Component.tsx`:

```typescript
export function User(props: any) {
  const [data, setData] = useState(null);
  
  useEffect(() => {
    fetch(`/api/users/${props.id}`).then(r => r.json()).then(setData);
  });
  
  return <div>{data?.name}</div>;
}
```

Ask Cursor: "Improve this component"

Expected improvements:
- Proper TypeScript types
- Custom hook extraction
- Error handling
- Loading states
- useEffect cleanup

### Test Docker Rules

Create `Dockerfile`:

```dockerfile
FROM node:20
COPY . /app
WORKDIR /app
RUN npm install
CMD ["node", "index.js"]
```

Ask Cursor: "Improve this Dockerfile"

Expected improvements:
- Multi-stage build
- Non-root user
- Layer optimization
- Health check

## 🔧 Customization

### Modify Existing Rules

Edit any `.mdc` file in `.cursor/rules/`:

```bash
code .cursor/rules/python-standards.mdc
```

Changes take effect immediately (no restart needed).

### Add New Rules

Create a new `.mdc` file:

```bash
touch .cursor/rules/my-custom-rule.mdc
```

Add frontmatter and content:

```markdown
---
description: My custom coding standard
globs: **/*.js
alwaysApply: false
---

# My Custom Rule

Your guidance here...
```

### Disable a Rule

Temporarily disable by renaming:

```bash
mv .cursor/rules/python-standards.mdc .cursor/rules/python-standards.mdc.disabled
```

Re-enable by removing `.disabled`.

## 📚 Learn More

- **[README.md](README.md)** - Comprehensive documentation
- **[EXAMPLES.md](EXAMPLES.md)** - See rules in action
- **[CONTRIBUTING.md](CONTRIBUTING.md)** - Add your own rules

## 🐛 Troubleshooting

### Rules Not Working?

1. **Check file location**: Rules must be in `.cursor/rules/` (note the dot!)
2. **Check file extension**: Must be `.mdc` not `.md`
3. **Check frontmatter**: Verify YAML is valid
4. **Restart Cursor**: Sometimes needed after adding rules

### Which Rules Are Active?

Open a file and check:
- Command Palette → "Cursor Rules" → See active rules
- Rules with `alwaysApply: true` are always active
- Others activate based on file patterns

### Rule Not Triggering?

Check the `globs` pattern matches your file:
- `**/*.py` - All Python files
- `**/*.{ts,tsx}` - All TypeScript files
- `src/**/*.js` - JS files in src directory

## 🚀 Next Steps

1. ✅ Install rules in your project
2. ✅ Test with a few files
3. ✅ Customize rules for your needs
4. ✅ Share with your team
5. ✅ Contribute improvements back!

## 💡 Pro Tips

- **Start small**: Enable one rule at a time to understand impact
- **Team adoption**: Share via git submodule for easy updates
- **Customize freely**: Fork and adapt to your standards
- **Stay updated**: Pull latest rules regularly for improvements

---

**Ready to code with AI guidance? Your rules are now active! 🎉**
