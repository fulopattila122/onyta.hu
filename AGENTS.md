# AGENTS.md

Instructions for AI coding agents working in this repository.

## What this is

A several-page static brochure website built with **Astro**. Output is plain HTML/CSS
deployed to Bunny CDN. There is no backend, no database, no CMS, and no runtime.

Keep it boring. This site should still be trivially editable in two years.

## Stack

- Astro (static output, `output: 'static'`)
- Plain CSS and Tailwind
- No UI framework. React, Vue, Svelte and Solid integrations must not be added.

## Structure

```
src/
  layouts/Base.astro     Single shared layout: <head>, header, footer
  components/            Small .astro partials (Nav, Footer, etc.)
  pages/                 One .astro file per route — these are the 4 pages
  styles/                Global CSS
public/                  Static assets copied verbatim (images, favicon, robots.txt)
```

- Every page in `src/pages/` **must** use `Base.astro` as its layout.
- Anything shared between two or more pages belongs in `components/`, not copy-pasted.
- Files in `public/` are served as-is at the root path. Do not import from there.

## Hard rules

1. **No or minimal client-side JavaScript.** No `client:*` directives, no `<script>` tags,
   no analytics snippets unless explicitly requested. The built pages ship zero JS.
2. **Do not create new top-level routes** without being asked. This is a several-page site.
3. **Do not add dependencies** without being asked. If a task seems to need one,
   say so and stop rather than installing it.
4. **Do not touch** `astro.config.mjs`, CI workflows, or deployment config unless
   the task is explicitly about them.
5. **No placeholder content.** Do not invent copy, addresses, phone numbers or
   fake testimonials. If real content is missing, leave a `TODO:` comment and ask.

## Conventions

- Components are `.astro` files in PascalCase (`Nav.astro`, `ContactForm.astro`).
- Page files are lowercase and kebab-cased (`about.astro`, `contact.astro`).
- Put page-specific metadata (title, description) in the page's frontmatter and
  pass it to `Base.astro` as props. Do not hardcode `<title>` per page.
- Use semantic HTML. Headings must nest correctly — one `<h1>` per page.
- Every `<img>` needs an `alt` attribute and explicit `width`/`height`.
- Keep CSS in global styles or in the component's own `<style>` block. Astro scopes
  component styles automatically — rely on that instead of BEM-style prefixes.

## Verifying changes

Before reporting a task as done:

```bash
npm run build     # must succeed with no errors
npm run preview   # sanity-check the built output
```

`npm run build` passing is the minimum bar. If you changed layout or navigation,
confirm all four pages still render.

## Deployment

Build output goes to `dist/`, which is uploaded to a Bunny Storage Zone and served
through a Pull Zone. Do not commit `dist/`. Do not add a deployment step to any
task unless asked.

## When in doubt

Ask. A short question is cheaper than a refactor. Prefer the smallest change that
satisfies the request, and do not opportunistically "improve" unrelated files.
