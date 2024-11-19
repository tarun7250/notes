# execution order in next js
- headers from next.config.js
- redirects from next.config.js
- Middleware (rewrites, redirects, etc.)
- beforeFiles (rewrites) from next.config.js
- Filesystem routes (public/, _next/static/, pages/, app/, etc.)
- afterFiles (rewrites) from next.config.js
- Dynamic Routes (/blog/[slug])
- fallback (rewrites) from next.config.js


- in pages folder any file is route with same filename
- index.js defaults to the above folder name 
- `pages/dashboard/settings/username.js → /dashboard/settings/username`
- export default must be there

# Single Shared Layout with Custom App
- create `_app.tsx`
```tsx
import Layout from '../components/layout'

export default function MyApp({ Component, pageProps }) {
  return (
    <Layout>
      <Component {...pageProps} />
    </Layout>
  )
}
```

# Per-Page layout
- create a `getLayout` function in each page 
```tsx
import Layout from '../components/layout'
import NestedLayout from '../components/nested-layout'
export default function Page() {
  return (
    /** Your content */
  )
}
Page.getLayout = function getLayout(page) {
  return (
    <Layout>
      <NestedLayout>{page}</NestedLayout>
    </Layout>
  )
}
```
- then in `_app.js`
```tsx
export default function MyApp({ Component, pageProps }) {
  const getLayout = Component.getLayout ?? ((page) => page)
  return getLayout(<Component {...pageProps} />)
}
```

# using typescript
- TypeScript, you must first create a new type for your pages which includes a getLayout function. Then, you must create a new type for your AppProps which overrides the Component property to use the previously created type.
```tsx
export type NextPageWithLayout<P = {}, IP = P> = NextPage<P, IP> & {
  getLayout?: (page: ReactElement) => ReactNode
}
type AppPropsWithLayout = AppProps & {
  Component: NextPageWithLayout
}
```

# data fetching
- fetch data on the client-side using `useEffect` or a library like `SWR`

# dynamic routing
- A Dynamic Segment can be created by wrapping a file or folder name in square brackets: [segmentName]. For example, [id] or [slug]
- Dynamic Segments can be accessed from `useRouter` hook
```tsx
const router = useRouter();
router.query.slug;
```

```tsx
import { withRouter } from 'next/router'
function Page({ router }) {
  return <p>{router.pathname}</p>
}
export default withRouter(Page)
```

### catching segments in dynamic routing
| Route | Example URL | params |
| -- | -- | -- |
| pages/blog/[slug].js |	/blog/a	| { slug: 'a' } |
| pages/blog/[slug].js |	/blog/b	| { slug: 'b' } |
| pages/blog/[slug].js |	/blog/c	| { slug: 'c' } |

catching all segments
| Route | Example URL | params |
| -- | -- | -- |
| pages/blog/[...slug].js |	/blog/a	| { slug: ['a'] } |
| pages/blog/[...slug].js |	/blog/a/b	| { slug: ['a', 'b'] } |
| pages/blog/[...slug].js |	/blog/a/b/c	| { slug: ['a', 'b', 'c'] } |


optional catching all segments
| Route | Example URL | params |
| -- | -- | -- |
| pages/blog/[[...slug]].js |	/blog	| { slug: undefined } |
| pages/blog/[[...slug]].js |	/blog/a	| { slug: ['a'] } |
| pages/blog/[[...slug]].js |	/blog/a/b	| { slug: ['a', 'b'] } |
| pages/blog/[[...slug]].js |	/blog/a/b/c	| { slug: ['a', 'b', 'c'] } |

# linking and navigation
- `Link` component is used for client side route transition
```tsx
<Link href="/about">About Us</Link>

<Link href={`/blog/${encodeURIComponent(post.slug)}`}>
  {post.title}
</Link>

<Link href={{
    pathname: '/blog/[slug]',
    query: { slug: post.slug },
  }}
>
  {post.title}
</Link>
```
- `pathname` is the name of the page in the pages directory. `/blog/[slug]` in this case.
- `query` is an object with the dynamic segment. `slug` in this case.


- `/about` -> `pages/about.js`
- `static generation` - data is prefetched
- 
## Imperative routing

```tsx
<button onClick={() => router.push('/about')}>
```

## shallow routing
- works only in same pages
- just change the queries will not reload the pages

# redirecting 
- `useRouter` hook

## next.config.js
```js
module.exports = {
  async redirects() {
    return [
      // Basic redirect
      {
        source: '/about',
        destination: '/',
        permanent: true,
      },
      // Wildcard path matching
      {
        source: '/blog/:slug',
        destination: '/news/:slug',
        permanent: true,
      },
    ]
  },
}
```
- `307 (Temporary Redirect)` or `308 (Permanent Redirect)` status codes
- redirects may have a limit on platforms
- redirects runs before Middleware.

-------------------------------



- App does not support Next.js Data Fetching methods like `getStaticProps` or `getServerSideProps`.

- Using `getInitialProps` in App will disable Automatic` Static Optimization` for pages without `getStaticProps`
```tsx
import App, { AppContext, AppInitialProps, AppProps } from 'next/app'
type AppOwnProps = { example: string }
export default function MyApp({
  Component,
  pageProps,
  example,
}: AppProps & AppOwnProps) {
  return (
    <>
      <p>Data: {example}</p>
      <Component {...pageProps} />
    </>
  )
}
MyApp.getInitialProps = async (
  context: AppContext
): Promise<AppOwnProps & AppInitialProps> => {
  const ctx = await App.getInitialProps(context)

  return { ...ctx, example: 'data' }
}
```

# middlewares
- Middleware runs before cached content and routes are matched
- create `middleware.ts` in root of project at same level as pages or app(not _app) inside src
- `NextResponse.redirect(new URL(destination,source))` - redirect from source to destination, export a config having url matchers
```ts
export function middleware(request: NextRequest) {
  return NextResponse.redirect(new URL('/home', request.url))
}
export const config = {
  matcher: '/about/:path*',//can be array
}
```
- bypass Middleware for certain requests by using the `missing` or `has`
- `NextResponse.rewrite(new URL(destination, source))` - rewrite destination into source url without changing source url
```ts
if (request.nextUrl.pathname.startsWith('/about')) {
  return NextResponse.rewrite(new URL('/about-2', request.url))
}
```

## getting and setting cookies 
```ts
request.cookies.has('nextjs')//getting cookies from request
```
```ts
const response = NextResponse.next();
response.cookies.set({
    name: 'nextjs',
    value: 'cookieValue',
    path: '/',
  });
return response;
```

- default, Next.js pre-renders every page in server.
# pre rendering
- Static Generation over Server-side Rendering, CDN caches SG
- hybrid site
## static generation
- HTML is generated on **build Time** and used on each request

```js
export default function Page({ data }) {
}
// This function gets called at build time
export async function getServerSideProps() {
  const res = await fetch(`https://.../data`)
  const data = await res.json()
  return { props: { data } }
}
```
- for having dynamic path make file name like /[id].js and
- export an async function called getStaticPaths from a dynamic page /[id].js
```js
// This function gets called at build time
export async function getStaticPaths() {
  const res = await fetch('https://.../posts')
  const posts = await res.json()
  const paths = posts.map((post) => ({
    params: { id: post.id },
  }))
  // { fallback: false } means other routes should 404.
  return { paths, fallback: false }
}
```

- use both together to use both usage

### increamental static generation
```js
export async function getStaticProps() {
  const res = await fetch('https://.../posts');
  const posts = await res.json();

  return {
    props: {
      posts,
    },
    revalidate: 60, // Number of seconds to wait before re-generating the page
  };
}
```

- In ISR the cache is only invalidated and regenerated when a `request is received after` the `revalidate time has passed`.
- `Middleware won't` be executed for `on-demand ISR` requests


### getStaticProps
- it runs on server not on client
- `getStaticProps` always runs during next build
- `getStaticProps` runs in the background when using `fallback: true` will server-render pages on-demand if the path doesn't exist
- `getStaticProps` is called before initial render when using `fallback: blocking`
- `getStaticProps` runs in the background when using `revalidate`
- `getStaticProps` runs on-demand in the background when using `revalidate()`
- `getStaticProps` can only be exported from a page like `getStaticPaths`


- In development (next dev), `getStaticProps` will be called on every request.

- defer generating all pages on-demand by returning an `empty array` for `paths`

```js
if (process.env.SKIP_BUILD_STATIC_GENERATION) {
  return {
    paths: [],
    fallback: 'blocking',
  }
}
```



## server side rendering
- HTML is generated on each request
- of activating `SSR` - `export` an `async` function called `getServerSideProps`
- user visits the page through `next/link` or `next/router`, Next.js sends an API request to the server, which runs `getServerSideProps`.?????
- cache control
```js
// This value is considered fresh for ten seconds (s-maxage=10).
// If a request is repeated within the next 10 seconds, the previously
// cached value will still be fresh. If the request is repeated before 59 seconds,
// the cached value will be stale but still render (stale-while-revalidate=59).
//
// In the background, a revalidation request will be made to populate the cache
// with a fresh value. If you refresh the page, you will see the new value.
export async function getServerSideProps({ req, res }) {
  res.setHeader(
    'Cache-Control',
    'public, s-maxage=10, stale-while-revalidate=59'
  )
 
  return {
    props: {},
  }
}
```


## client side rendering
- Using React's useEffect() hook inside your pages instead of the server-side rendering methods (`getStaticProps` and `getServerSideProps`).
- Using a data fetching library like `SWR` or `TanStack Query` to fetch data on the client (recommended).

```js
import useSWR from 'swr'
export function Page() {
  const { data, error, isLoading } = useSWR(
    'https://api.example.com/data',
    fetcher
  )
  if (error) return <p>Failed to load.</p>
  if (isLoading) return <p>Loading...</p>
  return <p>Your Data: {data}</p>
}
//can use this
const fetcher = (...args) => fetch(...args).then((res) => res.json())
function Profile() {
  const { data, error } = useSWR('/api/profile-data', fetcher)
}
```



## static assets
- `/public` folder can be used to serve `static assets` like images, fonts, and other files. 
- Files inside `/public` can also be cached by CDN providers so that they are delivered efficiently.

