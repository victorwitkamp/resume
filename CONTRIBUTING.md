# Contributing to Resume Project

Thank you for your interest in contributing to this resume project! This document provides guidelines for making contributions.

## 📋 Project Overview

This is a personal resume repository that uses Jekyll for static site generation and GitHub Actions for CI/CD. The content is written in Markdown and automatically converted to HTML and PDF formats.

## 🛠️ Making Changes

### Content Updates

1. **Resume Content**: Edit files in the `src/` directory:
   - `src/RESUME.md` - Main resume content
   - `src/Education.md` - Education section
   - `src/Certifications.md` - Certifications section  
   - `src/WorkExperience.md` - Work experience section

2. **Styling**: Modify `src/PDF.css` for PDF output styling

3. **Configuration**: Update `_config.yml` for Jekyll settings

### File Organization

- Keep all resume content in the `src/` directory
- Place images in `src/assets/images/`
- Use relative paths for internal links
- Follow existing naming conventions (PascalCase for sections)

### Content Guidelines

- **Markdown Format**: Use standard Markdown syntax
- **Links**: Use relative paths for internal navigation
- **Images**: Optimize file sizes and use descriptive alt text
- **Dates**: Use consistent date formatting (YYYY MMM format)
- **Technology Tags**: Use code blocks for technology mentions

### Testing Changes

1. **Local Testing**:
   ```bash
   # Test Markdown to HTML conversion
   pandoc src/RESUME.md -o test.html --css=src/PDF.css
   
   # Test Jekyll build (if Jekyll is installed)
   jekyll build
   ```

2. **Validation**: Check that all links work and images display correctly

## 🚀 Deployment Process

Changes are automatically deployed when merged to the `main` branch:

1. GitHub Actions workflow builds the site
2. Converts Markdown to PDF using Pandoc  
3. Deploys to GitHub Pages
4. Makes PDF available for download

## 📝 Best Practices

### Commit Messages
- Use clear, descriptive commit messages
- Reference specific sections when making content updates
- Use conventional commit format when possible

### Content Quality
- Keep information current and accurate
- Use professional language and formatting
- Ensure all external links are valid
- Optimize images for web use

### Technical Considerations
- Test changes locally before committing
- Verify PDF generation works correctly
- Ensure responsive design is maintained
- Check for broken links and missing images

## 🔍 Code Review Process

1. **Self-Review**: Review your changes before submitting
2. **Testing**: Verify the build process completes successfully
3. **Documentation**: Update relevant documentation if needed

## 📚 Resources

- [Markdown Guide](https://www.markdownguide.org/)
- [Jekyll Documentation](https://jekyllrb.com/docs/)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [Pandoc Manual](https://pandoc.org/MANUAL.html)

## 🆘 Getting Help

If you encounter issues or have questions:

1. Check the existing [BEST_PRACTICES.md](BEST_PRACTICES.md) documentation
2. Review the GitHub Actions workflow logs for build errors
3. Create an issue describing the problem

## 📄 License

By contributing to this project, you agree that your contributions will be licensed under the MIT License.