# HW - Technobabble Generator

## I. Overview

- Let's build a simple "Technobabble" JavaScript application:
  - What is *Technobabble*? --> https://www.youtube.com/watch?v=4RmKTAkNacw
- When the app starts up, it gives us a random string of *technobabble*, pulled from 3 arrays
- When the user clicks the button, they get to see some new *technobabble*
- Here's a screenshot of the finished product:

![screenshot](./_images/HW-technobabble-1.jpg)

- We'll even make it look acceptable on mobile phone

![screenshot](./_images/HW-technobabble-2.jpg)


## II. Start Code

- When constructing a JavaScript web app that runs in a web browser, we are usually using at least 3 distinct computer *languages*:
  - [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) - to determine the *structure* of the page, which includes text elements such as headings and paragraphs, as well as interactive elements such as buttons and text input fields
  - [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) - *presentation*
  - [JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript) - *behavior*
  

**technobabble-start.html**
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>Technobabble Generator</title>
	<style></style>
	<script>
	"use strict";
	
	const words1 = ["Acute", "Aft", "Anti-matter", "Bipolar", "Cargo", "Command", "Communication", "Computer", "Deuterium", "Dorsal", "Emergency", "Engineering", "Environmental", "Flight", "Fore", "Guidance", "Heat", "Impulse", "Increased", "Inertial", "Infinite", "Ionizing", "Isolinear", "Lateral", "Linear", "Matter", "Medical", "Navigational", "Optical", "Optimal", "Optional", "Personal", "Personnel", "Phased", "Reduced", "Science", "Ship's", "Shuttlecraft", "Structural", "Subspace", "Transporter", "Ventral"];
	
	const words2 = ["Propulsion", "Dissipation", "Sensor", "Improbability", "Buffer", "Graviton", "Replicator", "Matter", "Anti-matter", "Organic", "Power", "Silicon", "Holographic", "Transient", "Integrity", "Plasma", "Fusion", "Control", "Access", "Auto", "Destruct", "Isolinear", "Transwarp", "Energy", "Medical", "Environmental", "Coil", "Impulse", "Warp", "Phaser", "Operating", "Photon", "Deflector", "Integrity", "Control", "Bridge", "Dampening", "Display", "Beam", "Quantum", "Baseline", "Input"];
	
	const words3 = ["Chamber", "Interface", "Coil", "Polymer", "Biosphere", "Platform", "Thruster", "Deflector", "Replicator", "Tricorder", "Operation", "Array", "Matrix", "Grid", "Sensor", "Mode", "Panel", "Storage", "Conduit", "Pod", "Hatch", "Regulator", "Display", "Inverter", "Spectrum", "Generator", "Cloud", "Field", "Terminal", "Module", "Procedure", "System", "Diagnostic", "Device", "Beam", "Probe", "Bank", "Tie-In", "Facility", "Bay", "Indicator", "Cell"];

	console.log(words1[0]);
</script>
</head>
<body>
<p id="output">Loading...</p>
<button id="button">More Technobabble!</button>
	
</body>
</html>
```

- go ahead and copy the above code and save it as a file to your desktop - name it **technobabble.html**  

- https://love2dev.com/blog/javascript-strict-mode/
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode

- "The const declaration creates a read-only reference to a value. It does not mean the value it holds is immutable, just that the variable identifier cannot be reassigned."

## III. Review Questions


