# Abdullah Fareed — Personal Portfolio

A premium, single-page personal portfolio built with **plain HTML, CSS and JavaScript**.
No frameworks, no build step, no dependencies. Open `index.html` and it runs.

The site presents a learning journey honestly: what is being learned, what has been
built, and what is still a concept — with nothing invented.

---

## Quick start

**Option 1 — open directly**

Double-click `index.html`. Everything works from the local file system.

**Option 2 — local server** (recommended, and required for clipboard features on some browsers)

```bash
# any static server works, for example:
npx http-server . -p 8137
# then open http://localhost:8137
```

**Deploying:** push the folder to GitHub and enable GitHub Pages (Settings → Pages →
deploy from `main` / root). No configuration needed.

---

## Make it yours — edit one file

Almost everything personal lives in **`assets/js/config.js`**:

```js
window.PORTFOLIO_CONFIG = {
  name: "Abdullah Fareed",
  initials: "AF",
  tagline: "Student · Learning Generative AI, Prompt Engineering & Web Development",
  email: "abdullahfareed138@gmail.com",
  links: {
    github:   "",   // paste a full https:// URL to show the link
    linkedin: "",   // left empty → shows "Link not configured yet"
    website:  "",
  },
  formEndpoint: "", // paste a form service URL to enable real submissions
};
```

- **Name / initials / tagline** update everywhere automatically (`data-config` hooks).
- **Social links** are hidden with an honest "not configured" state until you add a URL.
- **Contact form** — see below.

### Enabling the contact form properly

Out of the box there is **no backend**, so the form does not pretend to send anything.
It validates your input, then honestly tells the visitor that nothing was sent and
opens their email app with the message pre-filled as a draft.

To enable real submissions, create a form endpoint (e.g. [Formspree](https://formspree.io),
or your own server) and set:

```js
formEndpoint: "https://formspree.io/f/your-id",
```

The form then `POST`s JSON (`name`, `email`, `subject`, `message`) and shows a real
success or error state based on the actual response.

> **Never** put API keys or secrets in `config.js` — it is public. Only use endpoint
> URLs that are safe to expose.

---

## Project structure

```
.
├── index.html                  ← all page content and structure
├── assets/
│   ├── css/
│   │   ├── tokens.css          ← design tokens (colour, type, spacing, motion)
│   │   ├── base.css            ← reset, typography, layout helpers, reveals
│   │   ├── components.css      ← nav, buttons, cards, forms, modal, toast
│   │   ├── sections.css        ← per-section layout (hero, lab, projects…)
│   │   └── animations.css      ← ambient layers and advanced motion
│   └── js/
│       ├── config.js           ← EDIT THIS: name, email, links
│       ├── main.js             ← config binding, nav, reveals, toast, clipboard
│       ├── motion.js           ← preloader, particles, cursor, spotlight, tilt
│       ├── promptlab.js        ← Prompt Lab (builder, templates, stepper, checklist)
│       ├── projects.js         ← project data, filters, case-study modal
│       └── contact.js          ← links + form validation and submission
└── README.md
```

The CSS is deliberately layered so you can change one concern without touching the
others. All colour decisions flow from `tokens.css`.

---

## Editing content

| What | Where |
|---|---|
| Name, email, links | `assets/js/config.js` |
| Hero, About, Skills, Journey, Contact copy | `index.html` (search for the section id) |
| Projects (titles, status, case studies) | `assets/js/projects.js` → the `PROJECTS` array |
| Prompt templates | `assets/js/promptlab.js` → the `TEMPLATES` array |
| Workflow steps | `assets/js/promptlab.js` → the `STEPS` array |
| Evaluation checklist | `assets/js/promptlab.js` → the `CHECKS` array |

### Project status labels

Each project carries a `status` of `"concept"`, `"progress"` or `"built"`, which renders
the matching badge. Keep these accurate — the whole point of the site is that the labels
mean something.

To add a repository or live demo link to a project, set its `repo` / `demo` field to a
URL string. Leaving them `null` shows the honest "no public repository yet" note instead.

---

## The Prompt Lab

The signature section. Everything runs **locally in the browser** — no AI API is called.

- **Basic vs. engineered prompt** — compare the two, and select a technique chip to
  highlight where it appears in the structured prompt.
- **Prompt builder** — fill in seven parts and assemble a structured prompt. Copy it
  into any AI tool. Handles empty fields gracefully and never invents content.
- **Templates library** — six realistic templates (web dev, AI agents, marketing,
  research, content, learning). Copy or load straight into the builder.
- **Workflow stepper** — the seven-step process, distinguishing *writing* a prompt
  (steps 1–5) from *evaluating* its output (steps 6–7).
- **Evaluation checklist** — seven checks with a progress meter.

---

## Design system

- **Palette:** pure black surfaces (`#000` → `#1b1b1e`), grey text (`#f4f4f5` → `#7c7c84`),
  chrome/platinum accent for primary actions. Desaturated success/warning/danger only
  where meaning requires it.
- **Type:** Inter (with a system-font fallback), fluid `clamp()` scales, JetBrains Mono
  for code and prompts.
- **Motion:** preloader, mouse-reactive particle canvas, custom cursor, spotlight,
  grain texture, scroll progress, magnetic buttons, 3D card tilt, scroll reveals.

### Accessibility

- **Reduced motion:** every decorative animation (particles, cursor, spotlight, grain,
  preloader, tilts, reveals) is disabled under `prefers-reduced-motion: reduce`.
- **Keyboard:** skip link, visible focus rings, focus management on navigation and in
  the modal, Escape closes menus and the dialog.
- **Content-first:** text is visible by default; the hidden "reveal" start-state only
  applies when JavaScript is running, so the page is fully readable if scripts fail.
- **Honest semantics:** labelled form controls, `aria-live` regions for status messages,
  ARIA-labelled tabs, and `dialog` for case studies.

Audited with Lighthouse: **Accessibility 1.0, Best Practices 1.0, SEO 1.0**.

### Responsive

Breakpoints at `56rem` (navigation collapses to a mobile menu), `60–62rem` (two-column
sections stack), and `40rem` (spacing tightens). The workflow stepper is horizontal on
desktop and becomes a vertical timeline on mobile. The builder preview is sticky on
desktop and static on mobile.

---

## Honesty rules this site follows

These are intentional, so please keep them intact when editing:

- No invented employment, clients, testimonials, certifications, grades, dates or metrics.
- Concepts are labelled **Concept**, and only real, working things are labelled **Built**.
- Planned features are listed separately from implemented ones.
- Skills carry no fake ratings — unfinished areas say so.
- The contact form never claims to have sent a message without a real service.
- Case studies show no mock-ups pretending to be real screenshots.

---

## License

Personal project — content and identity belong to Abdullah Fareed. Code is free to
learn from.
