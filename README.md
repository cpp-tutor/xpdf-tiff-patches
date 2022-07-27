# xpdf-tiff-patches

Patches for the Xpdf toolkit (version 4.04) to enable TIFF output and more, see: https://www.xpdfreader.com

Patch **pdftotiff-xpdf-4.04.patch** adds alpha channel export capability for pages rendered to bitmap:

* pdftoppm has `-alpha` option which exports the mask (only) as an 8-bit PGM
* new tool "pdftotiff" allows export of pages as TIFF files (requires an available libtiff to compile)
* pdftotiff also has `-alpha` option allowing generation of image with mask (to the same file)
* pdftotiff and pdftoppm have new `-cmyk` option allowing generation of color separated TIFF files (only if configured with `-DSPLASH_CMYK=ON` to cmake)
* TIFF output files are compressed by default with LZW (or Huffman-RLE for `-mono`); this can be disabled with option `-no-compression`

Patch **pdfimages-xpdf-4.04.patch** allows export of embedded images as more common formats:

* pdfimages now has `-png` option to export as PNG files as monochrome, grayscale or color
* pdfimages now also has `-tiff` option (when libtiff is available) to export as TIFF files in monochrome, grayscale, color or separated (as they are in the source PDF)
* pdfimages can now correctly export indexed color images as RGB (either PNG or TIFF)
* masks are written to separate image files, as either a monochrome or grayscale PNG or TIFF (this is not ideal, but I'm unsure of how to resolve this)
* specifying `-j` (optionally in addition to either `-raw`, `-png` or `-tiff`) exports embedded JPEG images as `.jpg` files with other images in the specified format (PBM if not specified)

See the [latest release](https://github.com/cpp-tutor/xpdf-tiff-patches/releases/tag/4.04-release1) for Windows binaries. To run these executables, you may need to install the Windows C++ redist (Visual Studio redistributable libraries) linked from this page:

https://docs.microsoft.com/en-US/cpp/windows/latest-supported-vc-redist?view=msvc-170
