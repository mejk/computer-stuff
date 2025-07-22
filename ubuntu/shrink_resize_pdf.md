## How to shrink the size of PDFs etc:

CHnage the value in `-r150` as needed. Using 150 still gives high quality figures so it is a good start.
Works also for converting to/from png etc
```
ps2pdf14 -sDEVICE=pdfwrite -r150 -sOutputFile=output_file.pdf input_file.pdf
```
