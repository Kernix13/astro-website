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

```
<!-- http://localhost:3000/ -->
```

- Run `npm create astro@latest` - the wizard is horrible - how do you navigate the terminal - could not change the folder name, ...
- Choose "Relaxed" for TypeScript, "yes" to git
- In `package.json` => `npm run dev` and `npm run start` will start the server 
- Other scripts: `npm run build` and `npm run preview`
- `astro.config.mjs`: can add React in here if you want to use that
- `tsconfig.json`: 
- `src/pages`: pages are components - when you add a page the route is automatically setup
- `src/pages/index.astro` is the home page
- `src/layouts` is where things like your nav goes - I don't have that folder nor do I have `src/components` folder
- Neither `npm run dev` or `npm run start` openeda browser tab at `http://localhost:3000/`

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
- `npm run astro add react` - that brings in `react`, `react-dom` and `@astrojs/react` and also brings it into `astro.config` in the `defineConfig()` function
- You will be prompted during the install, just answer "yes" - you could also just do `npm install react react-dom @astrojs/react` and then configure the config file manually adding to the integrations array:

```mjs
import react from '@astrojs/react";

export default defineConfig({
  integrations: [react()]
});
```

- Create a React function them import it into `index.astro` - then you can bring in `useState` or any other hook: 

```jsx
// Showcase.jsx
import { useState } from 'react';
function Showcase() {
  const [name, setName] = useState('Jim');
  return (
    <div>Hello {name}</div>;
  )
}
export default Showcase;

// index.astro
import Showcase from '../components/Showcase.jsx';

<Layout>
  <Showcase />
</Layout>
```

### Showcase

- create `components/Showcase.astro` - 
- Props for showcase: heading, text - use `interface` (ee notes at bootom for TypeScript interface)
- `heading` and `text` will have default values for this file, for other pages you would add the values into the component tag 

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

### Page content and Tabs component

- This will be the text on the index page  
- A Tab component with all the JS functionality for it in the file
- Pass in props for the headings and body so that it is a customizable and reusable Tab component
- Paste the HTML into `index.astro`, then create `Tabs.astro` and cut/paste the tabs HTML into that file thn import it into index
- Also grab the `page-content` CSS and put that in the global file so it is available for every page 
- Create `tabs.css` and add the CSS into there and import into Tabs
- For the JS, I got an error when I added it to the js hyphen code block at the top, but it worked in a `script` tag (???)

> Note: in React  you can't paste in vanilla JS and have it work, but it does in Astro

- Pass in variables to the `<script>` tag or pass it props - we want to pass in the color for the selected installer selected in the tabs as a prop
- Had to use `?` to make it optional or pass it into `<Tabs activeTextColor="#A741FF" />` to prevent a file error - but that is what you would do with any other page with tabs

> THIS IS THE MODERN WAY TO BUILD STATIC SITES! THAT EXAMPLE...

Now he wants to make the content props in case you have other tabs on other pages 

- see code

### Footer component

- Create `Footer.astro` - then bring it into Layout because it needs to be on every page and import the CSS - DONE!

## About page

- Create `pages/about.astro` and paste in the HTML
- Import LAyout and wrap the HTML - also import the 2 images
- There is a card in the HTML but he wants to wrap it in a Card class insted of have a tite and body prop
- Go into Card and remove those Props and he changed the markup:

```jsx
<div class="card">
  <h3>{title}</h3>
  <p>{body}</p>
</div>

<div class="card">
  <slot />
</div>
```

- He never explained what `slot` is and when to use it, though he said the slot is whatever you surround
- See the code but he had to make the change in Features also:

```jsx
{featuresData.map(feature => (
  <Card title={feature.title} body={feature.body} />
))}
// to
{featuresData.map(feature => (
  <Card>
    <h3>{feature.title}</h3>
    <p>{feature.body}</p>
  </Card>
))}
```

- It's up to you - if your cards will only ever have a heading and a title, you could leave it how it was - or add other props

## Blog page

- It's a markdown blog - main page will have excerpts with links to fulle post
- He is going to fetch them from `jsonplaceholder` - fetch example

```js
const response = await fetch('https://jsonplaceholder.typicode.com/posts/?_limit=5');

const posts = await response.json();
```

```jsx
{posts.map(post => (
  <Card>
    <h3>{post.title}</h3>
    <p>{post.body}</p>
  </Card>
))}
```

### Markdown

- Create `posts/astro-1-0.md` though he wants to use the post titles as a slug
- "`frontmatter`" => like database fields - put that stuff in triple hyphens like the JS and it is basically an object
- Use `Asto.glob()` - see code but anytime you add a new .md post to that folder, it will output onto the page
- The link to the post is the slug - how to do that is similar to Next.js or Nuxt.js

### Slug

- `[field_the_url_is_connected_to].astro`, or `[slug].astro`
-  In Next.js when you need to create paths, you use a function called `getStaticPaths()` - Astro also has that function
- return from it an object that has an array of params - with the fields that we want to use for the URLs
- The following code is not something I've ever done or would have thought of!
- Now you can get your posts and frontmatter thru props

> Getting complicated...se rest of code

## Deploy on Netlify

- Use `npm run build` - that will create a `dist` folder which will have all the static files you need
- Look at `dist/index.html` - the only JS in it is the code for the Tabs in a script tag - _Island Architecture_: No other script tags, HTML (water) with JS islands
- He says you can deploy your entire project to GitHub then push it to Netlify, then Netlify will host the dist folder
- You don't need to push the dist folder, Netlify will build it for you
- If you add a new markdown post, just push to GitHub and Netlify will handle the rest

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