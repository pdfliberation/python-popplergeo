python-popplergeo
=================

module to convert pdftotext bbox xhtml output to geojson

interop requirements
====================
 - poppler >= 0.20.5

obtaining poppler xhtml output
==============================

The `-bbox` flag of `pdftotext` will output XHTML with bounding box information as well as some meta information and the size of the page.
    
    pdftotext -r 150 -bbox original_document.pdf output.html

The `-r` flag sets the resolution that poppler is supposed to assume, in dots per inch (DPI). The default is 72. It doesn't really matter what you choose, and so far there's no reason to assume that 150 is a particularly good value. The important thing is that you choose the *same* value when generating an image file for display purposes (to ensure that your bbox coordinates match the pixels in the image).

    pdftoppm -r 150 -png original_document.pdf output.png

troubleshooting
===============

# Why is the size of the page tag smaller than the range of my bounding box coordinates?
This seems to be a bug in earlier versions of poppler, having to do with the difference between the dimensions of the MediaBox and the dimensions of the CropBox. This was apparently addressed by the 0.20 release. Note that the version of poppler that is packaged for Ubuntu 12.04 (precise) is 0.16.4, and will give dimensions of the page that do not correspond to the range of values of bounding boxes.
