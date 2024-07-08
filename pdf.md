# PDF notes

Hand-made PDF source code by [Alex Chan](https://alexwlchan.net/2024/big-pdf/)
(_licensed under MIT_)
of a simple red square, with detailed explanatory comments:

<!-- No relevant syntax highlighter available for PDF source code. -->
<!-- Choosing "raku" gives a "better that nothing" rendering, at least better than "c" or "sql". -->
```raku
%PDF-1.6

% The first object.  The start of every object is marked by:
%
%     <object number> <generation number> obj
%
% (The generation number is used for versioning, and is usually 0.)
%
% This is object 1, so it starts as `1 0 obj`.  The second object will
% start with `2 0 obj`, then `3 0 obj`, and so on.  The end of each object
% is marked by `endobj`.
%
% This is a "stream" object that draws a shape.  First I specify the
% length of the stream (54 bytes).  Then I select a colour as an
% RGB value (`1 0 0 RG` = red), then I set a line width (`5 w`) and
% finally I give it a series of coordinates for drawing the square:
%
%     (100, 100) ----> (200, 100)
%                          |
%     [s = start]          |
%         ^                |
%         |                |
%         |                v
%     (100, 200) <---- (200, 200)
%
1 0 obj
<<
	/Length 54
>>
stream
1 0 0 RG
5 w
100 100 m
200 100 l
200 200 l
100 200 l
s
endstream
endobj

% The second object.
%
% This is a "Page" object that defines a single page.  It contains a
% single object: object 1, the red square.  This is the line `1 0 R`.
%
% The "R" means "Reference", and `1 0 R` is saying "look at object number 1
% with generation number 0" -- and object 1 is the red square.
%
% It also points to a "Pages" object that contains the information about
% all the pages in the PDF -- this is the reference `3 0 R`.
2 0 obj
<<
	/Type /Page
	/Parent 3 0 R
	/MediaBox [0 0 300 300]
	/Contents 1 0 R
>>
endobj

% The third object.
%
% This is a "Pages" object that contains information about the different
% pages.  The `2 0 R` is reference to the "Page" object, defined above.
3 0 obj
<<
	/Type /Pages
	/Kids [2 0 R ]
	/Count 1
>>
endobj

% The fourth object.
%
% This is a "Catalog" object that provides the main structure of the PDF.
% It points to a "Pages" object that contains information about the
% different pages -- this is the reference `3 0 R`.
4 0 obj
<<
	/Type /Catalog
	/Pages 3 0 R
>>
endobj

% The xref table.  This is a lookup table for all the objects.
%
% I'm not entirely sure what the first entry is for, but it seems to be
% important.  The remaining entries correspond to the objects I created.
xref
0 4
0000000000 65535 f
0000000851 00000 n
0000001396 00000 n
0000001655 00000 n
0000001934 00000 n

% The trailer.  This contains some metadata about the PDF.  Here there
% are two entries, which tell us that:
%
%   - There are 4 entries in the `xref` table.
%   - The root of the document is object 4 (the "Catalog" object)
%
trailer
<<
	/Size 4
	/Root 4 0 R
>>

% The startxref marker tells us that we can find the xref table 2196 bytes
% after the start of the file.
startxref
2196

% The end-of-file marker.
%%EOF
```
