---
theme: seriph
title: CSS Standardization
titleTemplate: '%s - MllrDev'
lineNumbers: false
remoteAssets: true
fonts:
  sans: Roboto
  mono: Fira Code
layout: intro
download: true
---

# MllrDev CSS Standardization

Road to keeping our sanity <img style="height:20px;display:inline-block;" src="https://cdn.discordapp.com/emojis/596410833236525071.webp?size=96&quality=lossless" /> when writing CSS.

---

# Agenda

- Design Principles
- Current Pain Points
- ITCSS + shame.css
- BEMIT
- Adoption strategy
- Mobile-First Design
- Utility-First CSS  
- Open-discussion

---

# Design Principles

<v-clicks>

- Every developer and development team has their own rules and preferences when writing code. Those who work solo may come up with their own standards while an in house corporate team may be subject to standards put in place long before any of them ever worked at the firm. So if you ask five developers, you'll probably get five opinions on what is the right way to structure your code. So keep an open mind when tackling this topic.

- With that said, keep these principles in mind:
  - Keep markup structured and organized.
  - Only use ID for programmatic access, not styling.
  - Name classes by purpose or responsibility, not by appearance or layout.
  - Maintain separation of concerns.
  - Keep it simple.

</v-clicks>

---

# Current Pain Points

<v-clicks>

- Lack of confidence in editing existing **CSS**
- No formal structure on where to put **CSS** styles
- Poor naming conventions on **CSS** selectors
- Poor markup semantics leading to bloated and/or large components
  - Could've been broken down into smaller components
- Poor visibility of potentially reusable **CSS**

</v-clicks>

<v-click>

## Tangible Effects

</v-click>

<v-click>

- Hard to Code Review
- Hard to Maintain

<et-caution class="text-red-500" /> <ins class="text-red-500">**C**</ins>haos <ins class="text-red-500">**S**</ins>tyled <ins class="text-red-500">**S**</ins>heets <et-caution class="text-red-500" />

</v-click>

---

## The Problem

If you have worked on a site that has been around for quite some time, you will not be surprised to hear that:

<v-clicks>

- There are often multiple large style sheets associated with the site.
- The contents of the file are often not in a logical order.
- The names and folder structures weren't designed to make your life easier either.

</v-clicks>

---

## Worse Case Scenario

Now these files probably started life with the developer's best intentions, but over time as developers have come and gone and as the site has been maintained for quite some time, you may see that,

<v-clicks>

- Things were done in the interest of time and convenience (thus accruing technical debt) instead of logic and future maintenance.
- The existing CSS was written with rules that have certain specificity so when new pages or markup were added to the site, the new elements didn't look right.
- The developer may have become frustrated trying to find the right rules to replace or update and decided to just add a new file that overrides existing rules.
- The developer tacked their changed onto the end of one of the files without much thought as long as it worked.

</v-clicks>

---
layout: center
---
![image](/css-memes/blinders-css.gif)

---
layout: statement
---

# What can we do?

Adopt CSS Methodologies

---
layout: section
---

# ITCSS

Inverted Triangle CSS

---

# ITCSS

Inverted Triangle CSS

It was developed by Harry Roberts with the idea of <ins>organising our CSS code in an optimal way</ins>. Its name comes from Inverted Triangle architecture for CSS because of the way in which the files are <ins>organised in layers according to the level of specificity and importance</ins>.

Roberts himself defines ITCSS as follows:

- It is a **scalable and manageable architecture**.
- It is a philosophy, **not a library**.
- It is **preprocessor-independent** (although it is really best served by using one).
- It is a **meta framework**, a framework for frameworks. That is, it serves as a base to be used with other frameworks.

---
layout: center
---

![ITCSS Diagram](/css-diagrams/itcss.png)

---
layout: center
---

## Different specificity levels in our compiled stylesheet

![image](https://i.imgur.com/nqAhqps.png)

---
layout: center
---

## Goal

![image](https://i.imgur.com/5z6xERk.png)

---
layout: center
---

<div class="text-center">

## Projects here in MSD and their stylesheet specificity graphs

In no particular order :)

</div>

---

## Team Argus

![Team Argus](/css-graphs/Argus.png)

---

## Team BoardClic (Old)

![Team BoardClic Old](/css-graphs/BoardClic-Old.png)

---

## Team BoardClic (New)

![Team BoardClic New](/css-graphs/BoardClic-New.png)

---

## Team Designage

![Team Designage](/css-graphs/Designage.png)

---

## Team JobAgent

![Team JobAgent](/css-graphs/JobAgent.png)

---

## Team Loq

![Team Loq](/css-graphs/Loq.png)

---

## Team Profilservice

![Team Profilservice](/css-graphs/Profilservice.png)

---

## Team Schysst Kak

![Team Schysst Kak](/css-graphs/Schysst-Kak.png)

---

## Team Skavsta

![Team Skavsta](/css-graphs/Skavsta.png)

---
layout: center
---

![ITCSS Diagram](/css-diagrams/itcss.png)

---
layout: two-cols
---

## Settings

This is where variables (e.g., colors, fonts, spacing, breakpoints) are defined.

```scss
$main-color: #6834cb;
```

```scss
@font-face {
  font-family: myFirstFont;
  src: url(sansation_light.woff);
}
```

## Tools

If a preprocessor is used, functions and mixins are defined in this layer.

```scss
@function sum($numbers...) {
  $sum: 0;
  @each $number in $numbers {
    $sum: $sum + $number;
  }
  @return $sum;
}
```

::right::

![ITCSS Diagram](/css-diagrams/itcss.png)

<div class="text-center">1/5</div>

---
layout: two-cols
---

## Generic

This refers to generic code, that which serves to reset or standardise the base styles of browsers. For example a reset css or a normalize would go here.

```css
* {
  padding: 0;
  margin: 0;
}
```

<br />

## Elements

Rules affecting HTML tags.

```scss
h1 {
  color: $main-color;
  font-size: 24px;
}
```

::right::

![ITCSS Diagram](/css-diagrams/itcss.png)

<div class="text-center">2/5</div>

---
layout: two-cols
---

## Objects

Common structural design patterns. Small and reusable non-cosmetic pieces which can be used in UI composition.

```css
.o-grid-container {
  display: grid;
  grid-template-columns: auto auto auto auto;
}
```

<v-click>

The most confusing layer <img style="height:20px;display:inline-block;" src="/public/css-memes/kekw.jpg" />

If you make changes to any of the styles in this layer, you can expect changes throughout the entire app.
This is the most confusing layer due to it mixing _objects_ and _components_. We should be using this layer whenever possible. if this layer does not make sense in your current project, then this layer can be skipped. This is yet another nice aspect of ITCSS: you can change and adapt anything to your specific needs.

</v-click>

::right::

![ITCSS Diagram](/css-diagrams/itcss.png)

<div class="text-center">3/5</div>

---

## Objects

- Do note that if you skip this layer, that would mean this layer will essentially be one with the [`Components`](#components) layers and developers might change styles haphazardly without knowing its consequences on other places of the site.

---
layout: two-cols
---

## Components

Components, unlike objects, are specific parts of the interface. The styles we define for a component will only affect that component.

```scss
.c-search-bar {
  background-color: $color-pearl;
  color: $color-light-grey;
  font-size: 2rem;
}
```

::right::

![ITCSS Diagram](/css-diagrams/itcss.png)

<div class="text-center">4/5</div>

---
layout: two-cols
---

## Trumps

This layer, also called Utilities, encompasses all those rules that override any other rules defined in the previous layers. It is the only layer where !important is allowed.

```css
.d-none {
  display: none !important;
}

.w-1\/2 {
  /* <input class="w-1/2" /> */
  width: 50%;
}
```

::right::

![ITCSS Diagram](/css-diagrams/itcss.png)

<div class="text-center">5/5</div>

---
layout: two-cols
---

# shame.css

Please avoid populating this file too much.

Sometimes, we need to use quick fixes, hacks and questionable techniques in our code in order to meet deadlines, get something working, or fix pressing/live bugs. Where do we put this?

The real problem, though, is that we rarely go back and tidy these things up. They slip through the cracks, get ignored, go unnoticed, and stay for good. This file aims to centralize these so it's easier to locate and pay the technical debt down the line.

::right::

<v-click>

# Rules

</v-click>

<v-clicks>

- If it’s a hack, it goes in `shame.css`.
- Document all hacks fully:
  - What part of the codebase does it relate to?
  - Why was this needed?
  - How does this fix it?
  - How might you fix it properly, given more time?
- Do not blame the developer; if they explained why they had to do it then their reasons are probably (hopefully) valid.
- Try and clean `shame.css` up when you have some down time.
  - Even better, get a tech-debt story in which you can dedicate actual sprint time to it.

</v-clicks>

---

## shame.css file example

Below is a template you can use as a comment to your entries in the file:

```css
/*
1. What part of the codebase does it relate to?
Answer

2. Why was this needed?
Answer

3. How does this fix it?
Answer

4. How might you fix it properly, given more time?
Answer

*/
```

---

## Directory Example (1/2)

- Put the layer's number before the folder name.
- Apply an index barrel per layer.
- All files under the layer should have an `_` prefix to indicate that it is part of something and should be imported in their respective index barrel files.

---
layout: two-cols
---

###### Directory Scaffold

```text
/styles
  /1-settings
    /_colors.setting.css
    /_fonts.setting.css
    /_spacing.setting.css
    /index.css
  /2-tools
    /_mixins.tool.css
    /index.css
  /3-generic
    /_reset.generic.css
    /index.css
  /4-elements
    /index.css
  /5-objects
    /_containers.object.css
    /_button.css
    /index.css
  /6-components
    /_search-bar.component.css
    /_navbar.component.css
    /index.css
  /7-trumps
    /index.css
  /shame.css
  /main.css /* See snippet on the LEFTO */
```

::right::

###### MAIN CSS FILE

<v-click>

```scss
/* ./styles/main.css file */

@import './1-settings/index.css';
@import './2-tools/index.css';
@import './3-generic/index.css';
@import './4-elements/index.css';
@import './5-objects/index.css';
@import './6-components/index.css';
@import './7-trumps/index.css';
@import './shame.css';
```

</v-click>

---

## FAQ

<br>

### Where to put vendor or third party stylesheets?

<v-clicks>

- There's no one place to put this since it depends on what that third party stylesheet is doing.
- For example, `normalize.css` is a third party stylesheet depending on how you include it on your project and we import it on the [Generic](#generic) layer because of its purpose. Another example is [bootstrap](https://getbootstrap.com/docs/3.4/customize/) where you can actually import its individual files and then distribute across your project's [ITCSS](#itcss) layers based on its purpose.

</v-clicks>
<br>
<v-clicks>

### How to enforce these layers with Single Page Applications?

- If the project has a custom toolchain and/or each piece was built from scratch, this shouldn't be an issue as you can enforce it easily by manipulating the order of how the styles are imported. Otherwise, please refer to the toolchain of your framework/library/boilerplate.

</v-clicks>

---
layout: statement
---

# This should (hopefully) solve <ins>where</ins> to put <ins>what</ins>

---
layout: section
---

# BEMIT

BEM (Block Element Modifier) + ITCSS

---
layout: two-cols
---

# BEM

## Block

The sole root of the component.

## Element

A component part of the Block.

## Modifier

A variant or extension of the Block.

::right::

HTML

```html
<form class="form form--simple">
  <input class="form__input" type="text" />
  <button class="form__submit form__submit--disabled" type="submit"></button>
</form>
```

CSS

```css
.form {
  color: #000;
}
.form--simple {
  color: #00f;
}
.form__input {
  color: #000;
}
.form__submit {
  color: #000;
}
.form__submit--disabled {
  color: #fff;
}
```

---
layout: two-cols
---

## Blocks

Encapsulates a standalone entity that is meaningful on its own. While blocks can be nested and interact with each other, semantically they remain equal; there is no precedence or hierarchy. Holistic entities without DOM representation (such as controllers or models) can be blocks as well.

Block names may consist of Latin letters, digits, and dashes. To form a CSS class, add a short prefix for namespacing:

```css
.block {}

.form {}

```

::right::

## Elements

Parts of a block and have no standalone meaning. Any element is semantically tied to its block.

Element names may consist of Latin letters, digits, dashes and underscores. CSS class is formed as block name plus two underscores plus element name:

```css
.block__elem {}

.form__input{}
```

---
layout: two-cols
---

## Modifiers

Flags on blocks or elements. Use them to change appearance, behavior or state.

CSS class is formed as block’s or element’s name plus two dashes: `.block--mod`or `.block__elem--mod` and `.block--color-black` with `.block--color-red`. Spaces in complicated modifiers are replaced by dash.

::right::

Modifier is an extra class name which you add to a block/element DOM node. Add modifier classes only to blocks/elements they modify, and keep the original class:

Good

```html
<div class="form form--disabled">...</div>
 <input class="form__input form__input--shadow-yes">...</input>
```

Bad

```html
<div class="form--disabled">...</div>

```

CSS

```css
.form {
  background-color: black;
}
.form--disabled { // modifies .form class 
  background-color: white;
}

```

---
layout: two-cols
---

## SCSS

```scss
.form {
  color: #000;
    
  &--simple {
    color: #00f;
  }
    
  &__input { 
    color: #000; 
  }
    
  &__submit { 
    color: #000; 
      
    &--disabled {
        color: #fff;
    }
  }
}
```

::right::

## CSS

```css
.form {
  color: #000;
}

.form--simple {
  color: #00f;
}

.form__input {
  color: #000;
}

.form__submit {
  color: #000;
}

.form__submit--disabled {
  color: #fff;
}
```

---
layout: section
---

# BEMIT Namespaces

In no particular order.

---

# BEMIT Namespaces (1/2)

| Namespace | Description |
| --------- | ----------- |
| o- | Signify that something is an Object, and that it may be used in any number of unrelated contexts to the one you can currently see it in. Making modifications to these types of class could potentially have knock-on effects in a lot of other unrelated places. Tread carefully. |
| c- | Signify that something is a Component. This is a concrete, implementation-specific piece of UI. All of the changes you make to its styles should be detectable in the context you’re currently looking at. Modifying these styles should be safe and have no side effects. |
| t- | Signify that a class is responsible for adding a Theme to a view. It lets us know that UI Components’ current cosmetic appearance may be due to the presence of a theme. |
| is-,has- | Signify that the piece of UI in question is currently styled a certain way because of a state or condition. This stateful namespace is gorgeous, and comes from SMACSS. It tells us that the DOM currently has a temporary, optional, or short-lived style applied to it due to a certain state being invoked. |
| s- | Signify that a class creates a new styling context or Scope. Similar to a Theme, but not necessarily cosmetic, these should be used sparingly—they can be open to abuse and lead to poor CSS if not used wisely. |

---

# BEMIT Namespaces (2/2)

| Namespace | Description |
| --------- | ----------- |
| u- | Signify that this class is a Utility class. It has a very specific role (often providing only one declaration) and should not be bound onto or changed. It can be reused and is not tied to any specific piece of UI. This is _optional_. |
| _ | Underscore (_). Signify that this class is the worst of the worst—a hack! Sometimes, although incredibly rarely, we need to add a class in our markup in order to force something to work. If we do this, we need to let others know that this class is less than ideal, and hopefully temporary (i.e. do not bind onto this). |
| js- | Signify that this piece of the DOM has some behaviour acting upon it, and that JavaScript binds onto it to provide that behaviour. If you’re not a developer working with JavaScript, leave these well alone. |
| qa- | Signify that a QA or Test Engineering team is running an automated UI test which needs to find or bind onto these parts of the DOM. Like the JavaScript namespace, this basically just reserves hooks in the DOM for non-CSS purposes. |

---

## Nesting selectors is highly discouraged in BEM

However, there are valid use cases for it such as [a block modifier that can affect elements](http://getbem.com/faq/#can-a-block-modifier-affect-elements-) or the use of pseudo-selectors. If a selector other than pseudo-selectors is nested, scrutinize this during code review and see if there are alternatives to achieve the same effect.

```css
.form {
  color: #000;
}
.form__input {
  margin: 0;
}
.form__input > :first-child { // nested pseudo-selector
  text-transform: uppercase;
}
```

---
layout: two-cols
---

## Mobile-First Design

Mobile-first design is an approach in which web designers start product design for mobile devices first. This can be done by sketching or prototyping the web-app’s design for the smallest screen first and gradually working up to larger screen sizes.

Prioritizing design for mobiles makes sense as there are space limitations in devices with smaller screen sizes and teams need to ensure that the key elements of the website are prominently displayed for anyone using those screens.

::right::

![ITCSS Diagram](/public/css-diagrams/mobile-first.png)

---

## Utility-First

As the name suggests, you'll only use utility classes to style your markup. If you're to use this approach,
we recommend using [TailwindCSS](https://tailwindcss.com/) or [WindiCSS](https://windicss.org/).

```html
<div class="max-w-sm rounded overflow-hidden shadow-lg">
  <img class="w-full" src="/nature.jpg" alt="nature" />
  <div class="px-6 py-4">
    <div class="font-bold text-xl mb-2">Nature</div>
    <p class="text-gray-700 text-base">
      Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptatibus quia, Nonea! Maiores et perferendis eaque, exercitationem
      praesentium nihil.
    </p>
  </div>
  <div class="px-6 pt-4 pb-2">
    <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2">#photography</span>
    <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2">#travel</span>
    <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2">#winter</span>
  </div>
</div>
```

---
layout: two-cols
---

## Utility-First

Some Utility-First frameworks allow composition of these utility classes.

Apply [`BEMIT`](#bemit) naming convention when composing utility class names.

For example in tailwind:

```html

<!-- Before extracting a custom class -->
<button
  class="py-2 px-4 bg-blue-500 text-white font-semibold rounded-lg shadow-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-400 focus:ring-opacity-75"
>
  Save changes
</button>

<!-- After extracting a custom class -->
<button class="c-btn--primary">Save changes</button>

```

::right::

```postcss
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer components {
  .c-btn {
    @apply py-2 px-4 font-semibold rounded-lg shadow-md focus:outline-none focus:ring-2 focus:ring-opacity-75;

    &--primary {
      @apply bg-blue-500 text-white hover:bg-blue-700 focus:ring-blue-400;
    }
  }
}
```

---

## Utility-First

Do note that this approach is best used with web apps that follows a **component-based architecture** since these reusable utility classes gets abstracted within the component and you could expose variants programmatically. If you're not using such architecture, it'll be overly-repetitive when making a certain component that is commonly used and has multiple variants.

For example, imagine you have a button that has 4 variants (primary, secondary, ghost, danger) used by 30 pages, you'll end up repeating these base classes for each variant. If your team's designer decides to change something, the spacing or font size for instance, then you'll have to adjust all classes where this button is being used which can be a nightmare to maintain.

---
layout: statement
---

# Let's try to put it to practice

 <img class="m-auto" style="height: 300px" src="https://www.bram.us/wordpress/wp-content/uploads/2017/01/css-is-awesome.jpg"/>

<br>
Good Luck and have fun! <img style="height:20px;display:inline-block;" src="/public/css-memes/kekw.jpg" />
---
layout: statement
---

# Discussion
