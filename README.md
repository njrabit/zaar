# zaar
Working on an idea for a tool for interactively compressing files using zstd tunings &amp; dictionary, then compile to single BLOB

# Concept
Take advantage of the extensive features of the new Zstandard compression library to produce a new archive format that can be interactively "authored" to optimize certain files for compressibility (or uncompressed), random accessibility (block compressed, selectable sizing), and multiple zstd dictionaries by file extension or folder.
