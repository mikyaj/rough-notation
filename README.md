![Rough Notation logo](https://roughnotation.com/images/social.png)

# Rough Notation

A small JavaScript library to create and animate annotations on a web page.

Rough Notation uses [RoughJS](https://roughjs.com) to create a hand-drawn look and feel. Elements can be annotated in a number of different styles. Animation duration and delay can be configured, or just turned off.

Rough Notation is 3.63kb in size when gzipped.

[Visit website to see it in action](https://roughnotation.com/) and check out the [source code](https://github.com/pshihn/rough-notation-web) for the website

## Installation

You can add rough-notation to your project via npm

```
npm install --save rough-notation
```

Or load the ES module directly

```html
<script type="module" src="https://unpkg.com/rough-notation?module"></script>
```

Or load the IIFE version which created a `RoughNotation` object in your scope.

```html
<script type="module" src="https://unpkg.com/rough-notation/lib/rough-notation.iife.js"></script>
```

## Usage

Create an `annotation` object by passing the element to annotate, and a config to describe the annotation style. 
Once you have the annotation object, you can call `show()` on it to show the annotation

```javascript
import { annotate } from 'rough-notation';

const e = document.querySelector('#myElement');
const annotation = annotate(e, { type: 'underline' });
annotation.show();
```

*Note: This will add an SVG element as a sibling to the element, which may be troublesome in certain situations like in a `<table>`. You may want to create an inner `<span>` or `<div>` for the content to annotate.*

## Annotation Group

rough-notation provides a way to order the animation of annotations by creating an annotation-group. Pass the list of annotations to create a group. When show is called on the group, the annotations are animated in order.

```javascript
import { annotate, annotationGroup } from 'rough-notation';

const a1 = annotate(document.querySelector('#e1'), { type: 'underline' });
const a2 = annotate(document.querySelector('#e3'), { type: 'box' });
const a3 = annotate(document.querySelector('#e3'), { type: 'circle' });

const ag = annotationGroup([a3, a1, a2]);
ag.show();
```

## Configuring the Annotation

When you create an annotation object, you pass in a config. The config only has one mandatory field, which is the `type` of the annotation. But you can configure the annotation in many ways. 

#### type
This is a mandatory field. It sets the annotation style. Following are the list of supported annotation types:

* __underline__: Create a sketchy underline below an element.
* __box__: This style draws a box around the element.
* __circle__: Draw a circle around the element.
* __highlight__: Creates a highlight effect as if maked by a highlighter.
* __strike-through__: This style draws a box around the element.
* __crossed-off__: This style draws a box around the element.

#### animate
Boolean property to turn on/off animation when annotating. Default value is `true`.

#### animationDuration
Duration of the animation in milliseconds. Default is `800ms`.


#### animationDelay
Delay in animation in milliseconds. Default is `0ms`.


#### color
String value representing the color of the annotation sketch. Default value is `currentColor`.

#### strokeWidth
Width of the annotation strokes. Default value is `1`. 

#### padding
Padding between the element and roughly where the annotation is drawn. Default value is `5` (in pixels).
If you wish to specify different `top`, `left`, `right`, `bottom` paddings, you can set the value to an array akin to CSS style padidng `[top, right, bottom, left]` or just `[top & bottom, left & right]`.

#### iterations
By default annotations are drawn in two iterations, e.g. when underlining, drawing from left to right and then back from right to left. Setting this property can let you configure the number of iterations. 

## Annotation Object

When you call the `annotate` function, you get back an annotation object, which has the following methods:

#### isShowing(): boolean
Returns if the annotation is showing

#### show()
Draws the annotation. If the annotation is set to animate (default), it will animate the drawing. If called again, it will re-render the annotation, updating any size or location changes. 

*Note: to reanimate the annotation, call `hide()` and then `show()` again.

#### hide()
Hides the annotation if showing. This is not animated. 

#### remove()
Unlinks the annotation from the element. 

#### Updating styles
All the properties in the configuration are also exposed in this object. e.g. if you'd like to change the color, you can do that after the annotation has been drawn.

```javascript
const e = document.querySelector('#myElement');
const annotation = annotate(e, { type: 'underline', color: 'red' });
annotation.show();
annotation.color = 'green';
```

*Note: the type of the annotation cannot be changed. Create a new annotation for that.*

## Annotation Group Object

When you call the `annotationGroup` function, you get back an annotation group object, which has the following methods:

#### show()
Draws all the annotations in order. If the annotation is set to animate (default), it will animate the drawing. 

#### hide()
Hides all the annotations if showing. This is not animated.

## Wrappers

Others have created handy Rough Notation wrappers for multiple libraries and frameworks:

-   [React Rough Notation](https://github.com/linkstrifer/react-rough-notation)
-   [Svelte Rough Notation](https://github.com/dimfeld/svelte-rough-notation)
-   [Vue Rough Notation](https://github.com/Leecason/vue-rough-notation)
-   [Web Component Rough Notation](https://github.com/Matsuuu/vanilla-rough-notation)
-   [Angular Rough Notation](https://github.com/mikyaj/ngx-rough-notation)
