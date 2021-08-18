# HW - Technobabble Generator II

## Overview

Let's make some changes the Technobabble app and review some commonly used web technologies

## I. Improve the mobile experience

First, let's modify the viewport meta tag to more reliably turn off page zooming on mobile devices - we'll do this by adding a `maximum-scale` directive. Change the `<meta>` tag from this:

`<meta name="viewport" content="width=device-width, initial-scale=1, userscalable=no">`

To this:

`<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1.0, userscalable=no">`
