# FORENSICS

Steganography
=============

* [Advanced JPEG Steganography and Detection by John Ortiz](https://www.youtube.com/watch?v=BQPkRlbVFEs)  

General helpful tools:

* stegsolve.jar
* pngcheck
* Recover file headers: http://foremost.sourceforge.net/

Other
=====

Phonetic analysis: praat www.fon.hum.uva.nl/praat

Often files need to be opened in HEX view.

Image file which hides something? Might be steganography, wrong extension, EXIF data.
General tips: is it BASE64 encoded?  
Try to run `xxd` - binary / hex view.  
`file`, of course, to find out some more about the file.

Nice trick with strings: `strings file.dat | grep flag{``


Comparing Files
---------------

There is a software called bindiff, not sure, looks like it's not free. diff should do the trick too.

For windows, there's a nice tool called FC.

Metadata
--------

* [FOCA](https://www.elevenpaths.com/labstools/foca/index.html) - tool for finding metadata and hidden information in the documents
* [Metagoofil](http://www.edge-security.com/metagoofil.php) - information gathering tool designed for extracting metadata of public documents belonging to a target company
* [ExifTool](http://www.sno.phy.queensu.ca/~phil/exiftool/) - tool for reading, writing and editing meta information in a wide variety of files


Data Recovery
-------------

* [Recuva](https://www.piriform.com/recuva)
