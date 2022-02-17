# Create a Next.js App

- Details to consider:
- Code has to be bundled using a bundler like webpack and transformed using a compiler like Babel
- need to do a production optimizations such as code splitting
- consider statically pre-render some pages for performance and SEO and use server-side rendering for client-side rendering
- might have to write soem server-side code to connect your React app to your data store.


### Next.js: The React Framework

- provides solution to all of the above problems.
- puts you and your team in the pit of success when building react applications.
- aims to have best-in-class developer experience and many built-in featues such as:
- intuitive page-based routing sytem (support for dynamic routes)
- pre-rendering, both static generation (SSG) and server-side rendering (SSR)
- auto code splitting for faster page loads
- client-side routing with optimized prefetching
- Built-in CSS and Sass support, and support for any CSS-in JS library
- API rountes to build API endpoints wiht Srverless Functions
- Fully extendable

### Setup

- install Node.js (or make sure it's installed and version 10.13 or later)
- to create a Next.js app, open your terminal, `cd` into the directory you'd like to create the app in, run the following command:
`npx create-next-app nextjs-blog --use-npm --example "https://github.com/vercel/next-learn/tree/master/basics/learn-starter"`

### Run the development server

- cd into the new directory `cd nextjs-blog`
- run the dev server: `npm run dev`
- this starts your development server  on port 3000.

### Editing the Page

- Make sure the Next.js dev server is still running.
- Open `pages/index.js` with your text editor
- find the text that says "Welcome to" under the `<h1></h1>` tag and change it to "Learn". Save the file.
- Next.js dev server has Fast refresh enabled, so auto applies changes made in the file almost instantly.
- Use `Ctrl + c` to stop the server.

## Assets, MetaData, and CSS

### Asssets

- Next.js can server Static assets, like images, under the top-level `public` directory.
- Files inside the `public` can be referenced from the root of the app similar to `pages`
- The `public` directory is also usefull for `robots.txt`, Google site Verification, and any other static assets.

### Unoptimized Image

- regular HTML, add your profile images:
<img src="/images/profile.jpg" alt="Your Name" />
- This means you have to manually handle:
- ensuring the image is reposonive on different screen sizes
- optimizing your images with third-party tool or library
- only loading images when they enter the veiwport
- Next.js provide an `Image` component out of the box to handle this for you.

### Using teh Image Component

- Next.js optimizes the images on-demand, as users request them.
- Images are lazy loaded by defualt, which means your page speed isn't penalized for images outside the viewport.
- Images are loaded as they are scrolled into viewport.
- Here's an example using `next/image` to display your profile picture.
- The height and width props should be the desired rendering size, with an aspect ration identical to the source image.
import Image from 'next/image'

const YourComponent = () => (
  <Image
    src="/images/profile.jpg" // Route of the image file
    height={144} // Desired size with correct aspect ratio
    width={144} // Desired size with correct aspect ratio
    alt="Your Name"
  />
)

### Metadata

- open `pages/index.js` in your editor and find the following lines:
<Head>
  <title>Create Next App</title>
  <link rel="icon" href="/favicon.ico" />
</Head>

- `<Head></Head>` is used instead of lowercase. This is a React component that is built into Next.js.
- `import Head from 'next/head`

### CSS Styling

- styled-jsx is a "CSS-in-JS" library and lets you write CSS within a React component, and the CSS styles will be scoped.
- Next.js has built-in support for styled-jsx, but you can also use other popular CSS-in-JS libaries such as styled-components or emotion.
- Next.js has built-in support for CSS and Sass which allows you to import `.css` and `.scss` files.
- Using Tailwind CSS libary is also supported.

### Layout Component

- create a Layout component which will be shared across all pages.
- create a top-level folder/director call `components`
- inside `components`, create a file called `layout.js` with the following content:
export default function Layout({ children }) {
  return <div>{children}</div>
}
- then import the `Layout` component into the `pages/post/first-post.js`: `import Layout from '../../components/layout`

### Adding CSS

- add styling to the Layout components by using CSS modules, which let you import CSS files in a React component
- create a file called `components/layout.module.css` with the following content:
.container {
  max-width: 36rem;
  padding: 0 1rem;
  margin: 3rem auto 6rem;
}
- to use CSS modules, the CSS file name must end with `.module.css`
- use the `container` class inside `components/layout.js` by import CSS file and assing a name to it, like `styles`
- use `styles.container` as the `className`
- Open `components/layout.js` and replace its content with the following:
import styles from './layout.module.css'

export default function Layout({ children }) {
  return <div className={styles.container}>{children}</div>
}

### Global Styles

- CSS modules are useful for component-level styles, but not if you want some CSS loaded with every page.
- To load global.CSS files, create a file called `pages/_app.js` with the following content:
export default function App({ Component, pageProps }) {
  return <Component {...pageProps} />
}
- The `App` component is the top-level component which will be common across all the different apges.
- Use `App` component to keep state when nagivating between pages.

### Adding Global CSS

- add global CSS files by importing them from `pages/_app.js`
- cannot import global CSS anywhere else.
- glboal CSS can't be import outside of `pages/_app.js` is that global CSS affects all elements on the page
- Create a top-level `styles` folder/directory and create `global.css` insdie
- add the following content to `styles/glboal.css`. It resets soem styles and change the color of the `a` tag:
html,
body {
  padding: 0;
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, Oxygen, Ubuntu,
    Cantarell, Fira Sans, Droid Sans, Helvetica Neue, sans-serif;
  line-height: 1.6;
  font-size: 18px;
}

* {
  box-sizing: border-box;
}

a {
  color: #0070f3;
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}

img {
  max-width: 100%;
  display: block;
}
- import this to `pages/_app.js`
import '../styles/global.css'

export default function App({ Component, pageProps }) {
  return <Component {...pageProps} />
}

# React Context

### What is React context?

- allows us to pass down and us (consume) data in whatever component we need in our react app without using props.
- React context allow us to share data(state) across our compoenents more easily

### When should you use React context?

- them data (like dar or light mode)
- User data (currently authenticated user)
- Location-specific data (like suer language or locale)
- Data should be placed on React context that does not need to be updated often.
- This of React context as the equivalent of global variable for our ReaCT components

### What problems does React context solve?

- helps avoid the problems of props drilling
- Props drilling is a term to describe when you passing props down multiple levels to a nested component, through components that don't need it.
- we can bypass using props entirely and therefore avoid the issue of props drilling.

### How do I use Reactd context?

- context is an API built into React, starting from React version 16.
- can use context directly by import React in any React project.
- There are 4 steps involed:

1. Create context using the `createContext` method.
2. Take your created context and wrap the context provider around your component tree.
3. Put any value you like on your context provider using the `value` prop.
4. Read that value within any component by using the context consumer.

### What is the useContext hook?

- Instead of using render props, we can pass the entire context object to React.
- useContext() to consume context at the top of our component.
- Benefit of the useContext hook is that it make our components more concise and allows us to creat our own custom hooks.

import React from 'react';

export const UserContext = React.createContext();

export default function App() {
  return (
    <UserContext.Provider value="Reed">
      <User />
    </UserContext.Provider>
  )
}

function User() {
  const value = React.useContext(UserContext);  
    
  return <h1>{value}</h1>;
}








