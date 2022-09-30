# Topic: Objects and Classes 

# Goal

This programming assignment exercises how to construct abstract data types through implementing a finite data structure class in C++.  It also reviews operator overloading, and input/output including the friend concept.

# PPM Background

This program will implement an image class that will read, manipulate, and write basic PPM files.

# Format

A PPM file has the following format:

    P6  -- This is a magic number so that programs know this is a PPM file, these are literally the characters P and 6 (see https://en.wikipedia.org/wiki/List_of_file_signaturesLinks to an external site. for more details)
    <Number Of X Pixels> -- This is an integer
    Whitespace (eg, space, tab, new line, etc)
    <Number of Y pixels> -- This is an integer
    Whitespace (eg, space, tab, new line, etc)
    255 -- This is the maximum color value, 255 would be 8 bits of color, 65535 would be 16 bits of color (no more than 16 bits of color is allowed).  This is an integer
    Whitespace (eg, space, tab, new line, etc)
    <Red Value><Green Value><Blue Value> (and this is repeated XPixels across * YPixels down).  These are integers, not characters, but if the max color value is less than 256, these can only be 1 byte and if it is greater than or equal to 256, then these are two bytes each.  This means you will have to typecast the integer (typically 4 bytes) into the appropriately sized data type (eg, char ) -- https://en.cppreference.com/w/cpp/language/types

So the header of the PPM file for a 2x2 (4 pixel) image would look like this:

P6
2 2
255
128 0 128 128 0 128 128 0 128 128 0 128

Again, note that the 128 0 128 (just like all the values except "P6") is not the ASCII encoded 128 0 128, it is the actual (one byte because the max size is less than 256) value 128, not "1" "2" and "8" and the space that I have included is only to make it easier to read for you -- there is no actual " " character -- so you are going to do something like

output << (char) 128 << (char) 0 << (char) 128;

 

# Requirements

 

Your job is to implement a PPMImage class (and supporting classes) that has the following functionality:

 

# Constructor/Destructor:

Constructor -- Implement a default constructor.  Also implement constructors that accept a string containing a filename of the file to open.  Throw an exception if the file does not exist. Implement a copy constructor.  https://cplusplus.com/reference/cctype/isspace/Links to an external site.  may be useful when parsing the input file.

Destructor -- Clean up any dynamically allocated memory if necessary

# First Class Methods:

+ PPMLine -- appends a PPMLine object to the end of an existing image.  If the existing image has an X pixel value of 0, thrown an exception.  If the PPMLine object does not have the same X value as the existing image, throw and exception.
+ PPMImage -- Overlays the two images such that the resulting image has the x dimension of the image with the greater x dimension and the y dimension of the greater y dimension.  If the images have valid pixels, add the values together and modulo divide by the Maximum color size.  If one of the images doesn't have a pixel for a location, just use the value that does exist.

+= PPMLine -- Performs the + PPMLine functionality, but instead of returning a PPMImage, it modifies the existing image.

- PPMImage -- Removes the PPMImage from the existing image such that resulting image has the x dimension of the image with the greater x dimension and the y dimension of the greater y dimension.  If the images have valid pixels, subtract the second image value from the first and modulo divide by the Maximum color size.  If one of the images doesn't have a pixel for a location, just use the 0 minus the value that does exist under modulo division of the maximum color size.

- -- Returns an image so that every pixel has the value of Maximum color size - the original pixel value  (note that this is the unary operator -, not the subtraction operator)

<< -- Outputs the raw data (this needs to work for both file output and cout)

>> -- Reads the data from either a file stream or cin

== -- Returns true if the images are the same, otherwise false.
!= -- returns true if the images are different, otherwise false.

# Public Methods


void DrawLine(int startX, int startY, int endX, int endY, RGBValue color) -- Draws a line from (startX, startY) to (endX, endY) with the color of color.  If either point is outside the existing image, throw an exception.

void LoadFile(string) -- loads the PPM file with the name defined in the string.  If the file does not exist, throw an exception.

 Note that you may include other methods such as private helper methods as necessary.

 

# PPMLine Class

PPMLine should have a constructor that constructs a line given a vector of RGB values and a maximum color size --

struct RGBValue {
   int red=0;
   int green=0;
   int blue=0;
};


vector<RGBValue> lineInput;
RGBValue purple;
purple.red = 128;
purple.blue = 128;
for (unsigned short i = 0; i < 100; i++) {
    lineInput.push_back(purple);
}

PPMLine myline(lineInput, 255)

You many implement any other methods you need in PPMLine to make your program work.

 

 

# Turn in:

Submit the following in a ZIP file on canvas.

1) output (as text file, or captured image of console + the PPM images generated by the testfile ): This is the result with a given test file above.

2) PPMImage.h and PPMLine.h files

3) PPMImage.cpp and PPMLine.cpp files

3) PPMDriver.cpp and RGBValue.h (Do Not Modify)

4) execute.sh (Do Not Modify)

5)  (optional) readme.txt --   If anything is not complete or had to be changed in PPMDriver.cpp or execute.sh, explain that here.

Make sure that your program can be compiled and executed on the linux lab machines.

 

# Grading Guide 

    Correctness (78 points)

Compilation errors in Linux (0 points)

Each method + the PPMLine class that is correctly implemented is worth 6 points. 

  

    Program Organization (22)

   Proper comments (Every method has to be commented in the header and implementation file)

   Good (7)       Poor(3)        Almost non-existent (0)

 

   Coding style (proper indentations, blank lines, variable names, and non-redundant code)

  Good (7)       Poor(3)        Almost non-existent (0)

 

   Proper Git etiquette (Frequent commits, informational commit messages)

  Good (8)       Poor(4)       Almost non-existent (0)
