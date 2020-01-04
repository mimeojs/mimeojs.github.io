## Welcome to MimeoJS

> The stencil duplicator or mimeograph machine (often abbreviated to mimeo) is a low-cost duplicating machine that works by forcing ink through a stencil onto paper.<sup>[wikipedia](https://en.wikipedia.org/wiki/Mimeograph#cite_note-1)</sup>

MimeoJS combines the power of [StencilJS](https://stenciljs.com) with the ease of [GatsbyJS](https://gatsbyjs.org) to create awesome websites and apps.

### What does it do?

As a front-end developer it's a pain to write code in one way when you add CSS/JS in a back-end CMS and in a different way when you add them to your front-end app, gatsby solves this by basically creating a hydrated version of a [ReactJS](https://reactjs.org) app with data provided from a build-time GraphQL server (I'm over simplifying here, but hey). This makes front-end developers happy because templates _look_ and _feel_ like React components (sort of) and back-end developers are happy because there's a declarative way of exposing the whole taxonomy and data of a site through a common API (GraphQL).

As awesome as GatsbyJS and ReactJS are I want to re-invent the wheel because:

- I love StencilJS and I think that web-components are the atoms of what the future of the web is about.
- GraphQL is awesome but do I _really_ want to do my markdown-to-html rendering on the server (for example)?
- I beleive in [UNIX pipes](https://en.wikipedia.org/wiki/Pipeline_(Unix)) and think a CMS should be built in small pieces.

### How does it work

StencilJS already supports [prerendering](https://stenciljs.com/docs/prerendering) so we're going to leverage that, possibly together with the [hydrate app](https://stenciljs.com/docs/hydrate-app) depending on how data is provided.

> One thing I have to admit that GatsbyJS got right is that you want a unified data-access pipeline and that GraphQL is the correct protocol for it, but I'm not 100% convinced that putting _all_ your logic there is the correct thing. **So the idea is to use GraphQL to fetch content for pages, and for this GraphQL server to _only_ have to be avaliable during _build time_**.

It's trivial to set upp a StencilJS app that uses [`stencil-router`](https://github.com/ionic-team/stencil-router) or similar to parse parameters from the URL and fetch some data over GraphQL to display on the page, actually this is how most of us write a _basic_ front-end application today. But what pages to I need to render?

> In GatbyJS you get this fancy `gatsby-node.js` file that you can use to call the internal API's to tell the build server what pages should be generated, however flexible this is I just find it annoying.

There's an old-school way of defining possible routes on your web site, a [`sitemap.xml`](https://en.wikipedia.org/wiki/Site_map#XML_sitemaps). So the default way is just to make one of those and the rendering process will use that as input. If that's not enoug I'm thinkning a `sitemap.ts` would be easy enough to implement so that whoever want more flexibility can get it.

### Is there secret sauce?

Possibly. I'm thinking that injecting a different GraphQL client during SSR than post-hydration to get a division between static/dynamic content without having to do anything with your client code.

Another thing would be serializing any access data during SSR into the HTML but in such a way that it would populate something like [`apollo-cache-inmemory`](https://github.com/apollographql/apollo-client/tree/master/packages/apollo-cache-inmemory) so data access done after re-hydration is available without reloading.

### What's up with the logo?

Stole it [from here](http://redfinchjapanese.com/?action=kanji_dictionary&kanji=1888) Where I found out that 謄 (if I understand it correctly) means "Mimeograph" - perfect.
