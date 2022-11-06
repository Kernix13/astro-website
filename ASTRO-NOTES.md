# First Astro Project

Video by Brad Traversy: [Astro Crash Course](https://youtu.be/Oi9z5gfIHJs), and [his repo](https://github.com/bradtraversy/astro-crash-course).

Go to [Astro Docs](https://docs.astro.build/en/getting-started/) for detailed info.

There is a basic Astro Action on the Actions tab. Compare that YAML file to [Astro Github Action](https://github.com/marketplace/actions/astro-deploy): 

> This action for Astro builds your Astro project for GitHub Pages. Also the last action on the Actions page is for Astro: Deploy an Astro site but it's not the 1st one.

## Intro

- Astro is for building static websites - it acts a lot like a static site generator
- Other popular SSGs: Gatsby (React), Jekyll, Hugo, Gridsome (Vue), Eleventy, and Pelican
- Astro integrates with frameworks like React or just use Astro components
- Basically, you structure your site with UI components 
- _Island Architecture_: a paradigm that aims to reduce the volume of JavaScript shipped through "islands" of interactivity that can be independent delivered on top of otherwise static HTML...are a component-based architecture that suggests a compartmentalized view of the page with static and dynamic islands
- Astro tries to get away from your entire page being loaded with JavaScript
- You can use Astro components only or combine with React, Vue, or Svelte omponents

## Setup

- Run `npm create astro@latest` - the wizard is horrible - how do you navigate the terminal
- Choose "Relaxed" for TypeScript, "yes" to git
- In `package.json` => `npm run dev` and `npm run start` will start the server 
- Other scripts: `npm run build` and `npm run preview`
- `astro.config.mjs`: can add React in here if you want to use that
- `tsconfig.json`: 
- `src/pages`: pages are components - when you add a page the route is automatically setup
- `src/pages/index.astro` is the home page
- `src/layouts` is where things like your nav goes - I don't have that folder nor do I have `src/components` folder
- Neither `npm run dev` or `npm run opend` a browser tab at `http://localhost:3000/`

## Building

- Add folders like components, layouts, images, posts, styles, etc
- You may have to install the Astro extension to handle `.astro` files

### Using JavaScript 

- All the HTML and Astro tags tags are dynamic, you can add JS expressions in them, e.g. `{users.map(user => <li>{user}</li>)}`
- You don't need a wrapper around your HTML elements but you could do `<></>`
- You can do conditionals `{abc && ...}` and ternarys
- To add JavaScript to the page, use markdown syntax of triple hyphens (---) at the very top of the file
- You can fetch data from an API: note, there is an `async` that is wrapped arounf your JS code block

### Layouts and components

- In the `Layouts` folder create `Layout.astro` - need to grab boilerplate from an HTML file because Emmet doesn't work
- To get a page in there use a slot: `<slot />`
- You need to import that component for all pages but you don't have to export it
- Then wrap the content with a `<Layout>` tag or whatever you named it

Pages and layouts are all components and you can pass `props` into them.

- There is a `title` in Layout but you will want to change that for different pages (SEO) 
- You can pass `{Astro.props.title}` into the title tag but instead add JS at the top of Layout and destructure `Astro.props` which is obviously an object that Astro provides
- Use a TypeScript `interface` which is like `propTypes` in React
- You can add a default value for a prop, e.g, `{title = 'Astro Website'}`

### Styles

- Create `global.css` - you can also use SASS out of the box
- You need to import it into the layout or component you want to use it in
- You can have multiple layout files

### Components

- Create `Header.astro` - you can import your components into a single page - but if you want a comp on every page add it to `Layout.astro`
- In `Layout.astro`, why add `<Header />` but `<slot />` for other things?
- Import `header.css` into Header, and import the logo
- For the nav links he mentions you can have the `href` as `name.html` or `/name` so lose .html - FYI just `"/"` for index.html

#### How to use a framework with Astro

- Go to [Astro Integrations](https://docs.astro.build/en/guides/integrations-guide/)
  - UI Frameworks: AlpineJS, Lit, Preact, React, SolidJS, Svelte, Vue
  - SSR Adapters: Cloudflare, Deno, Netlify, Node, Vercel
  - Others: icons, image, mdx, partytown, prefetch, sitemap, tailwind
- Click on React - there are 2 ways: 1) run a single command to install the dependencies you need (`astro add`), 2) manually
- `npm run astro add react` - that brings in `react`, `react-dom` and `@astro/react` and also brings it into `astro.config` in the `defineConfig()` function
- Create a React function them import it into `index.astro` - then you can bring in `useState` or any other hook

### Showcase

- create `components/Showcase.astro` - 
- Props for showcase: heading, text - use `interface` (ee notes at bootom for TypeScript interface)
- `heading` and `text` will have default values for this file, for other pages you would add the values into the component tag 

> - so from 35:00 he created `/components/Showcase.jsx` - SKIP - but 

### Features component

- For the cards he recommends creating an arrray of objects for the title and body and adding it in that way - that is how you might get data from an API - 
- I tried to do the `featuresData.map` myself and it did not work because after `=>` I used `{}` instead of `()` like with React

### Card component

- Cut the div for the card out of Features and add to `Card.astro` 
- First, implement 1 way for title and body, then refactor later 
- I would not have got this: `<Card title={feature.title} body={feature.body} />`
- Add a boolean for a dark theme to the card - 
- YOU HAVE TO REMEMBER THIS SYNTAX:

```ts
export interface Props {
  title: string;
  body: string;
}

const {title, body, dark = false} = Astro.props as Props;
```

> Something happened where my CSS was not updated. I even removed all the CSS from cards.css and features.css and the styles remained. CACHING?

### Page content component

- This will be the text on the index page so it goes into the `pages` folder 

> STOPPED HERE FOR COPYING NOTES TO ASTRO-NOTES.md

<!-- http://localhost:3000/ -->


- - - 

## Interfaces from TypeScript repo

Check the [interface docs](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#enums).

- like a custom type or a specific structure to an object 

```ts
interface UserInterface {
  id: number,
  name: string
}
const user: UserInterface = {
  id: 1,
  name: 'Jim'
}
```

- Use an `interface` over a `type` but there are differnces
- A `type` can be used with primitives and unions - you can use unions with an `interface` or with primitives, only objects
- For an obj interface, you may want some props to be optional, use `?`, and for Read-only props, add `readonly`:

```ts
interface UserInterface {
  readonly id: number,
  name: string,
  age?: number
}
```

- You can also use interfaces with functions:

```ts
interface MathFunc {
  (x: number, y: number): number
}
const add: MathFunc = (x: number, y: number): number => x + y;
const subtract: MathFunc = (x: number, y: number): number => x - y;
// why not this: const add: MathFunc = (x, y) => x + y;
```