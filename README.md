# Musescore-to-RAB/SAB

The purpose of this repository is to create a documentation and system to create an epub for inclusion in RAB/SAB app builders.

## Issues

You have beautifully rendered musicscore in Musescore and can create great PDF and images. You want to create an app. Including an image of a music score in and app is problematical. Either the resolution is too poor or the image does not fit the app page.

## Solution

Create an SVG file of the music score and place that in a HTML file, use the multiple HTML import into one book method. That is add songe 1 in an HTML file as the Book file. Then import the remaining HTML files as part of that book.

## Secondary issues

### How to create the SVG file?

1. Use Musescore to output an SVG file for inclusion in an HTML file.
2. Use xml2abc to create a ABC file that can be embedded in an HTML file and rendered as an SVG via Javascript.

### Direct Musescore to SVG conversion issues
- The SVG file generated is large at about 1.5MB thus a song book of 100 songs would be 150+MB in size. Very big and too big for PlayStore.
- The process is simple and can be done via the command line so you don't have to do it one at a time.

### Indirect method via ABC that produces very small SVG file for inclusion in HTML.
- Output MusicXML files from the Musescore program via the command line.
- Modify the musicXML files if needed. 
  - Use CC tables to remove credits
  - Use XSLT transforms on some specific files that have new lines in the text matter. This causes the ABC files too have an empty line. This to not rendered after the blank newline.
- Convert the modified musicXML files to ABC format via `xml2abc.exe` program donwloadable from: https://wim.vree.org/svgParse/xml2abc.html The ABC files can be edited in EasyABC editor. 
- Modify the ABC files.
  - Remove the title (This is added when creating the HTML file).
  - A list of files is supplied that need further correction.
- Make the HTML pages that include the ABC text. There is a XSLT transformatio that does this task. It looks at the ABC files and if there is an ABC file it creates the HTML file. 
- The created HTML files can be viewed to see if the music looks correct.
- Next start a Webserver.
- Render all the HTML files containing the ABC text. This converts the ABC text with Javascript rendering into SVG images. Each songe will have multiple SVG images.
- Each SVG image has a font embeded in it. This needs to be removed.
- Also the styling in the SVG file needs to be removed. It will be added to RAB/SAB
- Some of the viewBox top and bottom margins are not big enough so increase all to an extra 10 units before and 20 units after to avoid some slurs being clipped.
- If needed some individual fixes can be run on particular songs.
- The HTML songs can be viewed before the last step that makes them not render properly.
- The Link to the CSS is removed so they are ready for inclusion in RAB/SAB.
- This last file does not render properly in a browser since it has no style information. That is solved when it is in RAB/SAB.

The Styling added to RAB/SAB in the Custom Styles looks like this:
```
.dlog		display: none; background: lightblue; position: absolute; top: 50%; left: 50%; width: 30%; padding: 10px; transform: translate(-50%,-50%); z-index: 9; 
.abc svg		max-width: 1000px; display: block; cursor: pointer; 
.ewd svg		max-width: 800px; 
.music		font: 28px abc2svg; 
div, h1, h2		text-align: center; 
div		font-size: 10pt; text-align: center; 
h2		padding: 0; font-size: 12pt; font-family: Padauk; 
h1		font-size: 12pt; 
.songnumb		float: left; font-size: 14pt; font-weight: bold; 
.tspan		font-size: 14pt; 
.stroke		stroke: currentColor; fill: none; 
.bW		stroke: currentColor; fill: none; 
.bthW		stroke: currentColor; fill: none; stroke-width: 3; 
.slW		stroke: currentColor; fill: none; 
.slthW		stroke: currentColor; fill: none; 
.sW		stroke: currentColor; fill: none; position: relative; stroke-width: .7; 
.f0_0		font-family: Kayan Unicode; font-size: 12px; 
.f1_0		font-size: 12pt; font-family: Kayan Unicode; 
.f2_0		font-size: 13pt; font-weight: bold; 
.f3_0		font-size: 13pt; font-weight: bold; 
td		text-align: left; 
.info		font-size: 10pt; 
```
With the above styling in place the songs shuld render properly in the Viewer section for song 1.



