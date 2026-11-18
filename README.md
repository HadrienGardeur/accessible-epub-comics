# Accessible EPUB Comics

This repo hosts a full example of an accessible comic where each panel and speech bubble:
- are identified using a fragment of the image (using `#xywh` from [Media Fragments URI 1.0](https://www.w3.org/TR/media-frags/))
- have a textual equivalent using XHTML
- and an audio one using MP3 (generated with synthesized voices)

Through a series of examples, it highlights how EPUB can be leveraged today and how it could evolve to provide support for accessible comics.

## Level 0

For this level, the focus is entirely on [EPUB 3.4](https://w3c.github.io/epub-specs/epub34/authoring/) and what can be done today according to the specification.

This does not allow the creation of fully accessible comics, but covers the following use cases:

* Visual reading
* Reading using a screen reader (with braille or text-to-speech)
* Listening using the read aloud feature of a reading system
* Listening using pre-recorded audio
* Visual reading with audio playback (either pre-recorded or TTS)

This is entirely achieved using techniques that are supported in EPUB 3.4:

* The script of each page is contained in the XHTML but it's visually hidden
* Using SMIL, we can synchronize the textual script with pre-recorded audio
* Using terms from [EPUB 3 Structural Semantics Vocabulary 1.1](https://www.w3.org/TR/epub-ssv-11/#sec-comics), each panel and speech bubble is identified both in SMIL and XHTML

## Level 1

With this level, we're trying to bridge the gap between level 0 and EAA compliance:

> Presenting in fonts of adequate size and suitable shape, taking into account foreseeable conditions of use and using sufficient contrast, as well as adjustable spacing between letters, lines and paragraphs

With our level 0 example, text is hidden from users and only made available to screen readers and the read aloud feature of a reading system.

To meet the requirements of dyslexic and some low-vision users, we would ideally need to:

* Display text alongside the visual
* Anchor this text to a specific fragment of the visual

EPUB 3.4 does not provide the mean to anchor text to a region of an image or a fixed layout resource in general, but [it leaves the door open to use additional fragments in SMIL](https://w3c.github.io/epub-specs/epub34/authoring/#sec-media-overlays-fragids:~:text=Other%20fragment%20identifier%20schemes%20MAY%20be%20used%20but%20reading%20systems%20might%20not%20support%20such%20identifiers.).

Level 1 currently relies on [a spatial dimension fragment](https://www.w3.org/TR/media-frags/#naming-space) to achieve this goal:

* Each panel in the SMIL references a rectangle using percentages
* But this is currently done using `epub:textref` rather than a dedicated property

The lack of a dedicated element limits what can be done with the current EPUB 3.4 specification:

* We can alternate between fragments using spatial dimensions for panels and IDs for descriptions and bubbles
* But [the content model](https://w3c.github.io/epub-specs/epub34/authoring/#sec-smil-par-elem) disallows the use of multiple `<text>` elements, which means that we can't reference visual fragments for `balloon`, `text-area` and `sound-area`

Skippability is also an issue since dyslexic readers do not necessarily need image descriptions and would need a way to skip them. The current vocabulary for `epub:type` lacks an adequate term to identify these descriptions.

To go beyond these constraints, we would ideally need to introduce the following changes in EPUB 3.5:

* New elements to reference a visual element with a spatial dimension in `<seq>` and `<par>` ([GitHub issue](https://github.com/w3c/epub-specs/issues/2883))
* A new value in `epub:type` to identify descriptions ([GitHub issue](https://github.com/w3c/epub-specs/issues/2936))

## Level 2

This level covers additions that go beyond the requirements for EAA such as:

* Identifying characters in comics and giving them a voice
* Defining an audio cast using text prompts and/or audio snippets
* Expressing emotions with a controlled vocabulary for TTS use cases
* Background sounds and music

## Attributions

This example is based on [episode 17](https://www.peppercarrot.com/en/webcomic/ep17_A-Fresh-Start.html) of [Pepper & Carrot](https://www.peppercarrot.com/en/) from [David Revoy](https://framagit.org/Deevad), 
which is available under a [Creative Commons Attribution 4.0 license](https://creativecommons.org/licenses/by/4.0/).

This EPUB is a direct port of the work initially done by [Hadrien Gardeur](https://github.com/HadrienGardeur) for the Readium Guided Navigation draft: <https://github.com/readium/guided-navigation/tree/main/examples/comics>
