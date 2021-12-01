---
title: Adding diagrams
description: 
published: true
date: 2021-12-01T02:36:00.258Z
tags: 
editor: markdown
dateCreated: 2021-11-17T10:06:49.972Z
---

# Introduction
Your options for adding diagrams depends on your choice of authoring format:

## Drafting in XML
If you are [drafting in XML](/drafting-in-xml) then your diagrams need to be provided in SVG format and optionally also in ASCII for use when the I-D is rendered in plain text.  The SVG can be generated in one of a number of ways:
1. Using an interactive diagramming tool that generates SVG
1. Using a diagramming language that generates SVG
1. Converting a diagram in another format into SVG
1. Hand-coding the SVG

## Drafting in Markdown or another lightweight markup language
If you are [drafting in Markdown](/drafting-in-markdown) or [another lightweight markup language](/drafting-in-other-formats) then your options depend on the toolchain you use:
    1. Some tools allow you to specify an external SVG file
    1. Some tools support embedded diagramming languages and manage the conversion of those into SVG
    1. Some tools do not support SVG diagrams requiring you to use ASCII diagrams and/or add the SVG manually after the I-D has been converted to RFCXML.

## Drafting in plain text
For I-Ds that are submitted in plain text, any diagrams need to be included in ASCII inline in the text.

# Accepted SVG - SVG 1.2 RFC
Your SVG diagrams must conform to the SVG profile "SVG 1.2 RFC" as documented in RFC 7996 (which is in turn a subset of SVG Tiny 1.2) that has the following restrictions compared to standard SVG:
* No animation
* No interactivity
* No scripting or other extensibility
* No colour or grayscale, only black and white
* Only 'serif', 'sans-serif', and 'monospace'generic font families from the WebFonts facility
* Only ASCII links

See [Document Validation](/document-validation) for details of how to validate your SVG.

# Tools that generate SVG

The following tools are known to be used to generate SVG:

## Inkscape
## {.tabset}
### Details


### Community tips
#### Nevil Brownlee, July 2018
Of the Open Source packages, in my opinion Inkscape is the best of them. It's a big package, though, with many features, so there's a big learning curve to go through. Fortunately there's a lot of tutorial material on the web, for example: [Inkscape tutorial](http://tavmjong.free.fr/INKSCAPE/MANUAL/html/QuickStart.html) Note, however, that SVG 1.2 RFC only allows objects that are part of black-and-white line drawings.

Again, Inkscape uses markers for line-end symbols (even if you create your own markers using Object → Objects to Marker). That means, if you want arrowheads at the end of lines, you have to draw them in yourself. The simplest way to do that is to make an arrowhead with two lines grouped together, draw your lines, then copy your arrowhead at the end(s) of them.

Another nice feature of Inkscape is that its 'Resize page to content' lets you resize your svg drawing to trim the white space around its edges before you save it as 'Plain SVG'. See the example [SVG flowchart diagram](https://www.rfc-editor.org/rse/wiki/lib/exe/fetch.php?media=inkscape-drawn-arrows.svg) produced in this way.

## LibreOffice Draw
## {.tabset}
### Details


### Community tips
#### Nevil Brownlee, July 2018
This is good if you're used to LibreOffice, and your drawing is fairly simple.

Create your drawing using Draw, group it into a single object, then export it. (For me, that makes an SVG diagram that emacs and Inkscape display properly, but Firefox donesn't - however, check-svg.py's rewritten SVG diagram displays properly in Firefox, with Draw's arrowheads displayed properly.)

## Dia
## {.tabset}
### Details
Dia is a program to draw structured diagrams.  It is open source and runs on Windows, OSX, GNU/Linux and Unix. For more details and downloads see [http://dia-installer.de](http://dia-installer.de).  Dia outputs SVG where text strings within the diagram are searchable and selectable.

### Community tips
#### Nevil Brownlee, July 2018
Dia is simple to use. Save your drawing as xxx.dia, then export it as xxx.svg.

Dia draws line-end arrowheads as filled polygons, and it doesn't use markers.

## Powerpoint
## {.tabset}
### Details

### Community tips
#### Don Fedyk, April 2021
If you have black and white diagrams in PowerPoint these can be copied and pasted into Inkscape. You can resize and position on Inkscape's default page or you can create a drawing size and adjust. Then you can save as a plain svg. PowerPoint can save natively into SVG as well but that SVG is very detailed.

The plain SVG will have:
```xml
  width="210mm"
  height="279mm"
  viewBox="0 0 210 279" 
```
(or whatever your starting size was)

It is easier to make Inkscape drawing size close to the dimensions you want before saving. For a 1/2 page drawing a full page may be used and the height can be adjusted, but sometimes the conversion will complain and the height/width have to be removed. See positioning tips.)

Editing the basic svg:

You will need to remove clipPath and metadata (it will probably look something like this):
```xml
 <defs
    id="defs2">
   <clipPath
      id="clip0">
     <rect
        x="52"
        y="349"
        width="2159"
        height="889"
        id="rect10" />
   </clipPath>
 </defs>
 <metadata
    id="metadata5">
   <rdf:RDF>
     <cc:Work
        rdf:about="">
       <dc:format>image/svg+xml</dc:format>
       <dc:type
          rdf:resource="http://purl.org/dc/dcmitype/StillImage" />
       <dc:title></dc:title>
     </cc:Work>
   </rdf:RDF>
 </metadata>
```
The basic svg has some identifiers that must be removed:
```
font-weight
font-family
style="stroke-width:0.0911541"<...
```
The font-related ones can usually be deleted by deleting the whole line. The style one is part of a tspan tag and you must only remove the text. These VIM command line commands do it properly:
```
:1,$s/style="stroke.*"// 
:g/font-weight/d   
:g/font-family/d
```
At this point you can test the SVG either by including and running it in xml2rfc or using the SVG tester but xml2rfc catches more issues so I skip the tester. Rendering: `xml2rfc –pdf your_v3_xml_draft.xml`

Another issue is with `<tspan>`s. It seems text is expanded to text and tspan tags. Sometimes the physical text is between `<text>like this</text>`and sometimes it is between `<text><tspan>like</tspan><tspan>this</tspan></text>`which is fine but with hyphenated text there are two issues. It might put the text between the tspan and text tags: `<text><tspan>fouled</tspan>-</tspan>up</text>` and you need to correct it by either moving the text or deleting the tags. The `xml2rfc –pdf` will complain about this. Simply moving the text inside the tspan tags works.

Usually there are coordinates within the text and tspan tags - you want to keep those. Another issue is the coordinates of the text can cause the characters to overwrite in different tspans. `<text><tspan>fouled-up</tspan></text>` will print better than `<text><tspan>fouled</tspan>-up</tspan></text>`.

Positioning: The ViewBox has x-min y-min
```
x="0" y="0" width="100%" height="100%"/
```
For a half page drawing from the original:
```
  width="210mm"
  height="279mm"
  viewBox="0 0 210 279" 
           x y  w%   h%
```

The height controls the whitespace; if your drawing is 1/2 page you can usually reduce by 1/2 and it will only take 1/2 a page. Inch-based dimensions were harder to work with, and width and height had to be removed, but with mm dimensions the height could be reduced more before it complained. The x y controls move the origin; positive values for y move the origin down and the drawing upwards.

Adjusted for 1/2 page it might look like this:
```

  width="210mm"
  height="110mm"
  viewBox="0 15 210 110"  
```

Note that the x dimension is unchanged; also, in my experience, the scaling is far from linear. A slightly large diagram needed these values but the difference from 50 to 30 on the veiwBox height was hardly noticeable.
```

  width="210mm"
  height="135mm"
  viewBox="0 52 210 30"
```

The scaling is constant whether the drawing is at the top or following other drawings. Two pictures easily fit with captions on a page using this.

## Adobe Illustrator
## {.tabset}
### Details
Adobe Illustrator is not open source but is included as some may have already have access to it.  

### Community tips
#### Nevil Brownlee, July 2018
If you're familiar with Adobe Illustrator, it can also be used. It can save files as SVG-t (i.e. SVG Tiny), which - I assume - means that drawings saved in SVG-t don't use arrowheads.