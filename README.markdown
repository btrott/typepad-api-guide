TypePad API Guide
=================

To generate HTML with code highlighting and a table of contents, use
[Python Markdown](http://www.freewisdom.org/projects/python-markdown/)
with the codehilite and toc extensions:

    markdown -x codehilite -x toc guide.markdown > guide.html