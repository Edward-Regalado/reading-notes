### Class4 notes

## New Vocabulary
* HTML / Markup
* Semantics
* Wireframe
* Personas
* Meta
* Content
* Element
* Tag
* Attribute
* Structure vs Presentation

### NOTE from class
### TAGs - 
* h1, h2, h3, ol, ul, li, article, section, button all have semantic meaning
* all elements are contained in <example> and closing </example> 
* images do not need an closing </>
* attribute <section class="news">

* 
### NOTES from class

### HTML5 LAYOUT 
* layout elements 
* How old broswers understand new elements
* Styling HTML5 layout elements w/CSS

### Headers & Footers
* Main header <header> or footer <footer>  
* used at the top and bottom of every page on site
* Used for an individual <artical> or <section> within the page
* Website with serveral blog posts, each blog post can ve viewed as a seperate section
* The <header> element can therefore be used to contain the title and date of each post
* The <footer> might contain links to share the article on scoial networking sites

* **Example** 
    <header>
    <h1>Yoko's Kitchen</h1>
    <nav>
    <ul>
    <li><a href=""> class="current">home</a></li>
    <li><a href="">classes</a></li>
    <li><a href="">catering</a></li>
    </ul>
    </nav>
    </header>

    <foooter>
        &copy: 201 Yoko's Kitchen 
    </footer>


### Navitgation <nav>

* the <nav> element is used to contain the major navigational blocks on the site such as the **PRIMARY**  site nav
* Genearlly, links at the bottom of a webpage (in the <footer> section) used for policy, terms, contact, etc. are not considered primary <nav> links and should remain outside of the main <nav> element

### Articles <article>

* The article <article> element acts as a contrainer for any section of a page that can stand alone and potentially be syndicated
* Such as an individual article or blog entry, a comments or forum post, or any other independent piece of content
* Pages with multiple articles will each have its own <artilce></article> element 
* The article element can even be nested within each other 

### Asides <aside>
* The <aside> element has two purpose depending on whether it is inside an <article> element of not
* When the <aside> element is used inside an <article> element, it should contain info that is related to the article but not essential to its overall meaning
* When the <aside> element is used outside of an <article> element, it acts as a container for content that is related to the entire page and might contain links to other sections fo the site, list of recent posts, a search box or recent tweets by the author

### Sections <section>
* the <section> element groups related contecnt toegher, and typically each section would have its own heading 
* There may be serveral <section> elements on a homepage
* groups related items together, it may contain several distinct <article> elements that have a common theme or purpose
* used to split up long articles into seperate sections
* the <section> element should not be used as a wrapper for the entire page (unless page contains on distinct piece of content)

### Heading Groups <hgroup>
* purpose is to group together a set of one or more <h1> through <h6> elements so that they are threated as one single heading
* Use <hgroup> as container element for <h1> through <h6> elements

### Figures <figure> <figcaption>
* used to contain any content that is referenced from the main flow of an article (not just images)
* make sure article still makes sense if <figure> element were moved to another part of the page or entire new page
* only used when the content simply references the element (images, videos, graphs, diagrams, code samples, text that support main body of article)
* <figure> element should contain a <figcaption> which provides a text description for the content of the figure

### Sectioning Elements <div>
* important way to group together related elements
* <div> is used when there is no suitible way to group a set of elements
* used as a wrapper for the entire page

### Linking around block-level elements 
* HTML5 allows web page authors to place an <a> element aroud a block level element that contains child elements 
* this is not a new element in HTML5, but it was not seens as a correct usage of the <a> element in earlier version of HTML 

### Helping older browser understand 
* older browsers do not know HTML5 elements will automatically treat them as inline elements so include the line of CSS on the left wich states which new elements should be rendered as blocl-level elements 
* header, section, footer, aside, nav, articl, figure {
    display: block; 
} 
* To make HTML5 elements works on older browsers, extra javascript is needed, which is available free from Google


