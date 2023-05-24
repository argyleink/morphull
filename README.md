# Morphull - Astro Starter Kit

A morphing or full page transition enabled slide creation starter kit that uses [View Transitions](https://developer.mozilla.org/en-US/docs/Web/API/View_Transitions_API) to do all the work. 

Until View Transitions are supported across all browsers, this API and starter kit only works in [Chrome Canary](https://www.google.com/chrome/canary/) with [chrome://flags/#view-transition-on-navigation](chrome://flags/#view-transition-on-navigation) enabled.

## 🚀 Project Structure

Inside the `/pages` folder you create your slides, each slide is it's own Astro component that uses the `/src/layouts/Slide.astro` layout.

There's one component called `Controls.astro` that handles making and placing the next arrow.

## How to get morphing slide pages

It's all generally handled for you! Just use `<h1>` elements, or images or links. Inside the `/src/styles/transitions.css` you'll find the unique names given to the elements that tells the browser which shared elements should morph. Like if you have a code snippet on one page, and the next page also has one, the browser will transition between those snippets.
