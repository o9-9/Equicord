# Workflow Configuration Summary

## ✅ What's Configured

```
.github/workflows/
├── test.yml        ← Tests code quality on every push/PR
└── build.yml       ← Builds and releases on push to main
```

## 🎯 Quick Start

### Your workflows will now:

1. **On every push/PR to `main` or `dev`:**
   - ✅ Run linting
   - ✅ Test compilation
   - ✅ Validate plugins

2. **On every push to `main`:**
   - ✅ Build desktop & web versions
   - ✅ Create browser extensions
   - ✅ Generate plugin metadata
   - ✅ Upload to "latest" release (pre-release)

3. **When you create a version tag:**
   ```bash
   git tag v1.0.0
   git push origin v1.0.0
   ```
   - ✅ Creates official release
   - ✅ Includes all build files
   - ✅ Not marked as pre-release

## 📦 What Gets Built

Every successful build produces:

| File Type | Description |
|-----------|-------------|
| `*.asar` | Desktop client files (Vencord/Vesktop) |
| `extension-chrome.zip` | Chrome browser extension |
| `extension-firefox.zip` | Firefox browser extension |
| `Equicord.user.js` | Userscript for Tampermonkey/Greasemonkey |
| `plugins.json` | All plugins metadata |
| `equicordplugins.json` | Equicord-specific plugins |
| `vencordplugins.json` | Vencord plugins |
| `devs.json` | Plugin developers list |

## 🚀 First Time Setup

1. **Enable GitHub Actions** (if not already enabled):
   - Go to repository Settings → Actions → General
   - Under "Actions permissions", select "Allow all actions"
   - Under "Workflow permissions", select "Read and write permissions"
   - Click "Save"

2. **Push to main** to trigger your first build:
   ```bash
   git add .
   git commit -m "Configure custom workflows"
   git push origin main
   ```

3. **Check the Actions tab** to see your build in progress

4. **Download from Releases page** once complete

## ⚙️ Optional Customization

### Build on Multiple Branches
Edit `.github/workflows/build.yml`:
```yaml
on:
    push:
        branches:
            - main
            - develop  # Add your branch
```

### Schedule Nightly Builds
Add to `.github/workflows/build.yml`:
```yaml
on:
    schedule:
        - cron: '0 0 * * *'  # Daily at midnight UTC
```

### Build on Release Creation
Add to `.github/workflows/build.yml`:
```yaml
on:
    release:
        types: [created]
```

## 🔧 Manual Build

Trigger a build without pushing:
1. Go to **Actions** tab
2. Select **Build & Release**
3. Click **Run workflow**
4. Choose branch and click **Run workflow**

## 📊 Monitoring

- **Actions tab**: See all workflow runs
- **Releases page**: Download built files
- **Artifacts**: Temporary builds (90-day retention)

## 🛠️ Troubleshooting

### "Permission denied" error
→ Enable write permissions (Settings → Actions → General → Workflow permissions)

### Build succeeds but no release
→ Check if "latest" tag exists; first run will create it

### Missing build files
→ Check workflow logs to see what was generated

### Want to disable builds temporarily?
→ Actions tab → Select workflow → ⋯ → Disable workflow

---

## 📚 More Information

See [WORKFLOWS.md](WORKFLOWS.md) for detailed documentation.

---

**Your fork is now self-contained and ready to build!** 🎉
