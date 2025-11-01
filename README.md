# What Drives Compositional Generalization in Visual Generative Models?

Static project page for the paper  
**“What Drives Compositional Generalization in Visual Generative Models?”** (Farid *et al.*, 2025).  
The live site is a single-page app built with plain HTML/CSS/JS and is intended for GitHub Pages hosting.

## Quick Start

- View online: enable GitHub Pages on the `main` branch (Settings → Pages → Source `main` / root).  
- Preview locally: run a lightweight HTTP server from the repo root and open the reported URL in your browser.

```bash
cd gen-comp-gen.github.io
python3 -m http.server 4000
# visit http://127.0.0.1:4000/
```

## Repo Layout

- `index.html` – main landing page with hero, findings, animated figures, tables, and BibTeX block.
- `figures/` – figure assets referenced by the page (PDF/PNG/SVG); see `.gitignore` for unused variants.
- `figs/teaser.jpg` – hero image shown in the header and social previews.
- `.gitignore` – ignores auxiliary figure exports that are not linked from the site.

## Editing the Site

1. Update copy or structure directly in `index.html`.  
2. Place new visual assets in `figures/` (or `figs/` for hero art) and reference them with relative URLs.  
3. If you add or remove assets, adjust `.gitignore` so only unused variants remain ignored.  
4. Commit and push; GitHub Pages will redeploy automatically after the push.

Animated figures use a tiny dependency-free script at the bottom of `index.html`. To add another carousel:

```html
<div id="fig-anim-xyz" class="anim-fig" data-dwell="1500">
  <!-- repeated .anim-step elements -->
</div>
<script>
  mountAnimFigure('fig-anim-xyz');
</script>
```

## Troubleshooting

- **Broken images**: ensure paths match the filenames (case-sensitive) and that the asset is not listed in `.gitignore`.  
- **PDF rendering issues**: export to PNG (same basename) if the browser cannot inline the PDF and update the `src`.  
- **No GitHub Pages output**: verify that Pages is enabled on the correct branch and that the build began in the Pages dashboard.

## TODO

- [ ] Add Orbis compositional videos with REAL, MaskGIT, and DiT (one video per novel composition) – Karim
- [ ] Add CelebA compostional split images - Karim
- [ ] Add CLEVRER videos (111 videos) - Rajat
- [ ] Fix language system prompt images - Rajat
- [x] Document the experimental setup underlying the probe accuracy results and clarify their interpretation on the site.
- [x] Restructure all sections that follow the JEPA section.
- [x] Add a qualitative results section sourced from Shapes3D.
- [ ] Add a world models section with quantitative and qualitative results – Karim
- [ ] Fix image sizes
- [ ] Proofread the full site copy.

For questions, contact the authors at `faridk@cs.uni-freiburg.de`.
