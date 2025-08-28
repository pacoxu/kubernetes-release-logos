# Kubernetes Release Logos Repository

**Always reference these instructions first and fallback to search or bash commands only when you encounter unexpected information that does not match the info here.**

## Repository Overview

This is a static asset repository containing Kubernetes release logos from version 1.10 onwards. The repository serves as a centralized collection of official release logos used across the Kubernetes ecosystem. There are no build systems, dependencies, tests, or compilation steps - this is purely a static asset collection.

## Working Effectively

### Repository Structure
- **Root directory**: Contains 24 logo image files (PNG, JPEG, SVG formats)
- **README.md**: Displays all logos with their version names and release codenames
- **LICENSE**: Apache License 2.0
- **.gitignore**: Simple file excluding .vagrant/ and .DS_Store
- **Kubernetes Blog | Kubernetes.webloc**: Mac shortcut to Kubernetes blog

### File Naming Convention
- Logo files follow the pattern: `v{major}.{minor}.{extension}`
- Examples: `v1.33.svg`, `v1.32.png`, `v1.14.jpeg`
- Supported formats: PNG (preferred), JPEG, SVG
- Version range: v1.10 through v1.33 (24 files total)

### Common Operations

#### Validate Repository State
- Run `ls -la v1.*.* | wc -l` to count logo files (should be 24)
- Run `file v1.33.svg v1.32.png v1.14.jpeg` to verify image formats
- Run `grep -c "v1\." README.md` to count version references (should be 48 - 2 per version)

#### Add New Release Logo
1. **Add the logo file**: 
   - Use naming convention `v{major}.{minor}.{extension}`
   - Preferred format is PNG, but JPEG and SVG are acceptable
   - Place in repository root directory
2. **Update README.md**:
   - Add new version section at the top (after line 3, before existing versions)
   - Follow format: `## v{version} - {codename}` followed by `![{codename}](v{version}.{extension})`
   - Example:
     ```markdown
     ## v1.34 - New Codename
     ![New Codename](v1.34.png)
     ```
3. **Validate additions**:
   - Run `file v{version}.{extension}` to verify image format
   - Check README renders correctly with `grep -A2 -B2 "v{version}" README.md`

#### Verify Image Integrity
- Run `file v1.*.* | grep -v "image data\|SVG"` to find corrupted files (should return empty)
- Check file sizes with `ls -lah v1.*.* | awk '{print $5, $9}' | sort -hr | head -5` 
- Typical sizes: 50KB-4.5MB (PNG/JPEG vary widely), SVG typically 1-2MB

#### README Maintenance
- Ensure versions are listed in descending order (newest first)
- Each version should have exactly 2 lines: header and image reference
- Image alt text should match the release codename
- Image path should be relative (no directory prefix)

## Validation Scenarios

### After Adding New Logo
1. **File validation**: Run `file v{new_version}.{ext}` - should show valid image type
2. **README validation**: Run `grep -A1 "v{new_version}" README.md` - should show header and image line
3. **Naming validation**: Ensure filename matches README image reference exactly
4. **Positioning validation**: New version should be at the top of the version list

### Repository Health Check
- Run `ls v1.*.* | wc -l && grep -c "##.*v1\." README.md` - both numbers should match (should be 24)
- Run `diff <(ls v1.*.* | sed 's/\.[^.]*$//' | sort) <(grep -o 'v1\.[0-9]*' README.md | sort | uniq)` - should show no differences
- Check for formatting issues: `grep -n '#.*v1\.' README.md | grep -v '##'` - should return empty (catches single # instead of ##)

## File Management

### DO NOT modify:
- LICENSE file
- .gitignore file  
- Existing logo files (unless replacing with higher quality version)
- .git directory contents

### Safe to modify:
- README.md (when adding new versions or fixing display issues)
- Adding new v{major}.{minor}.{ext} logo files

## No Build System

**IMPORTANT**: This repository has no build system, tests, or dependencies.
- Do not run `npm install`, `make`, `pip install`, or similar commands
- Do not look for package.json, Makefile, or build scripts - they don't exist
- No linting tools are configured - manual review is sufficient
- No automated tests exist - manual validation is the process

## Expected Workflow Times

All operations in this repository are near-instantaneous:
- Adding new logo file: < 1 second
- Updating README.md: < 1 second  
- Validation commands: < 1 second each
- Git operations: < 5 seconds

## Common Commands Reference

### Inventory and Validation
```bash
# Count logo files
ls -la v1.*.* | wc -l

# Verify image formats  
file v1.*.* | head -5

# Check README structure
grep -c "v1\." README.md

# List versions in README order
grep "## v1\." README.md | head -5
```

### File Operations
```bash
# Add new logo (example)
cp new_logo.png v1.34.png

# Verify new file
file v1.34.png

# Check file size
ls -lah v1.34.png
```

### Git Operations
```bash
# Check repository status
git status

# View recent changes
git diff

# Check commit history
git log --oneline | head -5
```

## Repository Statistics
- **Total logo files**: 24 (v1.10 through v1.33)
- **File formats**: PNG (21 files), JPEG (2 files), SVG (1 file)  
- **README entries**: 48 lines (2 per version: header + image)
- **Repository size**: ~34MB (primarily image assets)
- **Latest version**: v1.33 - Octarine

## Troubleshooting

### Missing Logo Display
- Verify filename matches README image reference exactly (case-sensitive)
- Ensure file is in repository root, not subdirectory
- Check file is valid image format with `file` command

### README Formatting Issues
- Ensure each version has exactly one blank line separation
- Verify image syntax: `![Alt Text](filename.ext)`
- Check version ordering (newest first)

### File Corruption
- Re-download/re-add the logo file
- Verify with `file` command shows valid image data
- Check file size is reasonable (not 0 bytes or extremely large)