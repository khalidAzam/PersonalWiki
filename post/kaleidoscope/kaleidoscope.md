## [原創] Kaleidoscope [Back](./../post.md)

<p align="center"><img src="./preview.png" alt="kaleidoscope" /></p>
<p align="center"><strong>Figure 1</strong> A simple preview of kaleidoscopes</p>

In Chinese, we will name kaleidoscopes as "萬花筒", which is a toy showing colorful shapes of thousands of flowers. Today, inspired by the project, [spring loaders](https://github.com/claudiocalautti/spring-loaders), I have tried myself to create a similar component with CSS and SVG, rather than Canvas. As the Figure 1 shown, that's my **kaleidoscope**.

### Introduction

Without reading the article, I have just created it through several processes. How to create, how to create regular polygons, and how to make it reusable for all kinds of regular polygons.

#### How to create?

At the start, I have utilized the feature of `div`, which is an HTML elements with a shape of rectangles. With setting a same value for the property `width` and `height` of these elements, I can easily generate a square like the first item from the left side in the Figure 1.

Then, to simulate such rotating animation, I would like to use `transform` and `transform-origin` property to implement it, rather than use Canvas, as Canvas is something complicated, which has been always confusing me.

```css
.item {
    transform: scale(0.5) rotateZ(45deg);
    transform-origin: center;
    
    /** other browsers */
    -webkit-transform: scale(0.5) rotateZ(45deg);
    -webkit-transform-origin: center;
    
    -moz-transform: scale(0.5) rotateZ(45deg);
    -moz-transform-origin: center;
    
    -ms-transform: scale(0.5) rotateZ(45deg);
    -ms-transform-origin: center;
    
    -o-transform: scale(0.5) rotateZ(45deg);
    -o-transform-origin: center;
}
```

The code snippet above has shown us how to use such two properties to animate our elements. With setting `scale(0.5)` and `rotateZ(45deg)`, the element will be scaled by half, and rotate 45 degrees clockwise.

If using JavaScript to change this value dynamically, we can code like this:

```js
/** sita is the rotating degree */
const sita = 45; 
const scale = 0.5;
const target = document.querySelector('.item');

target.style.transformOrigin = 'center';
target.style.transform = 'scale(' + scale + ') rotateZ(' + sita + 'deg)';

/** other browsers */
target.style.WebkitTransformOrigin = 'center';
target.style.WebkitTransform = 'scale(' + scale + ') rotateZ(' + sita + 'deg)';

target.style.MozTransformOrigin = 'center';
target.style.MozTransform = 'scale(' + scale + ') rotateZ(' + sita + 'deg)';

target.style.MsTransformOrigin = 'center';
target.style.MsTransform = 'scale(' + scale + ') rotateZ(' + sita + 'deg)';

target.style.OTransformOrigin = 'center';
target.style.OTransform = 'scale(' + scale + ') rotateZ(' + sita + 'deg)';
```

<p align="center"><img src="./figure2.png" alt="kaleidoscope" /></p>
<p align="center"><strong>Figure 2</strong> The relationship between sita and scale</p>

Then as the Figure 2 shown, how to calculate a proper value of ***a*** for `scale` with ***θ*** for `sita` as the variable, in order that vertexes of the item can stay on each side of another square? We may just have to solve the following equation:

<p align="center"><img src="./mathtran1.png" alt="kaleidoscope" /></p>

After calculating, we can easily get that:

<p align="center"><img src="./mathtran2.png" alt="kaleidoscope" /></p>

Then, for the first item, I have implement by the following code:

```js
/** the difference of degree in each duration */
const stepT = 0.5;

/** the time (ms) to update the sita value /
const dur = 10;
const num = 6;

var t = 0;
var dir = 1;

for (var i = 0; i < num; i++) {
	var div = document.createElement('div');
	div.className = 'rect rect' + (i + 1);
	document.querySelector('.rect' + i).appendChild(div);
}

setInterval(function () {
	t += stepT * dir;
	t = t % 90;

	if (t === 0) {
		dir *= -1;
	}

	var tan = parseFloat(Math.tan(Math.abs(t) * Math.PI / 180).toFixed(2));
	var scaleRatio = Math.sqrt(1 + tan * tan) / (1 + tan);

	for (var i = 0; i < num; i++) {
		document.querySelector('.rect' + (i + 1)).style.transform = 'scale(' + scaleRatio + ') rotate(' + t + 'deg)';
	}
}, dur);
```

### Demo

<p>
<p data-height="568" data-theme-id="21735" data-slug-hash="mOzbWW" data-default-tab="result" data-user="aleen42" data-embed-version="2" data-pen-title="mOzbWW" class="codepen">See the Pen <a href="http://codepen.io/aleen42/pen/mOzbWW/">mOzbWW</a> by aleen42 (<a href="http://codepen.io/aleen42">@aleen42</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>
</p>

