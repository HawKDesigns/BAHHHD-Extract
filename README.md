# BAHHHD-Extract

A Python command-line extractor for **Bark 1.06** `.BAD` data archives and their matching `.BAH` directory files. It was tested against the `ATV.BAD` / `ATV.BAH` pair from the original Xbox release of *ATV: Quad Power Racing 2*. It uses only the Python standard library (Python 3.7 or newer).

The repository contains the extractor, its documentation, and license. Supply archive files from your own game copy; no game files are included.

## Extract an archive pair

In PowerShell, point the tool at a matching `.BAD` data file and `.BAH`
directory file. Replace the example paths with your own files:

```powershell
py -3 .\bad_extract.py "C:\path\to\archive.BAD" --bah "C:\path\to\archive.BAH" --list
py -3 .\bad_extract.py "C:\path\to\archive.BAD" --bah "C:\path\to\archive.BAH" -o ".\output"
```

If the matching `.BAH` is next to the `.BAD` and shares its filename, the
`--bah` option can be omitted. Resolve any reported extraction failures before
using the output.

For the **ATV.zip** preparation steps specific to *ATV: Quad Power Racing 2*,
including extracting your ISO, making the ZIP with the correct internal layout,
and compiling its vertex programs, follow the [QPR2 project's
instructions](https://github.com/HawKDesigns/qpr2-recomp/blob/main/PUBLISHING.md#vertex-programs-from-your-extracted-archive).

## Other commands

```powershell
py -3 .\bad_extract.py "C:\path\to\ATV.BAD"
py -3 .\bad_extract.py "C:\path\to\ATV.BAD" --bah "D:\other\ATV.BAH" -o ".\output"
py -3 .\bad_extract.py "C:\path\to\ATV.BAD" --list -f "*.xml"
py -3 .\bad_extract.py "C:\path\to\ATV.BAD" -o ".\ATV" -f "VertexShader/*" --quiet
```

| Option | Meaning |
| --- | --- |
| `bad` | Required path to the data file. |
| `--bah PATH` | Directory file; otherwise the tool searches beside the `.BAD` for the matching name, ignoring case. |
| `-o, --output DIR` | Output folder; defaults to the `.BAD` filename without its extension in the current directory. |
| `-l, --list` | Show names and uncompressed sizes without extracting. |
| `-f, --filter GLOB` | Include matching paths; repeatable and case insensitive. |
| `-q, --quiet` | Suppress each successful file line; still report failures and summary. |

The parser understands stored files and the Bark 1.06 LZSS compression variant. Other `.BAD` or `.BAH` formats may differ. It rejects malformed records and unsafe parent-directory paths. Existing output files with the same path may be overwritten on another extraction run, so use a clean output folder when repeating a full extraction.

## License and credits

The independent extractor code is licensed under [MIT](LICENSE). See [ATTRIBUTION.md](ATTRIBUTION.md) for the game and tool credits. The license applies to this repository's code and documentation; it does not license extracted game content. Keep your ISO, `.BAD`/`.BAH` files, extracted files, and locally made archives out of public repositories.
