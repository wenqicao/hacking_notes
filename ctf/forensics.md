# FORENSICS

Often files need to be opened in HEX view.

Image file which hides something? Might be steganography, wrong extension, EXIF data.
General tips: is it BASE64 encoded?

Try to run xxd - binary / hex view.
"file", of course, to find out some more about the file.

Nice trick with strings: `strings file.dat | grep flag{``


Comparing Files
---------------

There is a software called bindiff, not sure, looks like it's not free. diff should do the trick too.

For windows, there's a nice tool called FC.
