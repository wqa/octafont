# Octafont

Pixelfont designed for flipdot matrices. Each text line has a height of 8 pixels and the characters, in favor of a natural appearance, have variable width (1 to 6 pixels).The bottom most pixel line is kept free by normal letters and only used by letters that go below the baseline, as for instance "g" or "q". A bold and a normal version is available.

The font for usage in C++ programs (it makes use of object oriented language) is generated by a python script `mkfont.py` which in turn reads the data from an image file. This way it is easy to adapt the font or to create completely new fonts. Using the generated C++ files, the font can be included in the program in hardcoded form.

Currently, the font generator is configured such that it provides all printable ASCII characters (from decimal 33 to decimal 126) and some german special letters from the upper block (greater than decimal 127). The german characters are encoded according to ISO 8859-15 (also called Latin 9). 

# The Font

The C++ pixelfont's interface is defined by its parent class `PixelFont`. It offers three basic methods for accessing the pixeldata:

* `has_char` determines whether a certain character is included in the font
* `get_width` returns the width in columns of the given character
* `get_octet` provides the pixel data for the given character and the given column index

The pixel data is stored and provided as `uint8_t` where the least significant bit is the topmost in the column. Each column has therefore a height of 8 pixels and that's why it is called octafont.

# The Generator

The generator is a python script which only needs [PIL/Pillow](https://pypi.org/project/Pillow/) as extra dependency. Therefore no `requirements.txt` is provided. Calling reads the image data and writes the C++ source and header file to the folder `output` in the current working directory. If the output folder does not exist, it is created.

The image pixel data itself is rather self explanatory. It includes two lines of characters, one for the normal variant and one for the bold variant. Each line has a height of 8 pixels and a special line of pixels above, which encodes the beginnings and endings of the characters. A red pixel marks the beginning of the character, a green pixel its end.
