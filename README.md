# Musescore-to-RAB

The purpose of this repository is to create a documentation and system to create an epub for inclusion in RAB/SAB app builders.

## Issues

You have beautifully rendered musicscore in Musescore and can create great PDF and images. You want to create an app. Including an image of a music score in and app is problematical. Either the resolution is too poor or the image does not fit the app page.

## Solution

Create an SVG file of the music score and place that in a HTML file then include the file in an epub that is imported into RAB/SAB.

## Secondary issues

### How to create the SVG file?

1. Use Musescore to output an SVG file for inclusion in an HTML file.
2. Use xml2abc to create a ABC file that can be embedded in an HTML file and rendered as an SVG via Javascript.

### Direct Musescore to SVG conversion issues
- The SVG file generated is large at about 1.5MB thus a song book of 100 songs would be 150+MB in size. Very big and too big for PlayStore.
- The process is simple and can be done via the command line so you don't have to do it one at a time



that is then placed in an epub file for inclusion as a song book with complete music score in a readable format
