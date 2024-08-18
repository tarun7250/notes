elemtent = opening tag + content + closing tag

### role attribute 
for better semantics and accessibility object model

Using `</nav>` and `</header>` closing tags removes the need for comments to identify which element each end tag closed. In addition, using different tags for different elements removes the need for id and class hooks. The CSS selectors can have low specificity; you can probably target the links with header nav a without worrying about conflict.

same with `<footer>` role contentinfo

```
<header> - role=banner 
<nav> - role=navigation
<footer> - role=contentinfo
<aside> - role=complementary
<main> - only one is allowed
<dt> - role=term
<dd> - role=definition
```
Chrome shows it as FooterAsNonLandmark; Firefox shows it as section

### anchor tag
`<a href="https://www.google.com">google</a> ` http:// shows protocol if // protocol is left then will follow the same as this <br/>
relative url does not need protocol or domain name

#### link fragment \#
`href="#top"` will go to top (browser support) unless element with id top
- href attribute can begin with mailto: or tel: to email or make calls
<br/> \<a href="mailto:?subject=Join%20me%21&body=body">mail</a>
- ? separates mail and subject and & separates fields
- download attribute to suggest a file name for the downloadable blob <br/>

#### target
`target="_blank"` opens new tab everytime , but with case sensitive values reloads the same tab not new tab

#### rel
- nofollow - not receive any "link juice" or ranking credit from the linking page, which can affect search engine optimization (SEO)
- external
- help
- alternative <br/>


#### ping
can track if link is clicked using ping attribute , post request with ping body

#### alt
description of accessible name

<br/>
in javascript
links attribute returns an HTMLCollection matching a and area

```js
a.href = 'newpage.html'; 
a.protocol = 'ftp'; 
a.setAttribute('href', 'https://machinelearningworkshop.com/'); 
```

## lists

### ol - ordered list

::marker element
### li - list items
used inside ordered list
#### value
gives exact value to the list item 


#### type
- change type from here , i , A ... <br/>
list-style-type in style can have many different values

#### reversed
reverses order
#### start
starts with that particular number..

### ul - unordered list

### description list - dl
consists of key value pair
description terms\<dt> and description details\<dd>

## navigation
### nav
- the pages the user followed to get to the current page, is called a `breadcrumb`.
- every page - site navigation, top level page - global navigation
- current page is also identified with the aria-current="page"
<br/>
`CSS display: none` tab skips

## forms
### form
#### novalidate 
novalidate attributes does not validate the contents of the form
#### action
url where data send - by defaults get sent to current page
form as name/value pair
#### method
POST, GET ....
`formmethod = "dialogue"` closes the dialoge <br/>
If the button includes a formaction, formenctype, formmethod, formnovalidate, or formtarget attribute, the values set on the button activating the form submission take precedence over the action, enctype, method, and target set on the <form>

### input
#### type
22 types
text, file, radio ...
#### name=""
specifies name
#### value=""
specifies value
#### required
if this attribute is there then does not allows to submit
:required and :valid/:invalid pseudo classes will match in cases
#### min, max, minlength, maxlength, pattern
these invokes particlar kind of classes

## tables
### table indicate table (aria role - table) if collapsable implicitly - treegrid
### caption
for table title
### colgroup
defines column groups by the help of col tag and span
### col
- span defines number of columns in the group

### thead
table header
### tbody
body
### tr
table row
### th
head in row or column based on scope attribute
#### scope
#### rowspan / colspan
if row is spanned 
### td
table data or cell
### tfoot

## images

### img
#### src 
image source
#### alt
alternative if not able to load image source
#### loading="lazy"
for lazy loading images
#### srcset 
attribute enables providing multiple image versions based on resolution and, along with the sizes attribute, browser viewport size.<br/>
If the image is of SVG file type, also include role="img", which is necessary due to VoiceOver bugs.
### picture 
can have multiple source
### source
srcset for multiple


## videos
### video
series of \<source> elements, each providing a src file <br/>
controls, autoplay, loop, mute, preload, and the global attributes. The \<video> element also supports the height, width, and poster attributes.
<br/>
`<source src="videos/machines.webm" type="video/webm">`

### control

### track
between video provides subtitles






  










