# 4 - The RiTa.js Computational Text Library

## I. Overview
- RiTa is a "software toolkit for computational literature"
- Documentation of the JavaScript version of RiTa is here: 
  - http://rednoise.org/rita/
  - http://rednoise.org/rita/reference/index.php
  - https://github.com/dhowe/RiTaJS
- Some of RiTa's capabilities:
  - *text tagging* - get the part of speech of a word - such as *adjective*, *verb*, *noun*, *proper noun*, *pronoun* etc  - from the PENN part of speech tags: http://rednoise.org/rita/reference/PennTags.html
    - https://en.wikipedia.org/wiki/Part-of-speech_tagging
  - *verb conjugation* and *pluralization*
  - *text generation* via context-free grammars
  


## II. Demo

### II-A. Create the Demo File
- To follow along on the demo and have a start file for the Homework , go ahead and grab the **load-text-textarea.html** file we have at [text-1.md](text-1.md#I-B)
- delete the `input.onchange = doChange;` line of JS, and the `doChange()` event handler (we don't need them)
- Now you need to import the RiTa.js library. There is a CDN for RiTa.ja here - look for the **rita-full.js** file here: https://cdnjs.com/libraries/rita - grab the URL and add a &lt;script> tag to the &lt;head> section of your start file
- Now open up the console - you should see the current version of RiTa logged out - someting like `[INFO] RiTaJS.version [1.3.89]`

### III-B. The RiTa.js library

- We now have 7 top-level objects to work with: `RiTa`, `RiString`, `RiGrammar`, `RiMarkov`, `RiWordNet`, `RiLexicon` and `RiTaEvent`
- Let's type in each of the commands listed below to see that they do.
  - These commands use the RiTa *lexicon* - a lexicon is a set of words. RiTa's lexicon is approximately 40,000 words - https://rednoise.org/rita/reference/RiLexicon.php
    - `RiTa.randomWord("nn")` - a random noun - full list of POS tags are here: http://rednoise.org/rita/reference/PennTags.html
    - `RiTa.rhymes("computer")`
    - `RiTa.pluralize("computer")`
    - `RiTa.singularize("people")`
    - `RiTa.alliterations("games")`
    - `RiTa.isRhyme("cat", "hat")`
    - `RiTa.similarByLetter("rochester")`
    - `RiTa.similarBySound("institute")`
    - `RiTa.similarBySoundAndLetter("technology")`
  
  - RiTa can also tell us about the parts of speech of a sentence:
     - `RiTa.isNoun("computer")`
     - `RiTa.isVerb("take")`
     - `RiTa.getPastParticiple("take")`
     - `RiTa.getPresentParticiple("take")`
     - `let rs = RiString("The elephant took a bite!")` - create a `RiString` object
     - `rs.analyze()` - lot's of info!
     - `rs._features.phonemes`
     - `rs._features.syllables`
     - `rs.pos()` - get the parts-of-speech of the string in an array
     - `rs.posAt(1)` - get the part-of-speech of the second word
     - `rs.words()` - tokenizes the sentence
     


<hr><hr>

**[Previous Chapter <-  Simple Text Analysis (Part III)](text-3.md)**

**[Next Chapter -> Context Free Grammars (Part V)](text-5.md)**
