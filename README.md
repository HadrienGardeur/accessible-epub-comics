# Accessible EPUB Comics

This repo hosts a full example of an accessible comic where each panel and speech bubble:
- are identified using a fragment of the page (using `#xywh` from [Media Fragments URI 1.0](https://www.w3.org/TR/media-frags/))
- provide a textual equivalent in HTML
- and an audio one using MP3 (generated with synthesized voices)

This is the first example of an EPUB files where `<img>` is used in SMIL (see related [issue](https://github.com/w3c/epub-specs/issues/2883) and [PR](https://github.com/w3c/epub-specs/pull/2919)).

## Attributions

This example is based on [episode 17](https://www.peppercarrot.com/en/webcomic/ep17_A-Fresh-Start.html) of [Pepper & Carrot](https://www.peppercarrot.com/en/) from [David Revoy](https://framagit.org/Deevad), 
which is available under a [Creative Commons Attribution 4.0 license](https://creativecommons.org/licenses/by/4.0/).

This EPUB is a direct port of the work initially done by [Hadrien Gardeur](https://github.com/HadrienGardeur) for the Readium Guided Navigation draft: <https://github.com/readium/guided-navigation/tree/main/examples/comics>
