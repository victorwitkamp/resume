# GitHub Copilot Instructions

## Repository Overview

This is a personal resume repository that uses Jekyll and GitHub Pages for automated deployment. The repository maintains a professional resume in multiple formats (Markdown, HTML, PDF) with automated build and deployment processes.

## Repository Structure

```
├── README.md                 # Main resume content (auto-generated)
├── _config.yml              # Jekyll configuration
├── src/                     # Modular resume sections
│   ├── RESUME.md           # Resume summary/template
│   ├── Introduction.md     # Personal introduction
│   ├── Education.md        # Educational background
│   ├── WorkExperience.md   # Professional experience
│   ├── Certifications.md  # Professional certifications
│   ├── PDF_ATS.css            # Styling for PDF generation
│   └── *.png              # Certificate badges and images
└── .github/
    └── workflows/
        └── jekyll-gh-pages.yml  # Automated build and deployment
```

## Key Concepts

### Modular Content Structure
- The resume is split into logical sections in the `src/` directory
- Each section is a separate Markdown file for easy maintenance
- The `stitchmd-action` combines these files into `README.md` during build
- This approach allows for better organization and version control of content

### Automated Build Process
1. **Content Assembly**: `stitchmd-action` combines src/RESUME.md with other sections
2. **PDF Generation**: Uses `pandoc` and `wkhtmltopdf` to create PDF version
3. **Jekyll Build**: Processes Markdown into static HTML site
4. **GitHub Pages Deployment**: Automatically deploys to GitHub Pages

### File Relationships
- `src/RESUME.md` serves as the main template/summary
- Other `src/*.md` files contain detailed sections
- `src/PDF_ATS.css` provides styling specifically for PDF output
- `_config.yml` configures Jekyll theme and site metadata

## Development Guidelines

### Content Updates
When updating resume content:
1. **Always edit source files in `src/` directory, never edit `README.md` directly**
2. `README.md` is auto-generated and will be overwritten on next build
3. Use consistent Markdown formatting across all sections
4. Maintain chronological order (newest first) for experience and certifications
5. Use code blocks (```) for technologies and skills
6. Include relevant links and badges for certifications

### Adding New Sections
To add a new resume section:
1. Create a new `.md` file in `src/` directory
2. Follow existing naming convention (PascalCase)
3. Update `src/RESUME.md` to reference the new section if needed
4. Ensure consistent formatting with existing sections

### Technical Skills Format
Use consistent formatting for technical skills:
```markdown
```Technology Name```
```
This creates styled code blocks that stand out in both HTML and PDF output.

### Image and Asset Management
- Store certification badges and images in `src/` directory
- Use relative paths when referencing images
- Optimize images for web delivery (reasonable file sizes)
- Use descriptive alt text for accessibility

### Build and Deployment
- All builds are automated via GitHub Actions
- Changes to `main` branch trigger automatic deployment
- PDF generation requires `pandoc` and `wkhtmltopdf` dependencies
- GitHub Pages serves the Jekyll-generated site

## Common Patterns

### Work Experience Entry
```markdown
### **COMPANY NAME**
START_DATE - END_DATE

***Job Title***

```Technology1```
```Technology2```
```Technology3```

Description of role and responsibilities...
```

### Certification Entry
```markdown
### Certification Name

ISSUE_DATE

[Link to credential](URL)

![Badge Description](src/badge-image.png)
```

## Troubleshooting

### PDF Generation Issues
- Ensure `src/PDF_ATS.css` is properly formatted CSS
- Check that all image paths are correct and files exist
- Verify `wkhtmltopdf` can access local files (--enable-local-file-access flag)

### Jekyll Build Issues
- Validate YAML frontmatter in `_config.yml`
- Ensure Markdown syntax is valid across all files
- Check for any special characters that might break Jekyll processing

### Content Assembly Issues
- Verify `src/RESUME.md` exists and has proper structure
- Ensure all referenced section files exist in `src/` directory
- Check that `stitchmd-action` configuration in workflow is correct

## Best Practices

1. **Keep content current**: Regularly update work experience and certifications
2. **Maintain consistency**: Use the same formatting patterns throughout
3. **Test changes**: Use GitHub's preview functionality to check Markdown rendering
4. **Backup important changes**: Git history serves as version control for career progression
5. **Professional presentation**: Maintain professional language and formatting
6. **Accessibility**: Include alt text for images and use semantic Markdown structures

## Automation Features

- **Automatic README generation**: Content from `src/` files is automatically assembled
- **PDF creation**: Professional PDF version is generated with each update
- **GitHub Pages deployment**: Changes are automatically published to the web
- **Asset management**: Images and stylesheets are properly included in builds

This repository demonstrates effective use of Git workflows, GitHub Actions, and Jekyll for maintaining a professional online presence.