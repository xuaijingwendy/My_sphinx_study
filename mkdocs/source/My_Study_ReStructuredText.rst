1.ReStructuredText
------------------------------------------------------
INline markup
------------------------------------------------------
.. code::
The standard reST inline markup is quite simple:use

 -  one asterisk:*text* for emphasis(italics),
 -  two asterisk:**text** for strong emphasis(boldface),and
 -  backquotes:``text`` for code samples

If asterisks or backquotes appear in running text and could be confused with inline markup delimiters,they have to be escaped with a backslash.

Be aware of some restrictions of this markup:

    it may not be nested,
    content may not start or end with whitespace:* text*is wrong,
    it must be separated from surrounding text by non-word characters.
    Use a backslash escaped space to work around that:thisis\ *one*\ word.

These restictions may be lifed in future versions of docutils.

It is also possible to replace or expand upon some of this inline markup with roles.

List and Quote-like blocks
--------------------------------------------------------------------

List markup(ref)is natural:just place an asterisk at the start of a paragraph and indent properly.The sam goes for numbered lists;they can alxo be sutonumbered using a # sign:

.. code::

* This is a bulledted list.
* It has two items,the second
  item uses two lines.

1. This is a mumbered list.
2. It has two items too.

#. This is numbered list.
#. It has two items too.

Nested lists are possible,but be aware that must be separated from ghr parent list items by blank lines:

.. code::

* this is
* a list

  * with a nested list
  * and some subitems
    
* and here the parent list continues

Definition list(ref)are created as follows:

term (up to a line of next)
   Definition of therm,which must be indented

   and can even consist of multiple paragraphs

next term
   Description.

Note that the term cannot have more than one line of text.

Quoted paragraphs(ref)are created by just indenting them more than the surrounding paragrphs.

Line blocks(ref)are a way of preserving line breaks:

.. code::

| These lines are
| broken exactly like in
| the source file.

There are also several more spvial blocks available:


   -  field list(ref,with caveats moted in Field Lists)
   -  option lists(ref)
   -  quoted literal blocks(ref)
   -  doctest blocks(ref)

Literal blocks
-------------------------------------------------------------

Literal code blocks(ref)are introduced by ending a paragraph with the special marker ::.The literal block must be indented(and,like all paragraphs,separated from the surrounding ones by blank lines):

This is mormal text paragraph. The next paragraph is a code sample::
   
   It is not processed in any way,except
   that the indentation is removed.

   It can span multiple lines.

This is amormal next paragraph again.

The handling of the :: marker is smart:
  -  If it occurs as a paragraph of its own,that paragraph is completely left ou     t of the document.
  -  If it is precede by whit espace,the marker is remoced.
  -  If it is preceded by non-whitespace,the marker is replaced by a single colo     n.


Doctest blocks
-------------------------------------------------------------
.. code::

>>> 1 + 1
2

Tables
-------------------------------------------------------------------

For *gride tables* (ref),you have to "paint" the cell grid yourself.They look like this:

.. code::

+--------------------------+------------+----------+----------+
|  Header row,column 1     | Header 2   | Header 3 | Header 4 | 
|  (header rows optional)  |            |          |          |
+==========================+============+==========+==========+
| body row 1,column 1      | column 2   | column 3 | column 4 |
+--------------------------+------------+----------+----------+
| body row 2               | ...        | ...      |          |
+--------------------------+------------+----------+----------+

*Simple tables* (ref)are easier to write,but limite:they must contain more than one row,and the first column cells cannot contain multple lines.They look like this:

.. code::

=====  =====  =======
A      B      A and B
=====  =====  =======
False  False  False
True   False  False
False  True   False
True   True   True
=====  =====  =======

Two more syntaxes are supported: *CSV tables* and *List tables* .
They use an *explicit markup block*.

**csv-table:**

.. csv-table:: Frozen Delights!
   :header: "Treat","Quantity","Description"
   :widths: 15, 10, 30

   "Albatross", 2.99, "On a stick!"
   "Crunchy Frog", 1.49, "If we took the bones out,it wouldn't be
   crunchy,now would it?"
   "Gannet Ripple", 1.99,"On a stick!"

**list-table:**

.. list-table:: Frozen Delithts!
   :widths: 15 10 30
   :header-rows: 1

   * - Treat
     - Quantity
     - Description
   * - Albaross
     - 2.99
     - On a stick!
   * - Crunchy Frog
     - 1.49
     - If we took the bones out,it wouldn't be
       crunchy,now would it?
   * - Gannet Ripple
     - 1.99
     - On a stick!
       

Hyperlinks
---------------------------------------------------------
.. code::

External Links
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++
Use `Link test <https://somain.invalid/>` _for inline web links.If the link text should be the web address,you don't need

Important
There must be a spaace between the link text and the opening<for the URL.

You can also separate the link and the target definition(ref),like this:

This is a paragraph that contains `a link`_.

.. code::

   .. _my_tag:

   news
   =============

   :ref:`http://www.baidu.com`

.. _a link: https://somain.invalid/

Internal links
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Internal linking is done via a special reST role provided by Sphinx,see the section on specific markup, `Cross-referencing arbitray locations`_.

.. _: https://zh-sphinx-doc.readthedoces.io/en/laest/markup/inline.html#ref-role

Section
-------------------------------------------------------------------

Section headers(ref)are created by underlining(and optionally oberlining)the section title with a punctuaation character,at least as long as the txt:

.. code::

=================
This is a heading
=================

Normally,there are no heading levels assigned to certain characters as the strucure is determined from the succession of headings.However,this conbention is used in Python's Style Guide for documentiong which you may follow:
 
.. code::

  - # with overline,for parts
  - * with overline,for chapters
  - =,for sections
  - -,for subsections
  - ^,for subsections
  - ",for paragraphs

Of course,you are free to use your own marker characters(see the reST documentation),and use a deeper nesting level,but keep in mind that most target formats(HTML,LaTex)have a limited supported nesting depth.

Field Lists
--------------------------------------------------------------------------

Field lists(ref)are sequences of fields marked up like this;

:fieldname: Field content

They are commonly used in Python documentation:

.. code::
 
def my_function(my_arg,my_other_arg):

    """A function just for me.

    :param my_arg: The first of my arguments.
    :param my_other_arg: The second of my arguments.

    :returns: Amessage (just for me, of course).
    """

Sphinx extends standard docutils behavior and intercepts field lists specified at the beginning of documents.Refer to Field Lists for mor information.

Roles
-----------------------------------------------------------------




Docutils supports the following roles:

.. code::

  - emphasis-equivalent of *emphasis*
  - strong-equivalent of **stong**
  - literal-equivalent if ``literal``
  - subscript-subscript text
  - superscript-superscript text
  - title-reference- for titles of books,periodicals,and other materials

Refer to Roles for roles added by Sphinx.

Directives
------------------------------------------------------------------------

Adirective(ref)is a generic block of explicit markup.Along with roles,it is one of the extension mechanisms of reST,and Sphinx makes heavy use of it.

Docutils supports the following directives:

.. code::
    
    - Admonitions: :dudir:`attention`, :dudir:`caution`, dudir:`danger`, dudir:'      error', :dudir:'hint`, :dudir:`important`, :dudir:`note`, :dudir:`tip`, :d      udir:'warning' and the generic :dudir:`admonition`.(Most themes style only      "note"and "warning"specially.)
    - Images:
      + :dudir:`image`
      - :dudir:`figure`
    - Additional body elements:
      +  :dudir:`contents<table-od-centents>`(a local,i.e. for the current file          only,table of contents)
      -  :dudir:`container`(an image with a custom class,useful to generate an           outer<div>in HTML)
      *  :dudir:`rubric`(a heading without relation to the document sectioning)

    - Special tables:

    - Special directives:

    -HTML specifics:

    -Influencing markup:


    Since these are only per-file,better use Sphinx's facilities for setting the    :dudir:`default_role`.

.. code::
    
   ** Warning**
   Do not use the directives :dudir:`sectnum`, :dudir:`header`and :dudir:`footer   `.

.. code::

.. function:: foo(x)
              foo(y,z)
   :module: some.module.name

   Retuen a line of text input from the user.

function is the directive name.It is given two arguments here,the remainder of the first line and the second line,as well as one option module(as you can see,options are giben in the lines immediately following the arguments and indicated by the colons).Options must be indented to the same level as the directive content.

The directive content follows after a blank line and is indented relative to the directive start.


Images
----------------------------------------------------------------

reST supports an image directive(ref),used like so:

.. code::

.. image::  gnu.png
   (options)

When used within Sphinx,the file name giben(here gnu.png)must either be relative to the source file,or absolute which means that they are relative to the top source directory.For example,the file **sketch/spam.rst** could refer to the image **images/spam.ong** as **../images/spam.png** or **/images/spam.png**.

Sphinx will automatically copy image files over to a subdirectory o fthe output directory on building(e.g.the_static directory for HTML output.)

Sphinx extends the standard docutils behavior by allowing an asterisk for the extension:

.. code::

.. image:: hnu.*

Note that image file names should not contain spaces.

*Changed in version 0.4*:Added the support for file names ending in an asterisk.
*Changed in version 0.6*:Image paths can now be absolute.
*Changed in version 1.5*:Iatex target supports pixels(default is 96px=1in).


Footnote
--------------------------------------------------------------------------------
.. code:: 

Lorem ipsum [#f1]_ dolor sit amet ... [#f2]_

.. rubric:: Footnotes

.. [#f1] Text of the first footnote.
.. [#f2] Text of the second footnote.
.. [1]<a id="id3"></a>
.. [2]
.. [#]
.. [#http://_]<a id="id5"></a>
.. [*]
.. [*]
.. [*]

Citations
--------------------------------------------------------------

.. code::

Lorem ipsum [Ref]_ dolor sit amet.

.. [Ref] Book or article reference, URL or whatever.

Citation usage is similar to footnote usage,but with a label that is not numeric or begins with #.

Substitutions
-------------------------------------------------------------------------------

.. code::

.. |name| replace:: replacement *text*

or this:

.. code::

.. |caution| image:: warning.png
             :alt: Warning!

Comments
------------------------------------------------------------------------

.. code::

.. This is a comment.

You can indent text after a comment start to form multiline comment:

..
 
  This whole indented block
  is a comment.
  
  Still in the comment.

2.Markdown
-----------------------------------------------------------------------------

 # First Class Title
 ## Second Class Title
 ### Third Class Title
 #### Foutth Class Title
 ##### Fifth Class Title
 ###### Sixth Class Title
 ####### Seventh Class Title


