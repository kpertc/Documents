#python 

`pyinstaller --windowed main.py`
`--windowed` no console window (GUI app) -> hides tracebacks, build without it to debug
`--onefile` single binary
`--add-data "src:dest"` bundle data files (`;` separator on Windows)
`--icon icon.ico`