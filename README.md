# edavgaun.github.io

Source for **https://edavgaun.github.io**, the portfolio of Dr. Edgar Avalos-Gauna (Rice University).

The site is also a reference for students building their own data science portfolio on GitHub Pages. Everything is plain Jekyll: no remote theme, no build tools. To add content, you edit a few YAML and Markdown files.

## How it's organized

```
_config.yml               ← name, role, bio, photo, social links
_data/projects.yml        ← every research card (papers, awards, links)
_data/teaching.yml        ← institutions, logos and courses for the Teaching tab
_data/showcase.yml        ← featured RCEL 506 student projects
index.html                ← home page: Research, Teaching and Showcase panels
projects/*.md             ← one Markdown file per case study (layout: project)
projects/micai-story.html ← self-contained interactive presentation
_layouts/default.html     ← sidebar (photo, bio, menu) + main content
_layouts/project.html     ← case study template (award, KPIs, buttons)
_includes/project-card.html ← the card used for every research item
assets/css/style.css      ← all styling; colors are variables at the top
assets/img/               ← profile photo, figures, institution logos
```

## Layout

- **Left sidebar (fixed):** photo, name, role, bio and the menu. Content comes from `_config.yml`.
- **Right side:** shows the panel selected in the menu: Research, Teaching or Student showcase.
- **Research tabs:** MICAI · IEOM · ASEM · ICMLA · Others. Each card appears in the tab named by its `group`.

## Add a paper

Add a block to `_data/projects.yml`:

```yaml
- title: Short, specific title
  summary: >-
    One or two sentences: the question, what was done, the main result.
  tags: [Method, Tool, Topic]
  metric: "Venue · year"                # shown above the title
  award: "1st place · Conference 2026"  # optional, shows a 🏆 badge
  image: /assets/img/folder/figure.png  # optional; add image_fit: cover for photos/networks
  page: /projects/my-paper/             # optional, link to a case study page
  links:                                # optional extra buttons
    - label: Paper
      url: https://doi.org/...
  featured: true
  group: micai                          # micai | ieom | asem | icmla | others
```

YAML is sensitive to indentation: every block must start with `- title:` at the very beginning of the line.

## Add a case study page

1. Create `projects/my-paper.md` starting with:
   ```yaml
   ---
   layout: project
   title: "Full paper title"
   award: "Award name"          # optional
   description: >-
     Two or three sentence summary shown under the title.
   tags: [Method, Tool]
   kpis:
     - value: "0.84"
       label: what the number means
   links:
     - label: Read the paper
       url: https://doi.org/...
   authors: "Author One (Institution) & Author Two (Institution)"
   venue: "Conference · Publisher"
   ---
   ```
2. Write the body in Markdown. A good case study answers, in this order:
   the question, the data, the main findings (one chart each), the implications, and the limitations.
3. Put its figures in `assets/img/<folder>/` and reference them with
   `![Alt text]({{ '/assets/img/<folder>/figure.png' | relative_url }})`.
4. Point the card to it with `page: /projects/my-paper/` in `_data/projects.yml`.

## Add a research tab

Add a button in `index.html`, inside `<div class="tabs">`:

```html
<button class="tab" data-filter="newgroup">New tab</button>
```

Then use `group: newgroup` in `_data/projects.yml`.

## Teaching

Each institution is one block in `_data/teaching.yml`:

```yaml
- name: Rice University
  logo: /assets/img/logos/rice.png
  role: Graduate Lecturer
  years: 2022 – present
  courses:
    - name: "RCEL 506 · Statistics & Data Science for Engineering Leadership"
      url: https://github.com/edavgaun/RCEL_506   # optional
```

Logos go in `assets/img/logos/` (PNG or SVG with a transparent background). If a logo file is missing, the row is still shown, just without it.

## Student showcase

Add selected RCEL 506 projects to `_data/showcase.yml` (only with the authors' permission):

```yaml
- term: Fall 2026
  title: Predicting ...
  team: [Name One, Name Two]
  summary: One sentence, problem → method → result.
  tags: [Regression, Hypothesis testing]
  repo: https://github.com/...
  site: https://student.github.io/...   # optional
```

## Publishing

Commit to `main`. GitHub Pages rebuilds the site in one or two minutes (see the **Actions** tab). If the change doesn't show up, open the site in a private window to skip the browser cache.

To preview locally (optional):

```bash
gem install jekyll jekyll-seo-tag
jekyll serve
```
