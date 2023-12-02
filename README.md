# Work with your favorite Master of the Universe

This is a practice project inspired by this [@MrNick_Buzz's tweet](https://twitter.com/MrNick_Buzz/status/1730257818035646729).

The resulting page is [visible here](https://lukeska.github.io/work-with-motu/).

Nick's design has a couple intersting details that were challenging to implement:

1. Connecting lines from the buttons to the main content box.
2. Gradient borders for buttons and the main content box.

## Curve connecting lines.

SVGs was the way to go to create connecting lines. Those SVGs needed to change depending on screen size.

To achieve that I used [this Javascript library](https://github.com/BrunoFenzl/svg-round-corners) that can take a path and add in the extra arcs to transform sharp angles into rounded corners.

## Gradient borders

Borders don't support gradient, so to achive that I user [background-origin property](https://www.w3schools.com/cssref/css3_pr_background-origin.php) to simulate a border through background color.
