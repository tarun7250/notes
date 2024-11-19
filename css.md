# Css



### display: grid;

#### grid-template-columns: min-content min-content min-content;
#### grid-template-rows: max-content max-content max-content max-content;
#### gap: 10px;
- min-content - wraps as the longest word
- max-content - makes everything in one line
- fit-content() - first max then min
- fr - first puts then arrages giving equal space if same number (fraction)
- minmax() -> min size and max size specified
- repeat(12, minmax(0,1fr));
- repeat(autofill/autofit, 200px) -> <br/>
auto-fill fills with childred <br/> auto-fit stretches the childrento fill <br/>
The default behavior of grid layout is to place items along the rows. You can instead cause the items to place into columns using `grid-auto-flow: column`<br/>
`writing-mode` vertical rl/lr<br/>
`grid-column-end: span 2;` to span in 2 columns similarly can be cone for rows
or may be `grid-column`

`grid-auto-flow: dense` to push 
```css
grid-column-start: 1; /* start at column line 1 */
grid-column-end: 4; /* end at column line 4 */
grid-row-start: 2; /*start at row line 2 */
grid-row-end: 4; /* end at row line 4 */
```

 you can use grid-column: 1 / -1. The item will stretch right across the explicit grid.
 1/2 means between line 1 and 2
can use custom naming of lines using square bracket
grid-template-colums: 
[line1 line2] 1fr
[line3 line4] 2fr;

can provide grid-area
```css
.header {
    grid-area: header;
}

.container {
    display: grid;
    grid-template-columns: repeat(4,1fr);
    grid-template-rows: repeat(3,1fr);
    grid-template-areas:
        "header header header header"
        "sidebar content content content"
        "sidebar footer footer footer";
}

```

This only works for the explicit grid howeve

   


### display: flex;
set by your flex-direction property. If that is row your main axis is along the row, if it is column your main axis is along the column.

row: the items lay out as a row.
row-reverse: the items lay out as a row from the end of the flex container.
column: the items lay out as a column.
column-reverse : the items lay out as a column from the end of the flex container.


The reordering only happens for the visual order, not the logical order. 



flex items behave by default is linked to the writing mode of the document.

writing-mode: vertical-rl;

normally overflows so use `flex-wrap: wrap`


flex-flow is short hand for flex-direction and flex-wrap
`flex-flow: column wrap`


flex-grow: 0: items do not grow.
flex-shrink: 1: items can shrink smaller than their flex-basis.
flex-basis: auto: items have a base size of auto.
This can be represented by a keyword value of flex: initial. The flex shorthand property, or the longhands of flex-grow, flex-shrink and flex-basis are applied to the children of the flex container.


flex: auto
flex-grow: 1: items can grow larger than their flex-basis.
flex-shrink: 1: items can shrink smaller than their flex-basis.
flex-basis: auto: items have a base size of auto.//actual size according to content


flex: 1
flex-grow: 1: items can grow larger than their flex-basis.
flex-shrink: 1: items can shrink smaller than their flex-basis.
flex-basis: 0: items have a base size of 0.

flex; 2 1 auto
flex-grow: 2
flex-shrink: 1
flex-basis: auto

#### flex-wrap
wrap,nowrap,wrap-reverse


#### order
can reorder items using attribute negative 0 and positive

justify-content: space distribution on the main axis.
align-content: space distribution on the cross axis.
align-items: aligns all of the items as a group on the cross axis.
place-content: a shorthand for setting both of the above properties.


align-self: aligns a single item on the cross axis.

flex-start 
flex-end
center

space-around -> half at the end and rest evenly
space-evenly -> full at the end evenly
space-between -> nothing at the end;




## selectors
### universal selector
```css
* {
    color: red;
}
```
selects everything
### type selector
```css
div {
    border: 2px solid;
}
```
adds in all types of same type
### class selector
```css
.my-class{
    color: red;
}
```
adds in all classes having this class
### id selector
```css
#idname {
    color: red;
}
```
select element with id
### attribute selector
[attribute=value]
[attribute]

```css
/* A href that contains "example.com" */
[href*='example.com'] {
  color: red;
}
/* A href that starts with https */
[href^='https'] {
  color: green;
}
/* A href that ends with .com */
[href$='.com'] {
  color: blue;
}

/* Sets all even paragraphs to have a different background */
p:nth-child(even) {
  background: floralwhite;
}
```

group selector using comma

```css
a.my-class {
  color: red;
}
```
> to apply to direct children
"space" to apply to all children
+ to apply to all the siblings

compound selectors
tag.attribute {}

## animations
### @keyframes

```css
@keyframes rotate {
    0%{
        transform: rotate(0);
    }
    50%{
        transform: rotate(180deg);
    }
    100%{
        transform: rotate(360deg);
    }
}
```
0% can be written as from <br/>
100% can be writtern as to <br/>

- animation : name
- animation-duration : time-to-complete-animation
- animation-timing-function : - (cubic , step)
- animation-iteration-count : - can be infinite
- animation-direction : normal, reverse, alternate, alternate-reverse
- animation-delay : after what time to start animation
- animation-play-state: paused/runing;
- animation : animation-name animation-duration animation-timing-function animation-delay animation-iteration-count animation-direction animation-fill-mode animation-play-state <br/>
animation-fill-mode property defines which values in your @keyframes timeline persist before the animation starts or after it ends. The default value is none, which means that when the animation is complete, the values in your timeline are discarded. Other options include:

forwards: The last keyframe persists, based on the animation direction.
backwards: The first keyframe persists, based on the animation direction.
both: Both the first and last keyframes persist.<br/>

## media queries
```css
@media print {
  body {
    background-color: transparent;
  }
}
@media (max-width: 400px) {
  // Styles for viewports narrower than 400 pixels.
}
@media (min-width: 50em) and (max-width: 60em) {
  // Styles for viewports wider than 50em and narrower than 60em.
}
@media (orientation: landscape) {
   // Styles for landscape mode.
}
@media (orientation: portrait) {
   // Styles for portrait mode.
}
```

## variable declaration in css
-- is strict requirement
```css
:root {
  --custom-color: pink;
}
body {
  background-color: var(--custom-color,red);
}
```
second argument is fallback<br/>
nesting like this <br/>
`var(--custom-color,var(--another-custom,--default-color))`

## font performance
font preload
font-display: swap/blocked
in link tag rel preload


## position 
- static - default,element will flow into the page as it normally would.only need when forcefully if because of  parent the positioning is persisting
- relative - first fits normally then according to top left bottom right positions it relative to normal doesnt changes other elements position (relative means relative to itself), use z-index on that element, which doesn’t work with statically positioned elements. Even if you don’t set a **z-index value**, this element will now appear on top of any other statically positioned element. You **can’t** fight it by setting a higher z-index value on a statically positioned element. **limits the scope of absolutely positioned child elements.**
- absolute - search for any parents that are positioned non statically(if not then root html element) 
- fixed - always fixed in viewport position according to top and bottom
- sticky - moves normally but fixes according to top and left


## specificity
id (1,0,0)
pseudo classes and elements (0,1,0)
rest (0,0,1)

## background-image
- by default background image is not scaled

### background-repeat

- no-repeat — stop the background from repeating altogether.
- repeat-x — repeat horizontally.
- repeat-y — repeat vertically.
- repeat — the default; repeat in both directions.
- space — repeat as many times as possible, adding space between the images if there is extra space available.
- round — similar to space, but stretches the images to fill any extra space

### background-size 
- cover — the browser will make the image just large enough so that it completely covers the box area while still retaining its aspect ratio. In this case, part of the image is likely to end up outside the box.
- contain - the browser will make the image the right size to fit inside the box. aspect ratio shall change

### background-position
uses the coordinate of box  top left is 0,0
```css
background-position: 20px 20%;
```

### background-attachment
how background scrolls relative to the content

- scroll - attached to the box
- fixed - fixed relative to viewport
- local - attached to the content of the box (both scroll inside the box)


 text-overflow: ellipsis;
background: radial-gradient(circle at 30% 70%, 
                                transparent 50px, 
                                rgba(0, 0, 0, 0.5) 50px);




- Constructing the Document Object Model (DOM) from the HTML.
- Constructing the CSS Object Model (CSSOM) from the CSS.
- Applying any JavaScript that alters the DOM or CSSOM.
- Constructing the render tree from the DOM and CSSOM.
- Perform style and layout operations on the page to see what elements fit where.
- Paint the pixels of the elements in memory.
- Composite the pixels if any of them overlap.
- Physically draw all the resulting pixels to screen.