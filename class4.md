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
* When the <aside> element is used outside of an <article> element, it acts as a container for content that is related to the entire page and might contain links to other sections fo the site, list of recent posts, a search box or recent tweets by the authoer

