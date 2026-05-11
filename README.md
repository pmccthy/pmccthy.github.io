# Academic Website with Jekyll

This is a clean, minimal academic website built with Jekyll and hosted on GitHub Pages at https://pmccthy.github.io

## Quick Start

### Prerequisites

- Ruby 2.5.0 or later
- Jekyll and Bundler

### Local Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/pmccthy/pmccthy.github.io.git
   cd pmccthy.github.io
   ```

2. **Install dependencies:**
   ```bash
   bundle install
   ```

3. **Run the site locally:**
   ```bash
   bundle exec jekyll serve
   ```

4. **Open in browser:**
   Navigate to `http://localhost:4000` to see your site

### Editing Content

All pages are written in Markdown. Here's where to find each section:

- **Home Page:** `index.md`
- **About:** `about.md`
- **Projects:** `projects.md`
- **Publications:** `publications.md`
- **Contact:** `contact.md`
- **Blog:** `blog.md` and `_posts/` directory

To add a new blog post:
1. Create a new file in `_posts/` with the format: `YYYY-MM-DD-title-slug.md`
2. Add frontmatter at the top (see existing posts for examples)
3. Write content in Markdown

### Customization

#### Change Site Title/Email
Edit `_config.yml`:
- `title:` — Your name
- `email:` — Your email
- `description:` — Site tagline

#### Change Colors
Edit `assets/css/style.scss` and modify these variables:
- `$brand-color:` — Main accent color
- `$text-color:` — Text color
- `$background-color:` — Background color

#### Change Navigation Links
Edit `_config.yml` under `header_pages:` to reorder or add/remove navigation items.

## Deployment to GitHub Pages

Once you have the site working locally:

1. **Commit and push to GitHub:**
   ```bash
   git add .
   git commit -m "Initial website setup"
   git push -u origin main
   ```

2. **Enable GitHub Pages:**
   - Go to your repository settings
   - Scroll to "GitHub Pages"
   - Select "Deploy from a branch"
   - Choose `main` branch and `/root` directory
   - Save

3. **Wait for deployment:**
   - GitHub will build and deploy your site automatically
   - Check the "Actions" tab to see the build status
   - Once complete, your site will be live at `https://pmccthy.github.io`

## File Structure

```
.
├── _config.yml          # Site configuration
├── _posts/              # Blog posts
├── assets/
│   └── css/
│       └── style.scss   # Custom styling
├── index.md             # Home page
├── about.md             # About page
├── projects.md          # Projects page
├── publications.md      # Publications page
├── contact.md           # Contact page
├── blog.md              # Blog listing page
├── Gemfile              # Ruby dependencies
└── README.md            # This file
```

## Theme Information

This site uses the **Minima** Jekyll theme with custom CSS overrides for a clean, academic aesthetic.

### Key Design Features

- **Minimal aesthetic** — Clean white background with selective use of color
- **Responsive design** — Works on mobile, tablet, and desktop
- **Fast loading** — Simple HTML/CSS, no unnecessary JavaScript
- **Dark theme option** — Can be toggled in `_config.yml`
- **Built-in SEO** — Jekyll SEO Tag plugin included

## Tips for a Great Academic Website

1. **Keep it updated** — Regularly add blog posts and project updates
2. **Be clear and concise** — Use short paragraphs and clear headings
3. **Add visuals** — Include diagrams, charts, or screenshots in posts
4. **Link to your work** — Add links to papers, code repositories, and external profiles
5. **Professional tone** — Maintain a professional but personable voice

## Troubleshooting

### Site not building locally?
- Make sure you have Ruby 2.5.0+: `ruby --version`
- Try: `bundle update` then `bundle exec jekyll serve`

### GitHub Pages not updating?
- Check the "Actions" tab for build errors
- Make sure `.gitignore` is correct (Gemfile.lock should be ignored)
- Wait a few minutes—deployment can take time

### Styling looks different locally vs. GitHub?
- GitHub Pages uses Jekyll 3.9.0; make sure your local version matches
- Clear Jekyll cache: `bundle exec jekyll clean`

## Further Customization

For more advanced customization, refer to:
- [Jekyll Documentation](https://jekyllrb.com/)
- [Minima Theme Documentation](https://github.com/jekyll/minima)
- [GitHub Pages Help](https://docs.github.com/en/pages)

## License

This website is yours to customize and use freely!

---

**Happy blogging!** 🎓
