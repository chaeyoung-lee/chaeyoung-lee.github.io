# Chae Young Lee

A simple, single-page academic website for GitHub Pages.

Edit `index.html` for the bio and the Awards, Publications, Talks, Teaching, and Service lists. Edit `style.css` for appearance. Publication images live in `assets/publications/`; their sources are recorded in `sources.json` there. The old page URLs redirect to matching sections on the homepage.

Preview with `python3 -m http.server 8000` from this folder. No build step is required.

After approval, publish to `chaeyoung-lee/chaeyoung-lee.github.io` and configure GitHub Pages to serve the `main` branch at `/ (root)`.

Papers, slides, and videos are stored locally in `papers/`, `slides/`, and `videos/`. The website uses relative links, so those resources do not depend on the Stanford server. `resource-manifest.json` records the original download URLs, sizes, and SHA-256 checksums for the migrated resources. Keep these folders in the GitHub repository when publishing.
