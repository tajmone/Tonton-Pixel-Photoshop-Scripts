# Photoshop Custom Shapes File Format

-   [Contents](<#contents>)

-   [Custom shapes file format](<#custom-shapes-file-format>)

    -   [Custom shapes file](<#custom-shapes-file>)

    -   [Custom shape](<#custom-shape>)

    -   [Unicode string](<#unicode-string>)

    -   [Pascal-style string](<#pascal-style-string>)

    -   [Bounds rectangle](<#bounds-rectangle>)

    -   [Path record](<#path-record>)

    -   [Path fill rule record](<#path-fill-rule-record>)

    -   [Initial fill rule record](<#initial-fill-rule-record>)

    -   [Subpath length record](<#subpath-length-record>)

    -   [Subpath Bezier knot](<#subpath-bezier-knot>)

    -   [Path point](<#path-point>)

-   [Path records order](<#path-records-order>)

-   [Parsing custom shapes files](<#parsing-custom-shapes-files>)

## Contents

This document provides information about the (undocumented yet) format of custom
shapes files in Photoshop.

**Note**: all multi-byte values, i.e., integer numbers (including C-style
4-character constants), fixed-point numbers, and Unicode characters are coded in
[big-endian](<http://en.wikipedia.org/wiki/Big-endian>)
format.

## Custom shapes file format

### Custom shapes file

| Name               | Type                      | Kind                                                | Description                                                                                                                                                                                                                                                                                               |
|--------------------|---------------------------|-----------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `CustomShapes.psp` | `'8BPF'`                  | Custom shapes file                                  | Adobe Photoshop preferences file containing all the custom shapes listed in the Preset Manager.                                                                                                                                                                                                           |
|                    |                           |                                                     | **Warning**: like most preferences files, the custom shapes file is not updated in real-time: it is read by the application only once at start-up (launch) time and written back at shut-down (quit) time.                                                                                                |
| `*.csh`            | `'8BCS'`                  | Custom shapes file                                  | Adobe Photoshop custom shapes file; generally produced by saving a selected set of custom shapes from the Preset Manager.                                                                                                                                                                                 |
| Length (in bytes)  | Description               | Comments                                            |                                                                                                                                                                                                                                                                                                           |
| 4                  | Magic number (= `'cush'`) | C-style 4-character constant.                       |                                                                                                                                                                                                                                                                                                           |
| 4                  | Version (= 2)             | 32-bit integer.                                     |                                                                                                                                                                                                                                                                                                           |
| 4                  | Number of custom shapes   | 32-bit integer.                                     |                                                                                                                                                                                                                                                                                                           |
| Variable           | Sequence of custom shapes | Each in [Custom shape](<#custom-shape>) format. |                                                                                                                                                                                                                                                                                                           |

### Custom shape

| Length (in bytes) | Description                                                                                                | Comments                                                                           |
|-------------------|------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| Variable          | Custom shape name                                                                                          | [Unicode string](<#unicode-string>) format.                                    |
| 0 or 2            | Extra null padding                                                                                         | Only if length of previous Unicode string is odd.                                  |
| 4                 | Unknown (= 1)                                                                                              | 32-bit integer.                                                                    |
| 4                 | Length (in bytes) of remaining custom shape data                                                           | 32-bit integer.                                                                    |
| 1 + 36            | Custom shape ID ([UUID](<http://en.wikipedia.org/wiki/Universally_unique_identifier>)) | [Pascal-style string](<#pascal-style-string>) format.                          |
| 16                | Reference bounds for anchor and control points                                                             | [Bounds rectangle](<#bounds-rectangle>) format.                                |
| Variable          | Sequence of path records                                                                                   | Each in [Path record](<#path-record>) format.                                  |
| 1 or 3            | Extra null padding                                                                                         | To match the above length of remaining custom shape data (always a multiple of 4). |

### Unicode string

| Length (in bytes) | Description                  | Comments                                            |
|-------------------|------------------------------|-----------------------------------------------------|
| 4                 | Number of Unicode characters | 32-bit integer.                                     |
| Variable          | String of Unicode characters | Two bytes per character; includes terminating null. |

### Pascal-style string

| Length (in bytes) | Description          | Comments                                     |
|-------------------|----------------------|----------------------------------------------|
| 1                 | Number of characters | 8-bit integer (unsigned).                    |
| Variable          | String of characters | One byte per character; no terminating null. |

### Bounds rectangle

| Length (in bytes) | Description                   | Comments                 |
|-------------------|-------------------------------|--------------------------|
| 4                 | Top coordinate (in pixels)    | 32-bit integer (signed). |
| 4                 | Left coordinate (in pixels)   | 32-bit integer (signed). |
| 4                 | Bottom coordinate (in pixels) | 32-bit integer (signed). |
| 4                 | Right coordinate (in pixels)  | 32-bit integer (signed). |

### Path record

| Length (in bytes) | Description      | Comments               |
|-------------------|------------------|------------------------|
| 2                 | Selector         | 16-bit integer:        |
|                   |                  |                        |
| 24                | Path record data | Depending on selector: |

-   0 (closed subpath length record)

-   1 (closed subpath Bezier knot, linked)

-   2 (closed subpath Bezier knot, unlinked)

-   3 (open subpath length record)

-   4 (open subpath Bezier knot, linked)

-   5 (open subpath Bezier knot, unlinked)

-   6 (path fill rule record)

-   7 (clipboard record)

-   8 (initial fill rule record)

-   [Subpath length record](<#subpath-length-record>) format

-   [Subpath Bezier knot](<#subpath-bezier-knot>) format

-   [Subpath Bezier knot](<#subpath-bezier-knot>) format

-   [Subpath length record](<#subpath-length-record>) format

-   [Subpath Bezier knot](<#subpath-bezier-knot>) format

-   [Subpath Bezier knot](<#subpath-bezier-knot>) format

-   [Path fill rule record](<#path-fill-rule-record>) format

-   Clipboard record format (not used)

-   [Initial fill rule record](<#initial-fill-rule-record>) format

Cf. [Path resource
format](<http://www.adobe.com/devnet-apps/photoshop/fileformatashtml/PhotoshopFileFormats.htm#50577409_17587>)
of the page [Adobe Photoshop File Formats
Specification](<http://www.adobe.com/devnet-apps/photoshop/fileformatashtml/PhotoshopFileFormats.htm>)
for more details about the way paths are stored in a Photoshop document.

### Path fill rule record

| Length (in bytes) | Description | Comments          |
|-------------------|-------------|-------------------|
| 24                | Unused      | Should be zeroes. |

### Initial fill rule record

| Length (in bytes) | Description        | Comments                                                                             |
|-------------------|--------------------|--------------------------------------------------------------------------------------|
| 2                 | Initial fill (= 0) | 16-bit integer (unsigned); should be 0 or 1 (fill starts with all pixels); not used. |
| 22                | Unused             | Should be zeroes.                                                                    |

### Subpath length record

| Length (in bytes) | Description                             | Comments                   |
|-------------------|-----------------------------------------|----------------------------|
| 2                 | Subpath length (number of Bezier knots) | 16-bit integer (unsigned). |
| 22                | Unused                                  | Should be zeroes.          |

### Subpath Bezier knot

| Length (in bytes) | Description                                                      | Comments                                |
|-------------------|------------------------------------------------------------------|-----------------------------------------|
| 8                 | Backward control point for the Bezier segment preceding the knot | [Path point](<#path-point>) format. |
| 8                 | Anchor point for the knot                                        | [Path point](<#path-point>) format. |
| 8                 | Forward control point for the Bezier segment leaving the knot    | [Path point](<#path-point>) format. |

Cf. [Bezier
curves](<http://en.wikipedia.org/wiki/Bezier_curves>).

### Path point

| Length (in bytes) | Description          | Comments                                                                                                                                |
|-------------------|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| 4                 | Vertical component   | 32-bit fixed-point number (signed), in [Q8.24](<http://en.wikipedia.org/wiki/Fixed_point_numbers#Notation>) format. |
| 4                 | Horizontal component | 32-bit fixed-point number (signed), in [Q8.24](<http://en.wikipedia.org/wiki/Fixed_point_numbers#Notation>) format. |

[Fixed-point
numbers](<http://en.wikipedia.org/wiki/Fixed_point_numbers>)
are implemented here as 32-bit integers, with 8 bits before the binary point and
24 bits after the binary point. In JavaScript, since all numbers are represented
as floating-point numbers, appropriate values are simply obtained by dividing
the extracted 32-bit signed integer values by 0x1000000 (224).

The resulting horizontal and vertical component values of a path point always
fall between 0.0 and 1.0 (both exclusive).  
[ 0.0, 0.0 ] and [ 1.0, 1.0 ] correspond respectively to the top-left and
bottom-right corners of the bounds rectangle, which appears to have an extra
"safety" margin of 1 pixel in each direction (i.e.: top, left, bottom, right).

## Path records order

For each custom shape, the first path record is always a "path fill rule record"
(selector: 6), immediately followed by an "initial fill rule record"
(selector: 8), whose initial fill value (0 or 1) is apparently not used.

Then, for each subpath:

-   a "closed subpath length record" (selector: 0) is followed by a sequence of
    either "closed subpath Bezier knot, linked" (selector: 1) or "closed subpath
    Bezier knot, unlinked" (selector: 2),

or

-   an "open subpath length record" (selector: 3) is followed by a sequence of
    either "open subpath Bezier knot, linked" (selector: 4) or "open subpath
    Bezier knot, unlinked" (selector: 5).

## Parsing custom shapes files

A practical set of JavaScript functions for parsing custom shapes files is
contained in the module
[jamShapes](<https://web.archive.org/web/20150907123059/http://www.tonton-pixel.com/JSON%20Action%20Manager/jsDoc/symbols/jamShapes.html>),
which is part of the [JSON Action
Manager](<https://web.archive.org/web/20150907123059/http://www.tonton-pixel.com/blog/json-photoshop-scripting/json-action-manager/>)
scripting library. It is used by the following utility scripts:

-   [Convert Custom Shapes File to SVG
    Set](<https://web.archive.org/web/20150907123059/http://www.tonton-pixel.com/blog/scripts/utility-scripts/convert-custom-shapes-file-to-svg-set/>):
    [Photoshop CS3 or later] convert a custom shapes file (.csh) or a custom
    shapes preferences file (CustomShapes.psp) into a set of SVG files.

-   [Insert Custom Shape
    Path](<https://web.archive.org/web/20150907123059/http://www.tonton-pixel.com/blog/scripts/utility-scripts/insert-custom-shape-path/>):
    [Photoshop CS3 or later] create a work path from a custom shape contained in
    a custom shapes file (.csh).

-   [Parse Custom Shapes
    File](<https://web.archive.org/web/20150907123059/http://www.tonton-pixel.com/blog/scripts/utility-scripts/parse-custom-shapes-file/>):
    [Photoshop CS3 or later] parse a custom shapes file (.csh) or a custom
    shapes preferences file (CustomShapes.psp) into a JSON text file.

-   [Preview Custom Shapes
    File](<https://web.archive.org/web/20150907123059/http://www.tonton-pixel.com/blog/scripts/utility-scripts/preview-custom-shapes-file/>):
    [Photoshop CS3 or later] graphically preview a custom shapes file (.csh) or
    a custom shapes preferences file (CustomShapes.psp) in a new image document.

All files are open-source and licensed under
[GPLv3](<http://www.gnu.org/licenses/gpl.html>); the utility
scripts have been successfully tested in Photoshop CS4 on Mac OS X, but should
be platform agnostic.

Doc version: 1.9  
Date: 2015-05-16  
Copyright: © 2013-2015 Michel MARIANI  
Disclaimer: this information is provided 'as is' without warranty of any kind,
express or implied; use it at your own risk.
