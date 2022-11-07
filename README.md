# Astro Crash Course

Go to [Astro Docs](https://docs.astro.build/en/getting-started/) for detailed info.

Check out [Astro Github Action](https://github.com/marketplace/actions/astro-deploy): This action for Astro builds your Astro project for GitHub Pages. Also the last action on the Actions page is for Astro: Deploy an Astro site but it's not the 1st one.

## Project Structure

Inside of your Astro project, you'll see the following folders and files:

```
/
├── public/
├── src/
│   └── pages/
│       └── index.astro
└── package.json
```

Astro looks for `.astro` or `.md` files in the `src/pages/` directory. **Each page is exposed as a route based on its file name**.

There's nothing special about `src/components/`, but that's where we like to put any Astro/React/Vue/Svelte/Preact components.

Any static assets, like images, can be placed in the `public/` directory.

## Key Astro 'Terms'

| Term                | Use                                                        |
| :------------------ | :--------------------------------------------------------- |
| `*.astro`           | All production files must end with this extension          |
| `<slot />`          | A placeholder for HTML content (child elements)            |
| `Astro.props`       | Obj, contains values passed as component attributes:       |
| -                   | e.g., `Astro.props as ObjName`                             |
| `npm run astro add` | To add NPM packages, followed bu package name              |
| `()`                | Use instead of `{}` in `.map()` methods                    |
| `frontmatter`       | _See notes below_                                          |
| `Asto.glob()`       | A way to load many local files into your static site setup |
| `[].astro`          | Dynamic params in the filename                             |
| `getStaticPaths()`  | _See notes below_                                          |

1. `frontmatter`: all variables declared in a frontmatter fence (`---`) will be accessible via the `frontmatter` export

```js
---
title: 'My first MDX post'
publishDate: '21 September 2022'
---

# {frontmatter.title}
```

2. `getStaticPaths()`: returns an array of objects to determine which paths will be pre-rendered by Astro

## Usage

All commands are run from the root of the project, from a terminal:

| Command                   | Action                                             |
| :------------------------ | :------------------------------------------------- |
| `npm create astro@latest` | Create a project, follow it by your project name   |
| `npm install`             | Installs dependencies                              |
| `npm run dev`             | Starts local dev server at `localhost:3000`        |
| `npm run start`           | Same as above?                                     |
| `npm run build`           | Build your production site to `./dist/`            |
| `npm run preview`         | Preview your build locally, before deploying       |
| `npm run astro ...`       | Run CLI commands like `astro add`, `astro preview` |
| `npm run astro --help`    | Get help using the Astro CLI                       |

## Netlify

1. Click `Add new site`
1. Select `Import an existing project`
1. Under _Connect to Git provider_ select GitHub
1. Authorize Netlify - Choose all repos - Choose your repo
1. Under Basic build settings, in the Build cmd field type `npm run build`
1. Double-check the fields
1. Click Deploy site

> Double-check those notes the next time I deploy to Netlify

<!-- folder: Documents/WebDev/Traversy/astro-project -->
