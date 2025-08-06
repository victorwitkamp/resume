# 📘 Project Best Practices

## 1. Project Purpose  
This project is a personal resume and portfolio site for Victor Witkamp. It is designed to showcase professional experience, certifications, and education, and is deployed as a static site using GitHub Pages with Jekyll. The site also provides a downloadable PDF version of the resume, generated automatically from Markdown sources.

## 2. Project Structure
- **Root Directory**: Contains configuration files for Jekyll, GitHub Actions workflows, and project metadata.
- **src/**: Contains all content files, including:
  - `RESUME.md`: Main resume in Markdown, includes links to education, certifications, and work experience.
  - `Education.md`, `Certifications.md`, `WorkExperience.md`: Sectional content in Markdown.
  - `PDF.css`: Stylesheet for PDF generation.
  - Image assets for certifications.
- **.github/workflows/**: Contains the `jekyll-gh-pages.yml` workflow for CI/CD, PDF generation, and deployment.
- **_config.yml**: Jekyll configuration, theme, and site metadata.

## 3. Test Strategy
- No automated code tests are present, as this is a static content and site generation project.
- Manual validation is performed by reviewing the generated site and PDF output after each change.
- GitHub Actions workflow ensures build and deploy steps complete successfully.

## 4. Code Style
- **Markdown**: Use clear, consistent heading levels and bullet points. Prefer semantic sectioning (e.g., `###` for job titles, `-` for lists).
- **CSS**: Minimal, focused on typography and link styling for PDF output.
- **YAML**: Use clear indentation and comments for configuration and workflow files.
- **Naming**: Use PascalCase for Markdown files, lowercase for assets and CSS.
- **Documentation**: Keep Markdown files well-commented and up to date.
- **Error Handling**: Ensure all referenced files (images, CSS) exist and are linked correctly.

## 5. Common Patterns
- Modular content: Each resume section is a separate Markdown file, included via links.
- Automated PDF generation: Uses Pandoc in CI to convert Markdown to PDF with custom CSS.
- GitHub Actions for CI/CD: Automates build, PDF generation, and deployment to GitHub Pages.
- Jekyll for static site generation and theming.

## 6. Do's and Don'ts
- ✅ Do keep all content modular and up to date in the `src/` directory.
- ✅ Do validate the site and PDF after changes.
- ✅ Do use clear, descriptive commit messages.
- ✅ Do keep configuration and workflow files well-commented.
- ❌ Don't hardcode file paths; use relative paths for portability.
- ❌ Don't add sensitive or personal data not intended for public view.
- ❌ Don't bypass the CI/CD workflow for deployment.

## 7. Tools & Dependencies
- **Jekyll**: Static site generator, configured via `_config.yml`.
- **GitHub Pages**: Hosting and deployment.
- **GitHub Actions**: Workflow for build, PDF generation (Pandoc), and deployment.
- **Pandoc**: Converts Markdown to PDF using custom CSS.
- **pages-themes/slate**: Jekyll theme for site styling.

## 8. Other Notes
- All resume content is in English.
- The workflow expects all referenced files (Markdown, images, CSS) to be present in `src/`.
- When adding new sections, update both the Markdown navigation and the workflow if needed.
- The project is optimized for clarity, maintainability, and ease of update for a personal portfolio/resume use case.
