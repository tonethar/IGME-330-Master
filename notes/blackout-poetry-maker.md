# Blackout Poetry Maker

## I. Overview

- Blackout Poetry is a form of *appropriation art* (the use of pre-existing objects or images) where the artist takes a pieces of text (a book, a newspaper article, a tweet, a speech and so on) and "blacks out" (subtracts) the words they don't want.
- https://writers.com/what-is-blackout-poetry-examples-and-inspiration
- https://www.google.com/search?q=blackout+poetry&source=lnms&tbm=isch
- Related antecedants:
  - Erasure Poetry - https://poets.org/glossary/erasure
  - Garfield Minus Garfield - https://garfieldminusgarfield.net/

<hr>

## II. Example App Screenshot

- Let's build a simple web version of a Blackout Poetry - the user can type text into the top `<textarea>`, click the button, and then have clickable blackout text in the bottom paragraph
- here's 2 screenshots of our first version:

![screenshot](_images/_bpm/bpm-1.png)

<hr>

![screenshot](_images/_bpm/bpm-2.png)

<hr>

## III. Start Code
- [bp-start.zip](_files/bp-start.zip)
  - look in **main.js** for comments that will get you started 


<hr>

## IV. Blackout Poetry Resources
- [YouTube - Coding Tech - Making Blackout Poetry With Computers!](https://www.youtube.com/watch?v=hoxS_tLbqYs)
- [YouTube - Austin Kleon - How To Make A Newspaper Blackout Poem](https://youtu.be/wKpVgoGr6kE)
- https://authority.pub/blackout-poetry/
- https://www.miamioh.edu/hcwe/hwc/writing-resources/howe-blackout-poetry/index.html
- https://powerpoetry.org/actions/5-tips-creating-blackout-poetry
- https://dev.to/ivavay/create-a-black-out-poetry-maker-with-javascript-4kah
- https://codepen.io/Johnesco/pen/geewXm
- https://github.com/emmawinston/blackoutpoetry
- https://codepen.io/emmawinston/pen/VqoPEY
- https://mkremins.github.io/blackout/
- https://www.poetryfoundation.org/poems

<hr>

## V. Adding more capabilities with RiTa.js

### V-A. Overview of RiTa
- RiTa is a "software toolkit for computational literature"
- Documentation of the JavaScript version of RiTa is here: 
  - http://rednoise.org/rita/
  - https://rednoise.org/rita1/reference/index.php
  - https://github.com/dhowe/RiTaJS
- Some of RiTa's capabilities:
  - *text tagging* - get the part of speech of a word - such as *adjective*, *verb*, *noun*, *proper noun*, *pronoun* etc  - from the PENN part of speech tags: https://cs.nyu.edu/grishman/jet/guide/PennPOS.html
    - https://en.wikipedia.org/wiki/Part-of-speech_tagging
  - *verb conjugation* and *pluralization*
  - word *rhyming* and *alliteration* (we'll use these today)
  - *text generation* via context-free grammars

### V-B. Installing RiTa
