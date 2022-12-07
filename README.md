![Zaar fancy logo](zaar.jpg)

# zaar
Working on an idea for a tool for interactively compressing files using zstd tunings &amp; dictionary, then compile to single BLOB

# Concept
Take advantage of the extensive features of the new Zstandard compression library to produce a new archive format that can be interactively "authored" to optimize certain files for compressibility (or uncompressed), random accessibility (block compressed, selectable sizing), and multiple zstd dictionaries by file extension or folder.

The goal is a file format that is transparently either a single blob that can be embedded into a binary (read-only) or as individual files on a filesystem (read/write with live compression)

# Filesystem mode
There is a root folder which is "root" for the archive.  It contains files comprising the zaar archive.  Files can be copied in there as normal.  When they are compressed, a .zaar extension is added to the filename.  A file named "items.csv" is renamed to "items.csv.zaar" when it's compressed.  To the developer, "items.csv" will be fetched and decompressed from "items.csv.zaar" if the compressed version exists.  

There is an optional 'zdict' file in a directory that is the zstd dictionary file for any compressed files in that directory.  If 'zdict' does not exist in that directory, it traverses upwards to the closest 'zdict' folder.  If there's a 'zdict.csv' in a directory, all csv files use that training dictionary.  A 'zmap' can provide any mapping of 'zdict' to files.  A 'rebuild' operation will retrain dictionaries on their applied set of files, then recompress those files and report any changes in compression ratio.

Files marked for random access speed will contain their own dictionary, trained on a file as if it was split into fixed size files.

An interactive UI with filesystem drag/drop shows archive size as if in it's single binary file form, with a 'compile' button to combine the files into this format.
