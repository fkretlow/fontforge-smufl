This script generates SMuFL metadata files from FontForge projects.

A copy of the `glyphnames.json` file from the SMuFL specification must be saved
in the working directory.
Download it [from the SMuFL repository](https://github.com/w3c/smufl/tree/gh-pages/metadata).

If all you need is a metadata file for your music font, copy the script and
`glyphnames.json` to the folder where your font is saved and edit the
`ENGRAVING_DEFAULTS` dictionary in the script as necessary. Then run the script with a
Python 3 interpreter that has access to the fontforge module, e.g.:
```bash
ffpython smufl_metadata.py myfont.sfd
```

If you need to create font metadata as part of a more involved scripted procedure,
you can import the `SmuflMetadata` class into your script:
```Python
import fontforge
from ff_smufl_metadata import SmuflMetadata

font = fontforge.open('myfont.sfd')

# define your engraving defaults:
defaults = { ... }

metadata = SmuflMetadata(font, defaults)
metadata.dump_json()

font.close()
```
