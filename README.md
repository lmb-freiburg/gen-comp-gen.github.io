# gen-comp-gen.github.io

**What Drives Compositional Generalization in Visual Generative Models?**

This is the project website and blogpost for the research paper on compositional generalization in visual generative models.

## 🌐 Website

The site is deployed via GitHub Pages at: `https://lmb-freiburg.github.io/gen-comp-gen.github.io/`

## 📝 Customization

To customize the blogpost for your specific paper, edit `index.html` and update:

- **Author information**: Replace `[Author Names]` with actual author names
- **Publication date**: Replace `[Publication Date]` with the publication date
- **Links section**: Update the `#` placeholders with actual URLs for:
  - Paper PDF
  - Code repository
  - Video presentation
  - Full project page
- **Abstract**: Customize the abstract content
- **Figures**: Add images to visualize your work (store in `assets/images/`)
- **Citation**: Update the BibTeX citation with correct details
- **Contact email**: Replace `[email]` with contact information

## 🎨 Adding Images

1. Create an `assets/images/` directory
2. Add your figures/images there
3. Reference them in the HTML using relative paths

## 🛠️ Local Development

To preview the site locally:

```bash
# Using Jekyll (if installed)
bundle exec jekyll serve

# Or using Python's simple HTTP server
python3 -m http.server 8080
# Then visit http://localhost:8080/
```

## 📄 Structure

- `index.html` - Main blogpost page
- `_config.yml` - Jekyll configuration
- `.gitignore` - Files to ignore in git
- `README.md` - This file
