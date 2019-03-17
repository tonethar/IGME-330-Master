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
- Change the &lt;h1> text to "RiTa - 1"
- name the file **rita-1.html**
- delete the `input.onchange = doChange;` line of JS, and the `doChange()` event handler (we don't need them)
- Now you need to import the RiTa.js library. There is a CDN for RiTa.ja here - look for the **rita-full.js** file here: https://cdnjs.com/libraries/rita - grab the URL and add a &lt;script> tag to the &lt;head> section of your start file
- Now open up the console - you should see the current version of RiTa logged out - someting like `[INFO] RiTaJS.version [1.3.89]`

### III-B. The RiTa.js library

- We now have 7 top-level objects to work with: `RiTa`, `RiString`, `RiGrammar`, `RiMarkov`, `RiWordNet`, `RiLexicon` and `RiTaEvent`
- Let's type in each of the commands listed below into the console, in order to see that they do.
  - These commands use the RiTa *lexicon* - a lexicon is a set of words, and information about these words - their pronunication and part-of-speech for example. RiTa's lexicon is approximately 40,000 words - https://rednoise.org/rita/reference/RiLexicon.php
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
     - `rs.words()` - tokenizes the sentence and puts the tokens into an array
     
### III-C. Part-of-speech "displayer"

- Now let's modify **rita-1.html** and try out some of these RiTa features we tried out above.
- What we would like to do is to display the part of speech for each word that is in the text area. This is pretty easy, here's what `doInput()` needs to look like:

```js
function doInput(e){
	let text = e.target.value;
	let rs = RiString(text);
	let pos = rs.pos()
	
	let s = "";
	for(let item of pos){
		s += item + " ";
	}
	
	output.innerHTML = s;
}
```

- Which gives you the PENN tags and looks something like this:

![screenshot](_images/text-9.png)

- Let's make this a little more human readable - here's a JavaScript dictionary (object) that has the full names for these tags - add this to your JS:

```js
let POS = {
	"cc":"Coordinating conjunction",
	"dt":"Determiner",
	"jj":"Adjective",
	"nn":"Noun, singular or mass",
	"prp":"Personal pronoun",
	"vbd":"Verb, past tense",
};
```

- Reminder - these POS tags are listed here: http://rednoise.org/rita/reference/PennTags.html
- You will also need to modify the loop to look like this:

```js
let s = "<ul>";
for(let item of pos){
  let desc = POS[item];
  if(desc == undefined) desc = "??"
  s += `<li><b>${item}</b> : ${desc}</li>`;
}
s += "</ul>";
output.innerHTML = s;
```

- Reload the page, here are the results:

![screenshot](_images/text-10.png)

- try typing in new words - you should see the part-of-speech tags appear for the new words. Obviously you will need to expand the `POS` dictionary to include all of the show the full names of all of these tags
- to get rid of the unwanted punctuation, add a call to `RiTa.isPunctuation()` for each `item`, and then `continue` if it returns true

## IV. Homework Assignment - **Maddening Libs**

- Rename **rita-1.html** to **maddening-libs.html**
- Change the &lt;h1> text to "Maddening Libs"
- Modify the example above so that it will:
  - replace all nouns and plural nouns, with a random noun or random plural noun
  - replace all proper nouns and plural proper nouns, with a random proper noun or random plural proper noun
  - replace all verbs (there are 6 tags), with a random verb of the same type
- Here is a screen shot of an example:



<hr><hr>

**[Previous Chapter <-  Simple Text Analysis (Part III)](text-3.md)**

**[Next Chapter -> Context Free Grammars (Part V)](text-5.md)**
