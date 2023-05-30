# Morphull - Astro Starter Kit

A morphing or full page transition enabled slide creation starter kit that uses [View Transitions](https://developer.mozilla.org/en-US/docs/Web/API/View_Transitions_API) to do all the work. 

Until View Transitions are supported across all browsers, this API and starter kit only works in [Chrome Canary](https://www.google.com/chrome/canary/) with [chrome://flags/#view-transition-on-navigation](chrome://flags/#view-transition-on-navigation) enabled.

## 🚀 Project Structure

Inside the `/pages` folder you create your slides, each slide is it's own Astro component that uses the `/src/layouts/Slide.astro` layout.

There's one component called `Controls.astro` that handles making and placing the next arrow.

## How to get morphing slide pages

It's all generally handled for you! Just use `<h1>` elements, or images or links. Inside the `/src/styles/transitions.css` you'll find the unique names given to the elements that tells the browser which shared elements should morph. Like if you have a code snippet on one page, and the next page also has one, the browser will transition between those snippets.

### Enabling page transitions

Full page transitions can be enabled on a per slide basis, by simply passing `animation="page"` as a property to the `Layout` / `Slide` component. This will on the other hand will automatically disable slide page morphing.

### Writing custom page transitions

To write custom page transitions, you can simply hook into the functionality already provided by morphull. Currently, there are two data attributes that are written to the `<html>` when the page is initialized that form the basis for all animations.

| Attribute | Values | Description |
| --- | --- | --- |
| `data-view-transition-direction` | `'forward'`, `'back'`, `'reload'` | The direction of navigation. Reload means that a page refresh is initiated. |
| `data-view-transition` | `'page'`, `'element'`, Custom | Default: `'element'`. <br>  Animation identifier used within CSS |

With the help of these attributes and open-props custom page transitions can be written as easy as:

```css
  html:not([data-view-transition-direction="reload"])[data-view-transition="slide"] {
    &::view-transition-new(root) {
      animation: var(--animation-slide-in-left) forwards;
    }

    &::view-transition-old(root) {
      animation: var(--animation-slide-out-left) forwards;
    }

    &[data-view-transition-direction="back"] {
      &::view-transition-new(root) {
        animation: var(--animation-slide-in-right) forwards;
      }

      &::view-transition-old(root) {
        animation: var(--animation-slide-out-right) forwards;
      }
    }
  }
```
In particular, we use `:not([data-view-transition-direction="reload"])` in this example to prevent transitions from being replayed on page refresh. There is currently an ongoing discussion about this behavior right [here](https://github.com/w3c/csswg-drafts/issues/8784).
A working example identical to the code above can be found in `src/pages/example-3.astro`.