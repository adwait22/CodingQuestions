# Web Components ---------------------------------------------
- Reusable custom web components
> class AppDrawer extends HTMLElement {  }
> window.customElements.define('app-drawer', AppDrawer);
- This helps you attach event listener inside class itself, like hover for tooltip

# App Shell Model ---------------------------------------------
- Minimum HTML/CSS/JS to power UI like nav and component, cache them and send them first

# PRPL (Push, Render, Pre-cache, Lazy-load) ---------------------------------------------
- optimize by aggressive code-splitting and caching

# Optimize JS first send with tree shaking and code-splitting ---------------------------------------------

# Cache API for cache network req. used by Service Worker but we can also used it

# Lazy loading images - load after scroll reached the viewport ---------------------------------------------
- user IntersectionObserver

# Critical Rendering Path ---------------------------------------------
- Optimize to allow browser to paint the page asap
- HTML and CSS parse in following way
- Byte -> Character -> Token(tags) -> Lexing(token->object) -> DOM/CSSOM markup object tree
- Combine DOM & CSSOM -> Render tree(only visible node) -> Layout Computes -> Paint
- until CSSOM is complete paint won't happen use media="print" to keep it later (only specific)
- JS initial execution use async/defer
- avoid two round trips use same basic css in index file

# HTTP/2 ---------------------------------------------
> Binary Framing <==
- Header Frame and Data Frame
> Multiplexing <==
- Browser can ask for multiple request(css and js encounter) at same time from server 
- and without cutting the connection get all responses in stream.
> HTTP/2 push <==
- Can be performed by server to push css even when only HTML is asked
- Can be done in .htaccess using Link HEADER
> <FilesMatch "\.html$">
>    Header set Link "</css/styles.css>; rel=preload; as=style"
> <FilesMatch>
- sever push when item is cached in server can use unnecessary bandwidth
- use h2-auto-push(by google) to take care of these automatically
> Header compression <==
- Why send same header again and again only send unique


# Rendering Performance ---------------------------------------------
> JS execution <==
- Avoid long-running JS code or use requestIdleCallback()
- requestAnimationFrame(cancelAnimationFrame) rather than setTimeout and setInterval
- requestAnimationFrame stop for inactive tab, and optimized by browser
- function step(time){ id = requestAnimationFrame(step); }
- time can use and it is time from opening of that tab
- use micro task happening to make DOM changes in several frames
> Style complexity <==
- reduce css complexity like last child first child
- because it needs resources
> Avoid large complex layout <==
- use flexbox for position it is optimized
> Reduce paint area <==
- Reduce shadows
- promote element you want to animate
- .moving-element {
-     transform: translateZ(0);
-   }
- This will allow to that element to be in different layer and repaint will happen only in that layer
> Debouncing your input handler <==


# Infinite list optimization ---------------------------------------------
- In react instead of passing all component to list
- Use viewport o determine the tweets can be shown in that space
- and only pass that many tweets to the list formation array
> Now when adding more tweets use requestAnimationFrame <== to add tweets over multiple frames rather than in one frame
- And preserve scroll position
> Also the components which are non-critical keep them in requestIdealCallback API <==
- And also keep requestAnimationFrame inside requestIdealCallback as well so that its safe to update DOM


# Event Listener options ---------------------------------------------
- { capture: true, passive: true, once: true }
- if passive e.preventDefault() cannot be called
- if not passive then browser will run the code block then it will run the event
- this causes slow browser scroll and we should use passive in "touchmove" events listeners (or better use intersectionObserver)
- use once if you know click should happened once and you will re-attach listener later if required

# Use GraphQL for less AJAX calls ---------------------------------------------

# Code Splitting ---------------------------------------------
- Code splitting not by a human is a good ides
- Code splitting by route is basic and must have
> One route can have many components which are not shown always like google page with calc
- So we use Lazy-Load at component level
> But lazy-loading can come out bad with latency(we reduce) point of view
> Again developer had to decide what to lazy-load - which is not good
- Split logic and rendering 
> Like UI to be server-side rendered but logic to be loaded if component is rendered
> Only trade of is Hydration while server-side rendered
> i.e. component loaded on both server side and client side (CPU wastage)
> But Google Does it
- CSS-in-JS to avoid "Central Configuration" at all cost
> Because removal of code becomes a challenge otherwise
- Router.JS, webpack.config.js and package.json to be decentralize as well

## Think with your engineers on your team about how they will use your APIs and how they will use your abstractions while build a framework or mini framework


## AMP make fast ---------------------------------------------
- ==> Never stop content use async
- ==> static layouting (image space before loading) (uncouple document layout from resource layout)
- ==> inline size-bound css (max size 50kb limit)
- ==> Web Font triggering and downloading (until font download zero http request)
- ==> Minimize style and layout recalculations (static layouting is an example)
- ==> GPU accelerated animation (stay with transform and opacity)
- ==> Prioritize resource loading

# Html in html
- Embed ==> any content hence used for video/audio
- iframe ==> frame with url link for show
- html import ==> <link import=""> with append script
- Shadow Dom


## Web RTC real time connection
- browser peer connection and sharing

## Web Assembly - Wasm
- running C/C++ like language by keep it pre downloaded and then running
- this will make realistic gaming possible inside browsers

# Prefetch - for next page
- Use intersection observer to add prefetch attribute dynamically

# Preload - for current page