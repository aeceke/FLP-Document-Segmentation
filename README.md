This repository contains code for segmenting judiciary financial disclosure documents. The script, disclosure_doc_segmenting.py, takes 2 command line arguments, the image file path, and an output directory path. The output is a series of PDF documents, created by segmenting the TIFF image, and iterates over a decreasing number of segmentation points in the image.

To run this script: python disclosure_doc_segmenting.py \<image file path\> \<directory path to save PDF output\>

Example: python disclosure_doc_segmenting.py '/Users/andreaekey/Desktop/FLP/Ungaro-U.  J3. 11. FLS_Resp_R_18.tiff' '/Users/andreaekey/Desktop/FLP'


I approached this problem by observing that within the document, the vertical margins between pages had large areas of whitespace. My script expands upon this observation to identify areas of the document where there were large portions of whitespace and use those as guides to segment the image into separate pages. 

The document was read in using the keras package, as an array of grayscale values. Rows where all color values are white are considered whitespaces, and consecutive rows of whitespaces are potential segmentation points. The code identifies the location (row index) and counts of consecutive whitespaces.

The number of consecutive whitespaces is used as a heuristic to determine where the image should be cut and a new page delineated. This is done iteratively, reducing the number of cutpoints by dropping the cutpoint with the smallest sized whitespace. On each iteration, the image is split image at the remaining cutpoints and PDFs are generated.
