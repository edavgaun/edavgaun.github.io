# edavgaun.github.io

Source for **https://edavgaun.github.io**: my data science portfolio and the RCEL 506 student showcase.

It is also meant as a reference for students building their own portfolio, so the structure is kept deliberately simple.

## How it's organized

```
_config.yml            ← name, photo, links (edit first)
_data/projects.yml     ← every project card on the home page
_data/showcase.yml     ← featured RCEL 506 student projects
index.html             ← home page layout (hero, work, teaching, showcase)
projects/*.md          ← one Markdown file per case study
_layouts/              ← page templates (default + project)
_includes/             ← reusable pieces (project card)
assets/css/style.css   ← all styling; colors are variables at the top
```

## Add a project in 3 steps

1. Add a block to `_data/projects.yml` (title, one-sentence summary, tags, metric, repo).
2. *(Optional)* Write a case study in `projects/your-project.md` using `layout: project`.
3. Commit to `main`. GitHub Pages rebuilds the site in about a minute.

## A good case study answers, in this order

1. What business question did you answer?
2. What is the headline result, as a number with context?
3. What does the data show? (one chart, titled with the finding)
4. Which model did you choose, and why?
5. What should the business do?
6. What are the limitations, and what would you do next?
7. How can someone reproduce it?

## Run locally (optional)

```bash
gem install bundler jekyll jekyll-seo-tag
jekyll serve
```
