# Local Development Guide

This guide helps you set up and work with the resume repository locally.

## Prerequisites

- **Node.js 18+** (for markdownlint and cspell)
- **pandoc** (for HTML/PDF generation)
- **wkhtmltopdf** (for PDF generation)
- **Ruby 3.0+ and Jekyll** (for site preview)
- **stitchmd** (for combining markdown files)

## Quick Setup

### Ubuntu/Debian
```bash
# Install system dependencies
sudo apt-get update
sudo apt-get install -y pandoc wkhtmltopdf ruby-full build-essential zlib1g-dev

# Install Node.js tools
npm install -g markdownlint-cli cspell

# Install Jekyll
gem install jekyll bundler

# Install stitchmd
curl -sSfL https://github.com/abhinav/stitchmd/releases/latest/download/stitchmd-linux-amd64.tar.gz | tar -xzf -
sudo mv stitchmd /usr/local/bin/
```

### macOS
```bash
# Install system dependencies
brew install pandoc wkhtmltopdf ruby node

# Install Node.js tools
npm install -g markdownlint-cli cspell

# Install Jekyll
gem install jekyll bundler

# Install stitchmd
curl -sSfL https://github.com/abhinav/stitchmd/releases/latest/download/stitchmd-darwin-amd64.tar.gz | tar -xzf -
sudo mv stitchmd /usr/local/bin/
```

### Windows
```powershell
# Install Chocolatey first (https://chocolatey.org/)
# Then install dependencies
choco install pandoc wkhtmltopdf nodejs ruby

# Install Node.js tools
npm install -g markdownlint-cli cspell

# Install Jekyll
gem install jekyll bundler

# Download stitchmd manually from GitHub releases
```

## Development Workflow

### 1. Content Updates

**Edit source files in `src/` directory** (never edit `README.md` directly):

```bash
# Edit content
vim src/WorkExperience.md
vim src/Certifications.md

# Lint your changes
markdownlint src/*.md --config .markdownlint.json

# Check spelling
cspell "src/*.md" --config .cspell.json

# Check links
lychee src/*.md --config .lycheerc.toml
```

### 2. Generate Combined README

```bash
# Combine all sections into README.md
stitchmd -o README.md src/RESUME.md
```

### 3. PDF Generation

```bash
# Generate HTML with ATS-friendly styling
pandoc README.md -o RESUME.html --standalone --css=src/PDF_ATS.css --metadata title="Victor Witkamp - Resume"

# Generate PDF
wkhtmltopdf --enable-local-file-access --page-size A4 --orientation Portrait --margin-top 15mm --margin-bottom 15mm --margin-left 15mm --margin-right 15mm RESUME.html RESUME.pdf

# Quick test PDF generation
npm run build:pdf  # (if you add this script to package.json)
```

### 4. Jekyll Site Preview

```bash
# Start Jekyll development server
jekyll serve

# Or with live reload
jekyll serve --livereload

# Site will be available at http://localhost:4000/resume/
```

### 5. Complete Build Test

Run the full build process locally:

```bash
#!/bin/bash
# Create this as scripts/local-build.sh

set -e  # Exit on error

echo "🔍 Running quality checks..."
markdownlint src/*.md --config .markdownlint.json
cspell "src/*.md" --config .cspell.json

echo "🔗 Checking links..."
lychee src/*.md --config .lycheerc.toml

echo "📝 Generating README..."
stitchmd -o README.md src/RESUME.md

echo "📄 Generating PDF..."
pandoc README.md -o RESUME.html --standalone --css=src/PDF_ATS.css --metadata title="Victor Witkamp - Resume"
wkhtmltopdf --enable-local-file-access --page-size A4 --orientation Portrait --margin-top 15mm --margin-bottom 15mm --margin-left 15mm --margin-right 15mm RESUME.html RESUME.pdf

echo "🌐 Building Jekyll site..."
jekyll build

echo "✅ Build complete! Check _site/ directory and RESUME.pdf"
```

## File Structure

```
resume/
├── src/                     # Source content (EDIT THESE)
│   ├── RESUME.md           # Main template/summary
│   ├── Introduction.md     # Personal introduction
│   ├── Education.md        # Educational background
│   ├── WorkExperience.md   # Professional experience
│   ├── Certifications.md  # Professional certifications
│   ├── PDF_ATS.css        # PDF styling
│   └── *.png              # Certificate badges
├── .github/
│   └── workflows/
│       ├── jekyll-gh-pages.yml  # Main build/deploy
│       └── security.yml         # Security scanning
├── _config.yml             # Jekyll configuration
├── README.md               # Auto-generated (DON'T EDIT)
├── RESUME.pdf             # Auto-generated PDF
└── _site/                 # Jekyll build output
```

## Content Guidelines

### Work Experience Format
```markdown
### **COMPANY NAME**

START_DATE - END_DATE

***Job Title***

```Technology1```
```Technology2```
```Technology3```

Description of role and responsibilities...
___
```

### Certification Format
```markdown
### Certification Name

ISSUE_DATE

[Link to credential](URL)

![Badge Description](src/badge-image.png)
```

### Skills Format
Use code blocks for technologies:
```markdown
```Microsoft Azure```
```PowerShell```
```Juniper```
```

## Testing Your Changes

### Before Committing
```bash
# Run all quality checks
markdownlint src/*.md --config .markdownlint.json
cspell "src/*.md" --config .cspell.json
lychee src/*.md --config .lycheerc.toml

# Test PDF generation
stitchmd -o README.md src/RESUME.md
pandoc README.md -o test.pdf --css=src/PDF_ATS.css
test -s test.pdf && echo "✅ PDF generated successfully"

# Test Jekyll build
jekyll build
```

### Visual Verification
1. Open `RESUME.pdf` and check:
   - Skills appear as styled blocks (not plain text)
   - All sections are present and formatted correctly
   - Images load properly
   - No broken layouts

2. Preview Jekyll site:
   - Start `jekyll serve`
   - Check responsive design on mobile
   - Verify all links work
   - Test PDF download link

## Troubleshooting

### Common Issues

**1. PDF Generation Fails**
```bash
# Check pandoc version
pandoc --version

# Check wkhtmltopdf version
wkhtmltopdf --version

# Test with minimal content
echo "# Test" | pandoc -o test.pdf --css=src/PDF_ATS.css
```

**2. Jekyll Build Fails**
```bash
# Check Ruby/Jekyll versions
ruby --version
jekyll --version

# Clear Jekyll cache
jekyll clean
```

**3. Markdownlint Errors**
```bash
# Show detailed error information
markdownlint src/*.md --config .markdownlint.json --fix
```

**4. Stitchmd Not Working**
```bash
# Check stitchmd installation
which stitchmd
stitchmd --version

# Test with simple file
stitchmd -o test.md src/RESUME.md
```

### Getting Help

1. Check GitHub Actions logs for CI/CD issues
2. Review error messages carefully
3. Ensure all dependencies are installed
4. Verify file permissions and paths
5. Test with minimal content to isolate issues

## Performance Tips

- **Cache Dependencies**: Install tools globally to avoid repeated downloads
- **Incremental Builds**: Only regenerate PDF when content changes
- **Local Preview**: Use Jekyll's live reload for quick iterations
- **Batch Changes**: Group related updates together

## Next Steps

After setting up local development:

1. **Make a small test change** to verify everything works
2. **Add your own package.json** with helpful scripts
3. **Create aliases** for common commands
4. **Set up editor plugins** for Markdown linting
5. **Configure git hooks** for automatic quality checks

Happy developing! 🚀