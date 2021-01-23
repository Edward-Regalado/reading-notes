## Daily Reading Notes 5

## Chapter 5: Images (p.94-125)
- be relevant, convery info + right mood, fit the color palette
- if build a site from scratch, it is good pratice to create a folder for all of the images the site uses
- use sub folders inside images folder 
- use <img> element to add an image into the page- it's an empty element so no closing tag <img src="image location" alt="description of image" title="aditional information" width="500" height="450" />
- where you place the image in the code is important because browsers show HTML elements in block and block inline elements.
- align="right/left" used to incidate how other parts of page should flow around an image (no longer used in HTML5)
_ align="top/middle/bottom" aligns first line of text to image 
- 3 rules for creating images - save images in the right format, save images at the right size, use the correct resolution. 
- use adobe photoshop to edit images 
- use jpeg when images has lots of different colors
- use GIF or PNG format when saving images with few colors or large areas of the same color 
- save images at the same width and height that you intend to use on your page
- Images created for the web should be saved at 72 ppi. 
- vector images differ from bitmap images and are resolutoin-independent
- GIFs show several frames of an images in sequence and therefore can be used to create simple animations
- <figure> element to contain <img> and their <figcaption> so that the two are associated
- <figcaption> allows web page authors to add a caption to an image


## Chapter 11: Color (p.246-263)
- Color property allows you to specify the color of text inside an element (RGB, HEX codes or color names). 
- CSS treats each HTML element as if it appears in a box, and background-color property set the color of the background for that box. 
- RGB values for red, green, and blue are expressed in number between 0 and 255. 
- HEX Codes values for red, gree, and blue in hexadecimal code #66cdaa
- Color names are predefined and are limited. 
- When picking a foreground and background colors, it's important to ensure that there is enough contract fro the text to be legible
- Opacity property allows you to specify the opacity of an element and any of its child elements (0.0 and 1.0 or 0-100%). 
- HUE is expressed as an angle between 0-360 degrees. 
- Saturation is express as a percentage
- Lightness is expressed as a percentage with 0% being white, 50% being normal and 100% being black. 
- CSS3 introduced HSLA which adds alpha for (transparency).
-
## Chapter 12: Text (p. 264-299)
- Formatting of your text can have a significant effect on how readable your pages are.
- monospace font is the same width and commonly used for code because they align nicely. 
- SERIF fonts have extra details on the end of the main strokes of the letters
- SANS_SERIF have straight ends to letters and therefore have a much cleaner design. 
- font-family property allows you to specify the typeface that should be used for any text inside the elements to which a CSS rule applies.
- If a font name is made up of more than one word, it should be put in double quotes
- Designers suggest not using more than 3 typefaces on a page. 
- font-size property allows you to specify a size for the font. 
- Pixels are commonly used because they allow very precies control over how much space their text takes up.
- Percentages- the default size of text in browsers in 16px. So a size of 75% would be 12px, and 200% would be 32px. 
- EMS - an EM is equivalent to the width of a letter m. 
- 8pt, 9pt, 10pt, 11pt, 12pt, 14pt, 18pt, 24pt, 36pt, 48pt, 60pt, 72pt this scale of font-size is most pleasing to the eye.
- Setting font size if pixels is the best way to ensure that the type appears at the size you intended.
- @font-face allows you to use a font, even if it is not installed on the computer of the person browsing.
- font-weight property allows you to create bold text. Normal and Bold. 
- font-style property allows you to create italic text. 
- text-transform - used to change the case of text giving it one of the following values: uppercase, lowercase, capitalize. 
- text-decoration - none, underline, overline, line-through, blink.
- line-height - increasing this makes vertical gap between lines of text larger.
- letter-spacing & word-spacing- used to control space between each letter and/or word. Recommended to use EMs to specify a value for these properties.
- text-align - allows you to control the alignment of text. text-aling: left, right, center or justify. 
- Justity indicates that every line in a paragraph, except the last line, should be set to take up the full width of the containing box. 
- Vertical-align - commonly used with inline elements such as <img>, <em>, or <strong> elements. It is not intended to allow you to vertically align text in the middle of block level elements such as <P> and <div>. 
- text-indent property allows you to indent the first line of text within an element, usually represented in pixels or ems. 
- text-shadows property created a drop shadow, which is a dark version of the word just behind it and slightly offset. 
- :link, :visited are two pseudo-classes that allow you to set different styles/colors for links
