The `SmuflFont` class defined in this module wraps SMuFL specific methods around `fontforge.font`
objects.

A copy of the `glyphnames.json` file from the SMuFL specification must be saved in the same
folder. Download it [from the SMuFL repository](https://github.com/w3c/smufl/tree/gh-pages/metadata).

### Just give me that metadata already
If all you need is a metadata file for your music font, copy `ffsmufl.py` and `glyphnames.json` to
the folder where your font is saved and edit the `ENGRAVING_DEFAULTS` dictionary at the bottom of
the script as necessary. Then run the script with an external Python 3 interpreter that has access
to the fontforge module (the script does **not** work with Fontforge's internal script console).

#### OS-dependant incantations:

On **Windows**, assuming `ffpython.exe` is in your PATH:
```
ffpython ./ffsmufl.py ./myfont.sfd
```

On **Mac**, assuming this monster is the path to your fontforge binary:
```
/Applications/FontForge.app/Contents/Resources/opt/local/bin/fontforge ./ffsmufl.py ./myfont.sfd
```

On **Linux**, assuming you have installed the Python bindings for Fontforge:
```
python3 ./ffsmufl.py ./myfont.sfd
```

### Advanced usage

If you need to create font metadata as part of a more involved scripted procedure,
you can import the `SmuflFont` class into your script. The class is just a thin wrapper around a
`fontforge.font` object that is accessible as the public `.font` member, so you can use the whole
Fontforge API with it.

```Python
import fontforge
from ffsmufl import SmuflFont


# create a SMuFL font object in memory from your project files:
with SmuflFont("path/to/my/font.ufo") as f:

    # use the Fontforge API on the font member
    for glyph in f.font:
        ...

    # set your engraving defaults
    f.engraving_defaults = { ... }

    # generate and export metadata
    f.export_metadata()

    # build the font itself
    f.export_font()
```
