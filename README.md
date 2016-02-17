# Tonton Pixel Photoshop Scripts

A collection of scripts and documents for Photoshop scripting in JavaScript (and
JSON), written/created by Michel MARIANI (aka “Mikaeru”) and originally
published on **Tonton Pixel’s Blog**
([www.tonton-pixel.com](<http://www.tonton-pixel.com>)) under the GNU General
Public License (GPL) v3.

Mariani has documented in detail the specifications of many of Photoshop saved
files formats (actions, custom shapes, gradients, and styles files) and written
an impressive JS/JSON library to parse and manipulate them.

## Why This Repository…

Unfortunately, in the past **Tonton Pixel’s Blog** has been unreachable for a
long time, and the only way I was able to visit the website (and retrive
material) was via
[WaybackMachine](<https://web.archive.org/web/20150906140236/http://www.tonton-pixel.com/blog/>)—also,
the only means of contacting the author was a contact-form, also unreachable.

Since this precious GPL lincensed material didn’t appear anywhere else on the
web, I thought of “salvaging” it by sharing it here on GitHub. It will most
definitely provide a good source of inspiration for anyone wishing to write some
Photoshop-related software, especially the well written “unofficial”
documentation on PS files specs—which, to my knowledge, is not to be found
elsewhere.

Soon after publishing this repository, Michel Mariani discovered it and
contacted me via email—a fortunate event which allowed me to get in contact with
him and also brought to his attention the problem regarding the non-reachability
of the blog, thus prompting an intervention on **Tonton Pixel’s Blog**, which is
now reachable again.

## Contents Description

The repository contains all the original—and unaltered—zip archives found on
**Tonton Pixel’s** website download section, along with the material downloaded
from its “documentation” section.

All materials are copyrighted © 2011-2014 by Michel MARIANI, all script files
are open-source, and licensed by MARIANI under the GNU General Public License
(GPL) v3.

### Documents

All documents downloaded from **Tonton Pixel’s** website are placed inside the
“[Documentation](<./Documentation/>)” folder. There are five documents in total
(in PDF and HTML format):

-   Photoshop Actions File Format

-   Photoshop Custom Shapes File Format

-   Photoshop Gradients File Format

-   Photoshop Styles File Format

-   Decision table for conflicting StringIDs in Photoshop (PDF).

### Scripts

All scripts downloaded from **Tonton Pixel’s** website are placed inside the
“[Scripts](<./Scripts/>)” folder.

Scripts fall into two main categories:

-   [Creative Scripts](<./Scripts/Creative_Scripts/>)  
    JavaScript creative scripts for Adobe Photoshop, making use of the scripting
    library.

-   [Utility Scripts](<./Scripts/Utility_Scripts/>)  
    JavaScript utility scripts for Adobe Photoshop, making use of the scripting
    library.

All of the scripts contained in these two categories are stand-alone scripts,
making use of the ”JSON Action Manager” scripting library.

Central to this Photoshop scripting project, are two components, each one
located in its own folder:

-   [JSON Action Manager](<./Scripts/JSON_Action_Manager/>)

-   [JSON Action Toolbox](<./Scripts/JSON_Action_Toolbox>)

### JSON Action Manager

In Mariani’s words:

>   “JSON Action Manager” is an open-source scripting library for Adobe
>   Photoshop, written in JavaScript, and licensed using GPLv3. It allows
>   developers to interact with the underlying Action Manager using a simpler
>   JSON AM Data Format (please refer also to the JSON Project Introduction page
>   to get more information).

>   What is called “JSON Action Manager” is basically a set of interrelated
>   modules defining global variables acting as namespaces…

### JSON Action Toolbox

>   “JSON Action Toolbox” is a developer-oriented set of automation plug-ins for
>   Adobe Photoshop running on Mac OS X, and is distributed as Freeware. It is
>   basically a combination of a “JSON Event Listener” and “JSON Property
>   Getter” modules, with several improvements over the original sample versions
>   coming with the SDK…

All the scripts are organized in a folders structure mirroring the original
grouping by Mariani. Each zip-archived library comes with a rich (JSDoc
generated) API documentation in HTML format, and with example/test scripts.

## More Resources…

For more documents by Michel Mariani on the subject, I strongly advice to visit
**Tonton Pixel’s Blog**:

-   [Tonton Pixel’s Blog](<http://www.tonton-pixel.com/>) Home

If for any reason the above link is unreachable, try via
[WaybackMachine](<https://web.archive.org/web/20150906140236/http://www.tonton-pixel.com/blog/>).

Especially, I advise to further read the articles linked below (which I didn’t
include in this repo since it wasn’t clear if they were too under GPL license,
and I haven’t yet managed to contact the author):

-   [JSON Photoshop
    Scripting](<http://www.tonton-pixel.com/blog/json-photoshop-scripting/>)

-   [Tutorials](<http://www.tonton-pixel.com/blog/tutorials/>)

-   [Scripts](<http://www.tonton-pixel.com/blog/scripts/>)

-   [FAQ](<http://www.tonton-pixel.com/blog/faq/>)

## Contributing

If you are interested in contributing to this repository, please read the
[CONTRIBUTING.md](<./CONTRIBUTING.md>) file for more info.

## History

-   2016/01/23 — Initial Commit.

-   2016/02/18 — **Tonton Pixel Blog** became available again:

    -   Re-downloaded HTML version of Documentation.

    -   Substituted links to Wayback Machine with direct links to **Tonton Pixel
        Blog** in various MD files.
