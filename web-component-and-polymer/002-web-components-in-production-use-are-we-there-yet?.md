## [转载-002-Web Components in production use - are we there yet?](https://vaadin.com/blog/-/blogs/web-components-in-production-use-are-we-there-yet-)

***posted on 2016/01/26***

A lot of progress has been made since the introduction of the Web Components back in 2011. All major browsers have started implementation of the technologies needed to run web components natively. While browser vendors are still working on native implementations, libraries have been able to use a polyfill to make web components available to developers already.

But what is the status of Web Components for actual production use in business applications? In this post, I’ll be taking a look at the support for Web Components in browsers and their adaptation by companies. But before we get to that, let’s take a quick refresher on what Web Components are and why we would want to use them in the first place.

## The promise of Web Components

Web Components aim to change the way we build web applications by allowing developers to extend the HTML vocabulary by creating their own reusable HTML elements. This seemingly simple addition means that developers can build their software out of higher level components.

Component based UI libraries have been the standard way of building complex native applications for years, and many modern web frameworks like Angular and Vaadin give us the ability to compose our UI out of reusable blocks. The big difference between these approaches and Web Components is that Web Components bring the componentization to a DOM level so that the custom elements can be used with any framework just like any standard HTML element.

One of the great advantages of Web Components is that they allow us to build on other’s work instead of reinventing the wheel. Most software use a fairly standardized set of UI controls – components like data tables, date pickers, input fields etc. By using an existing component for your software you are not only saving the time that it would take you to build it in the first place, but you also don’t need to spend time maintaining it in the future. Instead, you get the benefits of more people contributing bug fixes and performance improvements to the same component - resulting in a better component for all users.

For a more in-depth look at the history of Web Component and the problems they hope to solve, I suggest reading this great blog post on the [Microsoft Edge Blog](https://blogs.windows.com/msedgedev/2015/07/14/bringing-componentization-to-the-web-an-overview-of-web-components/).

When we talk about Web Components, we are really talking about four separate W3C standards that together give us the tools we need to build our own components: *Custom Elements, Templates, HTML Imports* and *Shadow DOM.*

The **Custom Element** standard defines a way for us to define new element types in the browser DOM. This allows us to give our components a meaningful name that allows developers to use the component like any other HTML element. For instance, the Vaadin Grid defines a ``element.

**HTML Imports** are a way of including HTML documents in other documents. This enables us to reuse the components as we can include them on any page without having to copy-paste the HTML.

**Templates** allow us to define inert HTML subtrees that can be stamped into the DOM. Being inert means that we can define the HTML without inserting it into the DOM or running it. As an example, this allows us to import [``](https://vaadin.com/elements/-/element/vaadin-grid) into our document without it showing up before we actually use it by inserting a `` tag into our HTML.

**Shadow DOM** is the core of the Web Components standards. Shadow DOM allows us to encapsulate our element implementation into a separate DOM tree in order to shield it form the surrounding document, and conversely shielding the host document from changes introduced by the component. A good example of why we want to do this is CSS styling. We do not want styles from a Web Component to affect the parent page, and conversely, we don’t want the parent page to break the component. The Shadow DOM spec gives us the tools to control how we want the trees to interact with each other.

## State of browser support

As I mentioned earlier on, all browser vendors are working on introducing native support for Web Components. What’s even better is that a lot of collaboration is happening between the vendors, with members from each participating in the specification process.

**Chrome** is the current gold standard for Web Component support, largely because of Google’s strong role in pushing for the standards. All four parts of the Web Components standards have native support in Chrome and can be used without polyfills.

**Firefox** ships with an implementation for Templates and allows you to turn on Shadow DOM and Custom Elements with a development flag. The only remaining piece, HTML Imports, has been put on hold as they feel that there is too much overlap between ES6 Module Loading and HTML Imports and want to see how this plays out. Regardless of this, Wilson Page from Mozilla concluded in a [June blog post](https://hacks.mozilla.org/2015/06/the-state-of-web-components/) that “we’re optimistic the end is near. All major vendors are on board, enthusiastic, and investing significant time to help resolve the remaining issues.”

**Safari (WebKit)** ships with template support and as of recently Shadow DOM support in nightlies. There is also a prototype implementation of Custom Elements, but like Mozilla, the WebKit team believes that [ES6 modules should be the basis for importing templates](https://webkit.org/blog/4096/introducing-shadow-dom-api/) and is therefore not actively working on supporting them yet.

Microsoft recently shipped HTML Template support in **Edge** 13. In a [blog post](https://blogs.windows.com/msedgedev/2015/07/15/microsoft-edge-and-web-components/), they indicated that they are working on implementing all of the Web Component standards and are collaborating with the other vendors in finalizing the specification work.

### Polyfills

As native browser support is not quite there yet even in the most recent browser versions, any production use will still need to rely on the [Web Components Polyfill](http://webcomponents.org/polyfills/) in order to support most browsers. With the polyfill, Web Components can be used in all the latest evergreen web browsers as well as Internet Explorer 11. As Microsoft [ended support for older versions of IE in January](https://www.microsoft.com/en-us/WindowsForBusiness/End-of-IE-support) the polyfill will allow you to target all actively supported web browsers out there.

As more browsers are adding support for Web Components, you should use feature detection to determine whether or not the polyfill is needed, so users on browsers with native support can get a faster experience.

### Libraries

The Web Component APIs offer fairly low level programmatic APIs, so several libraries have been created to ease the development of new Web Components: [X-Tag](http://x-tag.github.io/), [Polymer](https://www.polymer-project.org/) and [Bosonic](http://bosonic.github.io/). All the libraries offer helpers and syntax sugar to cut down boilerplate code and make creating new components easier. They all use the same Web Components polyfill as their base.

Both Polymer and Bosonic also offer a library of ready made Web Components in addition to the helper APIs. Fortunately, as a consumer of Web Components you don’t need to worry about what libraries have been used for creating components. As they are all based on the Web Components standards, you can mix and match components as you please.

Out of the three libraries, Polymer has been most widely adopted. [The Vaadin Elements web component library](https://vaadin.com/elements) is based on Polymer.

## Web Component adaptation

Web Components have been taken into production use by several big companies such as Google, GitHub, Comcast, Salesforce and General Electric. Some of the more high profile sites using Web Components are [Youtube Gaming](https://gaming.youtube.com/), [Google Patents](https://patents.google.com/), [Google Music](https://play.google.com/music/listen) and [GitHub](https://github.com/).

According to the [Chrome Dev Summit Keynote by Taylor Savage](https://www.youtube.com/watch?v=lck68wyVUo4), there were already over 1,000,000 sites using Polymer in November 2015. So even though Web Components are still a new and evolving technology, there are already a lot of people and companies using them in the wild.

## Should you build your app with Web Components?

Now that we’ve seen that Web Components are already in production use by some of the biggest companies in the world and that the Web Component polyfill will allow us to support all modern browsers, the question that remains to be answered – how do you get started?

Many people struggle with understanding how Web Components should be used. Should individual Web Components be used to extend existing front end frameworks, or should you build your entire application out of Web Components?

The creators of Bosonic [explain that](http://bosonic.github.io/documentation/reference/introduction.html) “Web Components enable the creation of UI atoms as HTML elements, atoms that you can include into your components templates, powered by Angular, Ember, React or whatever”. Likewise, Kevin Schaaf from the Polymer team [explained that](https://www.youtube.com/watch?v=ZDjiUmx51y8) “Polymer’s primary mission is to help you build custom elements – full stop”. However, he continues to explain that by leveraging the DOM as your framework, you are able to build full applications with nothing but Web Components.

This means that you can use Web Components as much or as little as you want in your application. You can decide to only improve one static table on your site by wrapping it in a [``](https://vaadin.com/elements/-/element/vaadin-grid) or introduce a “time ago” tag like [GitHub](https://github.com/github/time-elements). But there’s also nothing preventing you from building a full blown application with nothing but Web Components like we did in our [Expense Manager Web Components demo application](http://demo.vaadin.com/expense-manager/) – the choice is yours.

# [Get started with the Vaadin Elements Web Component library]()