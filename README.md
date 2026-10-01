# UNLV Percussion — Static Site

A plain HTML/CSS rebuild of unlvpercussion.com. No frameworks, no npm, no build
step — every page is hand-written HTML that links a single shared stylesheet.

## File layout

```
/
├── index.html                 Home (/)
├── about-1/index.html         About (/about-1/)
├── ensembles/index.html       Ensembles (/ensembles/)
├── media/index.html           Media (/media/)
├── services-2/index.html      Resources (/services-2/)
├── undergrad-resources/index.html   Undergraduate Resources
├── graduate-resources/index.html    Graduate Resources
├── contact/index.html         Contact (/contact/)
├── 404.html                   Not-found page
├── styles.css                 Shared stylesheet for every page
├── nav.js                     Mobile menu / dropdown toggle (vanilla JS)
├── images/                    All site images (faculty photos, ensemble
│                               photos, gallery photos, icons, logo)
└── README.md                  This file
```

Each page folder keeps the original Wix URL structure, so a page lives at
`/<folder>/` (served as `<folder>/index.html`) rather than `/<folder>.html`.
The home page is the one exception, living at the site root as `index.html`.

All links and image paths are **relative** (`../images/x.jpg`,
`../contact/`), so the whole folder can be moved, zipped, or served from any
sub-path without edits.

## Editing a page

1. Open the page's `index.html` (e.g. `about-1/index.html` for the About
   page).
2. Each page is built from a repeated section pattern:
   ```html
   <section class="block block-dark">
     <div class="block-inner">
       <p class="eyebrow">KICKER TEXT</p>
       <h2>Headline</h2>
       <p class="subtext">Supporting copy.</p>
       <div class="btn-wrap">
         <a href="..." class="btn">Button Label</a>
       </div>
     </div>
   </section>
   ```
   Edit the text inside the tags directly — no templating, no build step.
   `block-dark` gives a black section, `block-light` gives a white one.
3. The header/nav and footer markup is duplicated at the top/bottom of every
   page (there's no includes mechanism without a build step). If you change
   the nav or footer, update it in **every** `index.html` file, or run a
   find-and-replace across the project.
4. Images live in `/images/`. Add a new file there and reference it with a
   relative path such as `../images/new-photo.jpg` (one `../` per folder
   level the page sits below the root).
5. Styling lives entirely in `/styles.css`. Shared rules (buttons, section
   blocks, header, footer) are near the top; page-specific rules (faculty
   grid, ensemble rows, media gallery) are grouped by page further down.
6. Videos on the Media page are plain `<iframe>` embeds pointed at
   `youtube.com/embed/<id>` or `player.vimeo.com/video/<id>` — swap the ID to
   change a video.

## Previewing locally

From this folder:

```
python3 -m http.server 8000
```

Then open `http://localhost:8000/` in a browser. Because every page lives in
its own folder with an `index.html`, links like `/about-1/` resolve correctly
without any server configuration.
