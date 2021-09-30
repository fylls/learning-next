## Pages & Routes

inside this pages folder is where we create all of our page components so each page in next is driven by a react component so for an about page we'd have an about component for a contact page we'd have a contact component etc and each page component has its own file inside the pages folder so the file name and location of each page component is tied to the route for that particular page for example if i create a new file inside this called about.js then next we'll automatically create a route forward slash about which is the name of the file to serve up this components so we create a react component for this page inside this file so the route name is tied to the file name if i created one called contact.js then next would create a route forward slash contact for that component so this all happens automatically under the hood and there is one exception to the rule this thing right here index dot js now next doesn't create a route forward slash index for this which is the file name it just creates the route forward slash so all we have to do is go to the root of the domain to see this component right here so that's the one exception to the rule

sfc stateless functional components

if i was to create a new folder called ninjas for example i could create page components inside here and let's do one called test.js and we'll create a stateless functional component for this called test and then inside here i'm


we have a subfolder then next we'll create a route based on that subfolder as well so it would be in this case forward slash ninjas then forward slash whatever the file is called so i could go to forward slash ninjas right here forward slash test and that would be the route for this component

now again if we create one called index.js here and i'm going to boilerplate this component as well i'm going to call this ninjas because this will ultimately be the page that lists the ninjas and inside here i'm going to do a div and inside that an h1 that says all ninjas oops let me just make this h1 first all ninjas like so so the route for this will just be forward slash ninjas not then forward slash index just forward slash ninjas forward slash much like index over here when we have a file named index it creates a root path for that file so if we go to forward slash ninjas now it will serve up this component

---

## Adding Components

so just like in regular react applications in next you can have dropping components that are not page components so things like a navbar component or a contact form component which we can then reuse in multiple different page components if we need to

create components outside pages


a tags don't need anchor tags hef

and the reason for that is because later on when we start to work with linking between pages we don't have the href on the anchor tag we use something else

`nav.js`

```javascript
const Navbar = () => {
  return (
    <nav>
      <div className="logo">
        <h1>Ninja List</h1>
      </div>
      <a>Home</a>
      <a>About</a>
      <a>Ninja Listing</a>
    </nav>
);
}
export default Navbar;
```

`footer.js`

```javascript
const Footer = () => {
  return (
    <footer>
      Copyright 2021 Ninja List
    </footer>
  );
}
 
export default Footer;
```

hat's how simple it is to create other react components that are not page components but instead are dropped in to page components and that can be reused we could reuse those components in multiple different page components if we wanted to and remember we don't create those reusable dropping components inside the pages folder we create them in a separate folder somewhere else in the project structure i'


```javascript
import Head from 'next/head'
import Footer from '../comps/Footer'
import Navbar from '../comps/Navbar'
import styles from '../styles/Home.module.css'

export default function Home() {
  return (
    <div>
      <Navbar />
      <h1>Homepage</h1>
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Minus animi impedit suscipit tempore iure accusamus, dolorem nobis odit.</p>
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Minus animi impedit suscipit tempore iure accusamus, dolorem nobis odit.</p>
      <Footer />
    </div>
  )
}
```

---

## Linking Between Pages

the link component adds the ability to do client-side navigation in the browser meaning that different pages are loaded in via javascript and not new html page requests to the server so it results in a much quicker website experience when going between pages

```javascript

import Link from 'next/link';

const Navbar = () => {
  return (
    <nav>
      <div className="logo">
        <h1>Ninja List</h1>
      </div>
      <Link href="/"><a>Home</a></Link>
      <Link href="/about"><a>About</a></Link>
      <Link href="/ninjas/"><a>Ninja Listing</a></Link>
    </nav>
);
}
 
export default Navbar;
```
okay so now if i go to a different page like about notice over here we get about.js so that's the javascript bundle that controls the page for about okay so it only serves that after we go to the about page so it code splits and that means initially we only served the javascript code that we need for the initial request and when we navigate around we get served the javascript for that page now if we go to that page again it doesn't reserve it there's no reason to do that we still have that one that it sent us initially when we first went to this page but if we go to another page like ninja listing we're going to get ninjas.js all right so each page has its own javascript bundle which controls that page and it only gets served to us once we navigate to that page for the first time now when you build your next app for production next is also going to prefetch any code in the background that might be needed when the user clicks on a link from another page and it does this by looking at all of the link components like these things right here on the current page and it pre-fetches the code for any of those pages that those links navigate to so when a user clicks one the code for that page is ready and waiting so all in all it makes for a very very quick user experience

---

## "Layout" Component

I want to have `nav` and `footer` on every page, it does does makes sense to hardcode it for every page

---

`app.js`

**before**

```javascript
import '../styles/globals.css'

function MyApp({ Component, pageProps }) {
  return <Component {...pageProps} />
}

export default MyApp
```

**after**

```javascript
import Layout from '../comps/Layout'
import '../styles/globals.css'

function MyApp({ Component, pageProps }) {
  return (
    <Layout>
      <Component {...pageProps} />
    </Layout>
  )
}

export default MyApp
```

---

`layout.js`

```javascript
import Footer from "./Footer"
import Navbar from "./Navbar"

const Layout = ({ children }) => {
  return (
    <div className="content">
      <Navbar />
      { children }
      <Footer />
    </div>
  );
}
 
export default Layout;
```

---

## Styles

globals CSS in `/styles/globals.css` 

page-specific styles? (CSS modules)
no conflicts between classes in different components

in css modules you ca only write classes (no ID or HTML elements)

example: `/styles/home.module.css`


```javascript
import Head from 'next/head'
import Link from 'next/link'
import styles from '../styles/Home.module.css'

export default function Home() {
  return (
    <div>
      <h1 className={styles.title}>Homepage</h1>
      <p className={styles.text}>Lorem ipsum dolor sit amet consectetur adipisicing elit. Minus animi impedit suscipit architecto, odio inventore nostrum non neque dicta. Quam magni accusantium culpa distinctio tempore iure accusamus, dolorem nobis odit.</p>
      <p className={styles.text}>Lorem ipsum dolor sit amet consectetur adipisicing elit. Minus animi impedit suscipit architecto, odio inventore nostrum non neque dicta. Quam magni accusantium culpa distinctio tempore iure accusamus, dolorem nobis odit.</p>
      <Link href="/ninjas/">
        <a className={styles.btn}>See Ninja Listing</a>
      </Link>
    </div>
  )
}
```

---

## 404 Page

already built inj in next but you can customize it

`404.js` special name just like `index.js`

like a fallback if the link typed by the user is wrong

```javascript

import Link from 'next/link'

const NotFound = () => {
  return (
    <div className="not-found">
      <h1>Ooops...</h1>
      <h2>That page cannot be found :(</h2>
      <p>Go back to the <Link href="/"><a>Homepage</a></Link></p>
    </div>
  );
}
 
export default NotFound;
```

---

## Redirecting User

if the user stays in the 404 for more than 3 seconds he will be automatically redirected to the homepage


```javascript

import Link from 'next/link'
import { useEffect } from 'react'
import { useRouter } from 'next/router'

const NotFound = () => {
  const router = useRouter()

// firers only one when components first mounts ([ ])
  useEffect(() => {
    setTimeout(() => {
      // router.go(-1)
      // router.go(1)
      router.push('/')
    }, 3000)
  }, [])

  return (
    <div className="not-found">
      <h1>Ooops...</h1>
      <h2>That page cannot be found :(</h2>
      <p>Going back to the <Link href="/"><a>Homepage</a></Link> is 3 seconds...</p>
    </div>
  );
}
 
export default NotFound;
```

---

## Handling Images

static assets, everything in public folder is made accessible to the browser

`Image` component already implemented in NetJS


```javascript
import Link from 'next/link'
import Image from 'next/image'

const Navbar = () => {
  return (
    <nav>
      <div className="logo">
        <Image src="/logo.png" alt="site logo" width={128} height={77} />
      </div>
      <Link href="/"><a>Home</a></Link>
      <Link href="/about"><a>About</a></Link>
      <Link href="/ninjas/"><a>Ninja Listing</a></Link>
    </nav>
  );
}
 
export default Navbar;
```

image component must use width and height properties so it forces us to add these properties to images and it also automatically makes the image responsive based on these properties we give it 

---

## Metadata

another good thing about using this image component instead of the standard html one is that it automatically lazily loads in the image so if the image was somewhere down below this window right here and we had to scroll down to it it's only going to load in the image when we scroll to that point and we need to see it on the web page so it optimizes this for loading speeds if you like okay cool so that is the image component the other thing i want to talk about in this video is metadata so sometimes you might want to add in a custom title in the head for each page and remember the title inside the head is the thing that shows right here so i might want it to say home page ninja list or ninja list home page rather if we go to about it should say ninja list about instead of this url in the tab instead so we can do that but also we can add metadata as well how do we do this though because all that stuff goes inside the head of an html document if we open this up and go inside the head this is where it goes and we don't really do anything that goes inside the head right here do we well what we could use is the head component that's built in to next so if i open a page and i'm going to go to the home page


all we need to do is use that component down here and then we can place any title or metadata inside it and what next we'll do is take that and insert it into the head of our documents

fragment since we cannot have 2 returned tags in react at the same time

```javascript
import Head from 'next/head'
import Link from 'next/link'
import styles from '../styles/Home.module.css'

export default function Home() {
  return (
    <>
      <Head>
        <title>Ninja List | Home</title>
        <meta name="keywords" content="ninjas"/>
      </Head>
      <div>
        <h1 className={styles.title}>Homepage</h1>
        <p className={styles.text}>Lorem ipsum dolor sit amet consectetur adipisicing elit. Minus animi impedit suscipit architecto, dolorem nobis odit.</p>
        <p className={styles.text}>Lorem ipsum dolor sit amet consectetur adipisicing elit. Minus animi impedit suscipit architecto, dolorem nobis odit.</p>
        <Link href="/ninjas/">
          <a className={styles.btn}>See Ninja Listing</a>
        </Link>
      </div>
    </>
  )
}
```

---


## Fetching Data (getStaticProps)

in normal react applications we might do this from a hook like use effect and that would make the request in the browser but in our case we don't want to do that because remember the components are all pre-rendered by the time they reach the browser so ideally we want to fetch the data before they're rendered so the rendered components have data in the template and to do this we can use a special function provided to us by next

this function right here runs at build time as our app is built and our components rendered at this point we can add a fetch request inside it to fetch any data we need for our component template now this function never runs in the browser only at build time so don't write any code here that you expect to run in the browser


```javascript
import styles from '../../styles/Jobs.module.css'

export const getStaticProps = async () => {
  const res = await fetch('https://jsonplaceholder.typicode.com/users');
  const data = await res.json();
  return { props: { ninjas: data }}
}

const Ninjas = ({ ninjas }) => {
  console.log(ninjas)

  return (
    <div>
      <h1>All Ninjas</h1>
      {ninjas.map(ninja => (
        <div key={ninja.id}>
          <a className={styles.single}>
            <h3>{ ninja.name }</h3>
          </a>
        </div>
      ))}
    </div>
  );
}
 
export default Ninjas;
```

---

## Dynamic Routes

`/ninjas/:id`

once we've completed developing our application next is going to generate a static site for us based on all of our page components and it's at this point that next renders all of our page components into html files and javascript bundles that go with them for any interactivity on those pages so now we have a load of pages ready to deploy to the web a static site containing just these html pages and javascript so it's going to generate in our case at the minute an index homepage and about page and also the ninjas homepage as well so when it comes to building our ninja details pages it's going to need to generate an html file for each item of data that we have in our case that will be 10 different pages which is how many items we get back from the api endpoint that we're using so it could be this one for forward slash ninjas forward slash one this for forward slash ninjas forward slash two etc and we'd have all of these for each one of our items from the data now the template and the component that we use will be the same for each one of these pages so we don't need to make multiple components for them but next still needs to pre-render a separate page for every single ninja and assign each one its own route so we'll see that in action later on but first of all let's create the ninja details components that these pages are going to be based on 


`[id].js` tells NextJS that this first part is changeable



with square brackets id and that's us saying that this id part the route is changeable it's a route parameter and that means that there will be a ninja details page for each different ninja id that we have so ultimately when we build our app for production next needs to be able to generate a route and an html page for each of these ninjas for example in our case it should create 10 html pages for each of our 12 ninjas that we're listing or each of our 10 ninjas rather right here and assign each one to a specific route based on its id but next doesn't automatically know what routes and html pages to generate because that depends on external data for example if i was to build this app it wouldn't automatically know to create 10 routes and 10 html pages for our ninja detail pages and that's because it doesn't know what's in our data when it's building the application that's being stored somewhere else on the internet and it's only after we fetch the data that we have a list of 10 ninjas so we need a way to explicitly tell next what ninja details routes and pages we need to create at build time based on our data and to do this we use a function called get static paths 

get static paths and this is another function that's going to run at build time and inside it we return all the possible values for our route parameter the id right here for this component and then next we'll know to generate a route and html page for each of those ids

paths property needs to be an array of objects where each object represents a route if you like and in each of those objects we need to specify any route parameters in our case the id so it will look something like this where we have a load of different objects where each one represents a route and then in each object there would be a params property which specifies any parameters of this particular route and inside there any route parameters so in our case the id which would be the id of each item inside this data so we need to somehow formulate this array like this from this thing

```javascript
export const getStaticPaths = async () => {
  const res = await fetch('https://jsonplaceholder.typicode.com/users');
  const data = await res.json();

  // map data to an array of path objects with params (id)
  const paths = data.map(ninja => {
    return { params: { id: ninja.id.toString() }}
  })

  return {
    paths,
    fallback: false
  }
}

const Details = () => {
  return (
    <div>
      <h1>Details Page</h1>
    </div>
  );
}

export default Details;
```

---

## Fetching a Single Item

we're running this function 10 times because we have 10 items inside this array right here and each time we get a different id from the context object and so we can make a fetch request for each id below that so i'm going to say const response is equal to fetch and we're going to fetch from this end point but we also need to tack on at the end of it a single id so forward slash and then plus the id which is this thing right here so that's going to get one single item for us each time around

```javascript
export const getStaticPaths = async () => {
  const res = await fetch('https://jsonplaceholder.typicode.com/users');
  const data = await res.json();

  // map data to an array of path objects with params (id)
  const paths = data.map(ninja => {
    return {
      params: { id: ninja.id.toString() }
    }
  })

  return {
    paths,
    fallback: false
  }
}

export const getStaticProps = async (context) => {
  const id = context.params.id;
  const res = await fetch('https://jsonplaceholder.typicode.com/users/' + id);
  const data = await res.json();

  return {
    props: { ninja: data }
  }
}

const Details = ({ ninja }) => {
  return (
    <div>
      <h1>{ ninja.name }</h1>
      <p>{ ninja.email }</p>
      <p>{ ninja.website }</p>
      <p>{ ninja.address.city }</p>
    </div>
  );
}

export default Details;

```
