Ganon
The Ganon library gives access to HTML/XML documents in a very simple object oriented way. It eases modifying the DOM and makes finding elements easy with CSS3-like queries. 

Ganon is:

A universal tokenizer
A HTML/XML/RSS DOM Parser
Ability to manipulate elements and their attributes
Supports HTML5
Supports invalid HTML
Supports UTF8
Can perform advanced CSS3-like queries on elements (like jQuery -- namespaces supported) 
A HTML beautifier (like HTML Tidy)
Minify CSS and Javascript
Sort attributes, change character case, correct indentation, etc.
Extensible
Parsing documents using callbacks based on current character/token
Operations separated in smaller functions for easy overriding
Fast
Easy
Ganon is designed for and written in PHP5, but there is also a PHP4 version available. All code in the repository is designed for PHP5 and a simple converter is used to make it compatible with PHP4. Although PHP4 isn't officially supported, a lot of features will still work with it. New bug reports for PHP4 will be taken into consideration and might be fixed if it doesn't require an overhaul of the current model. Learn more about using Ganon with PHP4. NOTE: Ganon is written in PHP version 5.3.1, if you are using a previous version of PHP5 and experience problems, please try the PHP4 version.




Quick start
First off, you need to download the latest version of Ganon.
 include('path/ganon.php');
 
 // Parse the google code website into a DOM
 $html = file_get_dom('http://code.google.com/');
After including Ganon and loading the DOM, it is time to get started.
Access
Accessing elements is made easy through the CSS3-like selectors and the object model.
 // Find all the paragraph tags with a class attribute and print the
 // value of the class attribute
 foreach($html('p[class]') as $element) {
   echo $element->class, "<br>\n"; 
 }


 // Find the first div with ID "gc-header" and print the plain text of
 // the parent element (plain text means no HTML tags, just the text)
 echo $html('div#gc-header', 0)->parent->getPlainText();


 // Find out how many tags there are which are "ns:tag" or "div", but not
 // "a" and do not have a class attribute
 echo count($html('(ns|tag, div + !a)[!class]');
Learn more about accessing elements.
Modification
Elements can be easily modified after you've found them.
 // Find all paragraph tags which are nested inside a div tag, change
 // their ID attribute and print the new HTML code
 foreach($html('div p') as $index => $element) {
   $element->id = "id$index";
 }
 echo $html;


 // Center all the links inside a document which start with "http://"
 // and print out the new HTML
 foreach($html('a[href ^= "http://"]') as $element) {
   $element->wrap('center');
 }
 echo $html;


 // Find all odd indexed "td" elements and change the HTML to make them links
 foreach($html('table td:odd') as $element) {
   $element->setInnerText('<a href="#">'.$element->getPlainText().'</a>');
 }
 echo $html;
Learn more about modifying elements.
Beautify
Ganon can also help you beautify your code and format it properly.
 // Beautify the old HTML code and print out the new, formatted code
 dom_format($html, array('attributes_case' => CASE_LOWER));
 echo $html;



Related Projects
PHP Simple HTML DOM - This project started because Simple HTML DOM didn't perform quite well for me with complex HTML.
phpQuery - This project started because phpQuery wasn't fast enough for me.
SimpleXML - PHP extension with similar functionality for XML only.
