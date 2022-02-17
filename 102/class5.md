### How is CSS used?
* typically saved as .css formate, and link to using an HTML tag
* CSS seletors can be used to address parts of the page to style and use
* HTML elements are given **Class and ID** attributes, which are then used to manipulate in CSS
* typlically follows this method: Select, the Edit

### CSS selectors (Class and Element)
* selectors are ways of grabbing and manipulating HTML elements <body> <header> <p> exampe: body { color; red }
* many different ways to select, however they all turn out the same way- some are more effiecient to read and process
*  diff selectors have diff applications

## Element Selectors
* you can select entire elements without any special character
* applies to all of the element with that tag on the page
* It ranks on the bottom of the specificity scale
* <p> {color; red}

## Class and ID Selectors
* used to select elements with a certain class name 
* can be used on any and all elements with that class
* can be used multipe times, and is select with the .symbol 
* <h2 class="aclass">A Subheading.</h2>   
* <p class="acalss">Some more text.</p>
* <p id="sometext">Some Text.</p>  #sometext {color: blue;}
* class

### CSS Color 
* 3 common ways to specify colors RGB, HEX or color names
* Color terminology- terms that are helpful to understand when picking colors 
* Background colors for behind entire page or just part of page

### Foreground Color 
* Color property allows you to specify color of text inside element
* RGB Values: express colors in terms of how much red, green and blue: rgb (100, 100, 90)
* HEX Codes: six-digit codes that represent the amount of RGB, preceded by a # sign: #ee3e80
* Color Names: 147 colors names are recognized by browser (DarkCyan)

### Background Colors 
* CSS treats each HTML element as if it appears in a box and background color property sets color for that box: body/h1/h3/p { background-color: rgb(200, 200, 200);}
* specify BG color in the same 3 ways you specify FG colors
* if you do not specify BG color then BG is transparent
* by default most browser windows have white BG <body> element 
* Padding property to sept the text from edges of the boxes 

### Understanding Color 
* every color on a computer screen is created by mixing RGB
* computer monitors are made up of thousands of tiny squares/pixels
* each pixel is expressed in terms of a mix of RGB
* color picking tools are available in image editing programs like photoshop and GIMP
* RGB Values- values for RBG are expressed as number between 0 and 255 (rgb 102, 205, 160)
* HEX Codes- values represtn values for RBG in hexadecimal code (#66cdaa)
* COLOR Names- represented by predifined names and limted in numbers (MediumAquaMarine)
* HUE- hue is near to the colloquial idea of color
* Staturation refers to the amount of gray in a color. At maximum sat, there would be no gray in the color, at min sat the color would be mostly gray 
* Brightness refers to how much black is in a color 
* Contrast- when picking foreground and background colors, it is important to ensure that there is enough contrast for the text to be legible
* CSS3 opacity property allows you to specify the opacity of an element and any of it's child elements (0.0 and 1.0) 0.5 being 50% opacity 

### CSS3: HSL Colors 
* CSS3 introduces a new and intiutive way to specify colors using hue, saturation and ligthness values
* Hue is the colloquial idea of color and is often represented as a color cirle
* Saturation is the amouth of gray in a color as percentages full sat 100%- 0% which is a shade of gray
* Lightness, sometimes refferred to as luminosity, is the amount of white or black in a color. 0% equals black and 100% equal white. Lightness is a different concept to brightness.  
*  HSL and Hsla <hsl>, <hsla> The hsl color property has been introduced in CSS3 as an alternative way to specify colors. The value of the property starts
with the letters hsl, followedby individual values inside
parentheses for: hue This is expressed as an angle
(between 0 and 360 degrees)
* Hue is expressed as an angle between 0 and 360 dgress
* Saturation is expressed as a percentage
* Lightness is expressed as a percentage with 0% being white, 50% normal and 100% black 
* Alpha is expressed as a number between 0 and 1.0

