# HW - Web Components-3 - Build a component driven web app

## I. Overview

- Video links are below
- Coming soon! An announcement will be made in Slack once this document has been updated

<hr>

## II. Start Code

- Start files are here: [sw-start.zip](_files/sw-start.zip)
- Here's a screenshot of the starting version
- It has most of the fuctionality of the completed version, except that we are going to rewrite much of the app to use 3 web components

![screenshot](_images/_wc/HW-wc-9.png)

<hr>

## III. Screen Shot of completed version

- Note the HTML for the 3 components below
- The final version allows us to add multiple `<sw-card>` instances to the page

```html
<body>
	<sw-header data-title="Star Wars Character Finder"></sw-header>
	<main>
		<select id="character-select"></select>
		<hr>
		<div class="cardlist">
			<!-- This is where the <sw-cards> are displayed -->
		</div>
	</main>
	<sw-footer data-title="Ace Coder" data-year="2021"></sw-footer>
</body>
```

<hr>

![screenshot](_images/_wc/HW-wc-10.png)

<hr>

## IV. Walkthrough

### IV-A. Look at start code
- A few new things in here:
  - `fetch()` (with no error handling code)


<hr><hr>

| <-- Previous Unit | Home | Next Unit -->
| --- | --- | --- 
|  [**HW - Web Components II**](HW-wc-2.md)  |  [**IGME-330**](../README.md) | :-\
