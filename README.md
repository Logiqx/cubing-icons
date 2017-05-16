# Cubing Icons

## Background

This project contains the various cube icons for my speedcubing website. It targets the most common operating systems (Android, Apple, Microsoft) and browsers (Chrome, Firefox, IE / Edge, Safari) in addition to many other popular platforms.

Before embarking on this activity, I didn't anticipate the complexities and gotchas relating to favicons and touch icons. Cross-platform support has many pitfalls and is a lot tricker than I had originally anticipated! After putting so much time and effort into the creation of my icons, I felt it was worth documenting my learnings and processes.

Two of the online resources that I used at the beginning of this project were the [RealFaviconGenerator](http://realfavicongenerator.net/faq) and the [favicon-cheat-sheet](https://github.com/audreyr/favicon-cheat-sheet). They are really useful references and have helped me to make a number of the technical choices.

I've provided support for a number of platforms and split them into separate folders for the sake of clarity:

* **android** - Quick access icons, launcher icons and splash icons
* **apple** - Touch icons for the home screen and browser favorites on iOS
* **classic** - Favorites / bookmarks, browser tabs, desktop links, etc.
* **microsoft** - Start menu tiles for Windows 8.1 / Windows 10 + IE 11
* **visualcube** - The original SVG images from which all of the icons were generated

All of the icons were generated using [VisualCube](http://cube.crider.co.uk/visualcube.php) and [ImageMagick](https://www.imagemagick.org/).

The remainder of this document describes how the icons were created and the various platforms / features that are supported.


## VisualCube

The "visualcube" folder contains the master images in [SVG](https://en.wikipedia.org/wiki/Scalable_Vector_Graphics) format.

* **master-colour.svg** - The colour image is used for most of the icons
* **master-black.svg** - The black silhouette was used during testing
* **master-white.svg** - The white silhouette is used for the Microsoft tiles

### Commands
The colour image was generated online using using [VisualCube](http://cube.crider.co.uk/visualcube.php):

```bash
curl -o visualcube/master-colour.svg "http://stachu.cubing.net/v/?fmt=svg&size=720&bg=t&r=y45x-30"
```

The black and white silhouettes were hand-crafted by manually tweaking the colour SVG.

### References
* Conrad Rider - [VisualCube](http://cube.crider.co.uk/visualcube.php)


## ImageMagick

[ImageMagick](https://www.imagemagick.org/) is an image processing tool which can be used from the command line.

The following options are used to create most of the images in this package:

* **-background** is used to specify a solid background colour or a transparent background
* **-trim** removes any redundant space around the source image
* **-resize** is fairly obvious but it is worth noting that the original aspect ratio is retained
* **-gravity** specifies how the resized image is to be positioned on the final canvas
* **-extent** specifies the size of the final canvas and utilises the gravity parameter

e.g. Creating a 180 x 180 pixel Apple touch icon with a white background and 5% border:

```bash
convert -background white visualcube/master-colour.svg -trim -resize 162x162 -gravity center -extent 180x180 apple/apple-touch-icon.png
```

### References
* ImageMagick - [Trim, the 'Auto-Crop' Operator](http://www.imagemagick.org/Usage/crop/#trim)
* ImageMagick - [Resizing Images](http://www.imagemagick.org/Usage/resize/#resize)
* Matteo Spinelli - [Create fixed size thumbnails with ImageMagick](http://cubiq.org/create-fixed-size-thumbnails-with-imagemagick)


## Android Chrome

The "android" folder contains all of the images used by Android Chrome, referenced by the Web App manifest.

The 192x192 image is the only icon included in the \<head> section of the HTML:

```xml
<link rel="icon" type="image/png" sizes="192x192" href="/android-chrome-192x192.png">
```

Note: 192 is a common factor of 16, 24, 32, 48, 64 and 96 so it can easily be scaled when a smaller icon is required.

The Android images are primarily used for launcher icons and splash screens. This package includes images for all of the standard pixel densities documented for Android.

Launcher Icon for Web App:

|    DPI    |   120 dpi   |    160 dpi   |    240 dpi   |    320 dpi   |    480 dpi   |    640 dpi    |
|:---------:|:-----------:|:------------:|:------------:|:------------:|:------------:|:-------------:|
|  Density  | ldpi @0.75x |  mdpi @1.0x  |  hdpi @1.5x  |  xhdpi @2.0x | xxhdpi @3.0x | xxxhdpi @4.0x |
| Icon Size | 36 x 36 px  |  48 x 48 px  |  72 x 72 px  |  96 x 96 px  | 144 x 144 px | 192 x 192 px  |

Splash Screen for Web App:

|    DPI    |   120 dpi   |    160 dpi   |    240 dpi   |    320 dpi   |    480 dpi   |    640 dpi    |
|:---------:|:-----------:|:------------:|:------------:|:------------:|:------------:|:-------------:|
|  Density  | ldpi @0.75x |  mdpi @1.0x  |  hdpi @1.5x  |  xhdpi @2.0x | xxhdpi @3.0x | xxxhdpi @4.0x |
| Icon Size | 96 x 96 px  | 128 x 128 px | 192 x 192 px | 256 x 256 px | 384 x 384 px | 512 x 512 px  |

The images must be listed in manifest.json along with other Web App metadata:

```json
{
    "name": "Mike's Cube Algs",
    "short_name": "Cube Algs",
    "start_url": "/algs",
    "display": "standalone",
    "icons": [
        {
            "src": "/android-chrome-36x36.png",
            "sizes": "36x36",
            "type": "image/png"
        },
        {
            "src": "/android-chrome-48x48.png",
            "sizes": "48x48",
            "type": "image/png"
        },
        {
            "src": "/android-chrome-72x72.png",
            "sizes": "72x72",
            "type": "image/png"
        },
        {
            "src": "/android-chrome-96x96.png",
            "sizes": "96x96",
            "type": "image/png"
        },
        {
            "src": "/android-chrome-128x128.png",
            "sizes": "128x128",
            "type": "image/png"
        },
        {
            "src": "/android-chrome-144x144.png",
            "sizes": "144x144",
            "type": "image/png"
        },
        {
            "src": "/android-chrome-192x192.png",
            "sizes": "192x192",
            "type": "image/png"
        },
        {
            "src": "/android-chrome-256x256.png",
            "sizes": "256x256",
            "type": "image/png"
        },
        {
            "src": "/android-chrome-384x384.png",
            "sizes": "384x384",
            "type": "image/png"
        },
        {
            "src": "/android-chrome-512x512.png",
            "sizes": "512x512",
            "type": "image/png"
        }
    ]
}
```

The manifest itself requires a link in the \<head> section of the HTML:

```xml
<link rel="manifest" href="manifest.json">
```

To support older versions of Android Chrome (M31 to M38) there is an additional declaration in the HTML:

```xml
<meta name="mobile-web-app-capable" content="yes">
```

A theme colour can also be specified as follows:

```xml
<meta name="theme-color" content="#387ebb">
```

### Commands
All of the Android images were generated with transparent backgrounds and filling the canvas:

```bash
convert -background transparent visualcube/master-colour.svg -trim -resize 36x36 -gravity center -extent 36x36 android/android-chrome-36x36.png
convert -background transparent visualcube/master-colour.svg -trim -resize 48x48 -gravity center -extent 48x48 android/android-chrome-48x48.png
convert -background transparent visualcube/master-colour.svg -trim -resize 72x72 -gravity center -extent 72x72 android/android-chrome-72x72.png
convert -background transparent visualcube/master-colour.svg -trim -resize 96x96 -gravity center -extent 96x96 android/android-chrome-96x96.png
convert -background transparent visualcube/master-colour.svg -trim -resize 128x128 -gravity center -extent 128x128 android/android-chrome-128x128.png
convert -background transparent visualcube/master-colour.svg -trim -resize 144x144 -gravity center -extent 144x144 android/android-chrome-144x144.png
convert -background transparent visualcube/master-colour.svg -trim -resize 192x192 -gravity center -extent 192x192 android/android-chrome-192x192.png
convert -background transparent visualcube/master-colour.svg -trim -resize 256x256 -gravity center -extent 256x256 android/android-chrome-256x256.png
convert -background transparent visualcube/master-colour.svg -trim -resize 384x384 -gravity center -extent 384x384 android/android-chrome-384x384.png
convert -background transparent visualcube/master-colour.svg -trim -resize 512x512 -gravity center -extent 512x512 android/android-chrome-512x512.png
optipng -o7 -zm1-9 android/*.png
```

### References
* RealFavIconGenerator - [Android Chrome and its favicon](https://realfavicongenerator.net/blog/android-chrome-and-its-favicon/)
* Android Developer API Guides - [Launcher Icons](https://developer.android.com/guide/practices/ui_guidelines/icon_design_launcher.html)
* Chrome Developer - [Add to Homescreen](https://developer.chrome.com/multidevice/android/installtohomescreen)
* Goole Developers Web Fundamentals - [The Web App Manifest](https://developers.google.com/web/fundamentals/engage-and-retain/web-app-manifest/)
* Google Developers Updates - [Adding a Splash Screen](https://developers.google.com/web/updates/2015/10/splashscreen)
* Google Developers Updates - [Support for theme-color in Chrome 39 for Android](https://developers.google.com/web/updates/2014/11/Support-for-theme-color-in-Chrome-39-for-Android)
* MDN - [Web App Manifest](https://developer.mozilla.org/en-US/docs/Web/Manifest)


## Apple iOS

The "apple" folder contains all of the images used by iOS - e.g. iPhones and iPads.

Although iOS supports an alpha channel (i.e. transarency information) it chooses to use a black background which looks ugly on the home page. The icons in this package have therefore been created with a solid white background.

There is no need to reference the icons from the HTML (e.g. apple-touch-icon) since the iOS devices will automatically retrieve the appropriate image from the root of the website. Some older browsers may attempt to download an Apple touch icon if a link exists in the HTML but this would be undesirable because of the solid white background. It is therefore preferable to avoid links in the HTML and leave iOS to automatically retrieve the appropriate image.

Specific images for every resolution have been created to avoid 404 errors on the server. Default images are included ensure there is always an icon for iOS regardless of the device / version; apple-touch-icon.png and apple-touch-icon-precomposed.png

iOS 6 and earlier used the following sizes and corresponding precomposed images:

| iPhone (non-Retina) | iPhone (Retina) | iPad (non-Retina) | iPad (Retina) |
|:-------------------:|:---------------:|:-----------------:|:-------------:|
|     @1x display     |   @2x display   |    @1x display    |  @2x display  |
|     57 x 57 px      |  114 x 114 px   |    72 x 72 px     | 144 x 144 px  |

iOS 7 was released on 18/09/2013 and replaced the iOS 6 image sizes with the following:

| iPhone (non-Retina) | iPhone (Retina) | iPad (non-Retina) | iPad (Retina) |
|:-------------------:|:---------------:|:-----------------:|:-------------:|
|     @1x display     |   @2x display   |    @1x display    |  @2x display  |
|     60 x 60 px      |  120 x 120 px   |    76 x 76 px     | 152 x 152 px  |

iOS 8 was released on 17/09/2014 and added the following size:

| iPhone 6+ (Retina) |
|:------------------:|
|      @3x display   |
|    180 x 180 px    |

iOS 9 was released on 16/09/2015 and added the following size:

| iPad Pro (Retina)|
|:----------------:|
|     @2x display  |
|   167 x 167 px   |

Note: This package does not include dedicated images for iOS <=6 since they have been superceded by iOS 7 since 2013.

### Commands
All of the images were generated with a white background and a slight border:

```bash
convert -background white visualcube/master-colour.svg -trim -resize 54x54 -gravity center -extent 60x60 apple/apple-touch-icon-60x60.png
convert -background white visualcube/master-colour.svg -trim -resize 108x108 -gravity center -extent 120x120 apple/apple-touch-icon-120x120.png
convert -background white visualcube/master-colour.svg -trim -resize 68x68 -gravity center -extent 76x76 apple/apple-touch-icon-76x76.png
convert -background white visualcube/master-colour.svg -trim -resize 136x136 -gravity center -extent 152x152 apple/apple-touch-icon-152x152.png
convert -background white visualcube/master-colour.svg -trim -resize 150x150 -gravity center -extent 167x167 apple/apple-touch-icon-167x167.png
convert -background white visualcube/master-colour.svg -trim -resize 162x162 -gravity center -extent 180x180 apple/apple-touch-icon.png
convert -background white visualcube/master-colour.svg -trim -resize 162x162 -gravity center -extent 180x180 apple/apple-touch-icon-precomposed.png
optipng -o7 -zm1-9 apple/*.png
```

### References
* Mathias Bynens - [Everything you always wanted to know about touch icons](https://mathiasbynens.be/notes/touch-icons)
* RealFavIconGenerator - [Apple touch icon: The Good, the Bad and the Ugly](https://realfavicongenerator.net/blog/apple-touch-icon-the-good-the-bad-the-ugly)
* Apple - [Configuring Web Applications](https://developer.apple.com/library/content/documentation/AppleApplications/Reference/SafariWebContent/ConfiguringWebApplications/ConfiguringWebApplications.html)
* Apple - [App Icon Sizes](https://developer.apple.com/ios/human-interface-guidelines/graphics/app-icon/)

## Classic Favicon

The "classic" favicon is supported by pretty much all browsers and resides in the root directory of the website. There is no requirement for a link in the HTML and this seems like a decent policy because there are a number of differing / conflicting approaches which are browser specific.

Here are just a few examples:

```xml
<link rel="shortcut icon" href="/favicon.ico" type="image/vnd.microsoft.icon">
<link rel="shortcut icon" href="/favicon.ico" type="image/x-icon">
<link rel="shortcut icon" href="/favicon.ico">
```

The ICO format was invented by Microsoft and typically contains multiple images. Microsoft recommends 16x16, 32x32 and 48x48 pixel images to be included in a favicon. The most commonly used sizes are 16x16 and 32x32 but larger sizes may be used for desktop icons, etc.

Remote desktop environments prefer 256 colour images but this favicon includes 32-bit images (RGB + alpha) because they look nicer and support transparency. In theory the ICO format also supports image compression but there are reports of compression causing applications to crash on some platforms (e.g. Windows Vista).

Modern browsers are better off with a high resolution PNG rather than the ICO so you can use the following in the HTML:

```xml
<link rel="icon" type="image/png" sizes="192x192" href="/android-chrome-192x192.png" />
```

Note: 192 is a common factor of 16, 24, 32, 48, 64 and 96 so it can easily be scaled when a smaller icon is required.

### Commands
The classic favicon was created using [ImageMagick](https://www.imagemagick.org/):

```bash
convert -background transparent master/svg-colour.svg -trim -resize 576x576 -gravity center -extent 576x576 -define icon:auto-resize=48,32,16 classic/favicon.ico
```

### References
* Mathias Bynens - [rel="shortcut icon" considered harmful](https://mathiasbynens.be/notes/rel-shortcut-icon)
* Jonathan T. Neil - [Understand the Favicon](http://www.jonathantneal.com/blog/understand-the-favicon/)
* MSDN - [Customizing the Site Icon](https://msdn.microsoft.com/library/gg491740(v=vs.85).aspx)
* W3C - [How to Add a Favicon to your Site](https://www.w3.org/2005/10/howto-favicon)


## Microsoft Edge + Internet Explorer

The "microsoft" folder contains all of the tile images used by Windows 8.1 / Windows 10 + IE 11. These tiles can be pinned to the start menu by Edge and Internet Explorer and blend in with other applications using the Metro style.

There are 4 tile sizes (small, medium, wide and large) and the resolutions are specified by Microsoft. You will notice that the recommended size of the tiles is larger than you might expect; Microsoft recommends +80%.

e.g. The 150 x 150 (medium) tile is actually 270 x 270.

| Tile Name | Tile Size    | Minimum Size | Recommended Size |
|:---------:|:------------:|:------------:|:----------------:|
| Small     |  70 x 70 px  |  56 x 56 px  |   128 x 128 px   |
| Medium    | 150 x 150 px | 120 x 120 px |   270 x 270 px   |
| Wide      | 310 x 150 px | 248 x 120 px |   558 x 270 px   |
| Large     | 310 x 310 px | 248 x 248 px |   558 x 558 px   |

The tiles need to be specified in browserconfig.xml which should be in the root of your website:

```xml
<?xml version="1.0" encoding="utf-8"?>
<browserconfig>
    <msapplication>
        <tile>
            <square70x70logo src="/mstile-70x70.png"/>
            <square150x150logo src="/mstile-150x150.png"/>
            <wide310x150logo src="/mstile-310x150.png"/>
            <square310x310logo src="/mstile-310x310.png"/>
            <TileColor>#da532c</TileColor>
        </tile>
    </msapplication>
</browserconfig>
```

There is no need for the following in the \<head> section of the HTML as the Microsoft browsers will search the website root automatically:

```xml
<meta name="msapplication-config" content="/browserconfig.xml">
```

Note: My package does not include a 144x144 tile for Windows 8 + IE 10 because it has been superceded.

### Commands
All of the images were generated from the white silhouette and the image itself is only a small portion of the canvas:

```bash
convert -background transparent visualcube/master-white.svg -trim -resize 64x64 -gravity center -extent 128x128 microsoft/mstile-70x70.png
convert -background transparent visualcube/master-white.svg -trim -resize 90x90 -gravity center -extent 270x270 microsoft/mstile-150x150.png
convert -background transparent visualcube/master-white.svg -trim -resize 90x90 -gravity center -extent 558x270 microsoft/mstile-310x150.png
convert -background transparent visualcube/master-white.svg -trim -resize 186x186 -gravity center -extent 558x558 microsoft/mstile-310x310.png
optipng -o7 -zm1-9 microsoft/*.png
```
### References
* Microsoft - [Creating custom tiles for IE11 websites](https://msdn.microsoft.com/library/dn455106(v=vs.85).aspx)
* Microsoft - [Browser configuration schema reference](https://msdn.microsoft.com/library/dn320426(v=vs.85).aspx)
* ImageMagick - [Shifting images keeping size](http://www.imagemagick.org/discourse-server/viewtopic.php?t=20823)
* RealFaviconGenerator - [More browserconfig.xml, less HTML](https://realfavicongenerator.net/blog/more-browserconfig-xml-less-html/)


## Additional Comments
### Usage
All of the files can simply be placed in the root of a website:

| Platform  | Files                 | Minimum Size | Maximum Size |
|:---------:|:---------------------:|:------------:|:------------:|
| Android   | android-chrome-*.png  |  36 x 36 px  | 512 x 512 px |
| Android   | manifest.json         |  36 x 36 px  | 512 x 512 px |
| Apple     | apple-touch-icon*.png |  60 x 60 px  | 180 x 180 px |
| Classic   | favicon.ico           |  16 x 16 px  |  48 x 48 px  |
| Microsoft | mstile-*.png          |  70 x 70 px  | 310 x 310 px |
| Microsoft | browserconfig.xml     |  70 x 70 px  | 310 x 310 px |

The Android Chrome manifest requires a link in the \<head> section of the HTML:

```xml
<link rel="manifest" href="manifest.json">
```

You can also include some additional markup for Android Chrome M31 to M38, described earlier in this document.

### References
* Favicons / Touch Icons
 ** RealFaviconGenerator - [Favicon – Why you’re doing it wrong](https://realfavicongenerator.net/blog/favicon-why-youre-doing-it-wrong/)
 ** RealFaviconGenerator - [FAQ](https://realfavicongenerator.net/faq)
 ** RealCSS - [Favicons, Touch Icons, Tile Icons, etc. Which Do You Need?](https://css-tricks.com/favicon-quiz/)
 ** favicon-cheat-sheet - [Obsessive cheat sheet to favicon sizes/types](https://github.com/audreyr/favicon-cheat-sheet)
* Web Apps
 ** Google Developers Web Fundamentals - [Icons & Browser Colors](https://developers.google.com/web/fundamentals/design-and-ui/browser-customization/)
 ** Google Developers Web Fundamentals - [Making Fullscreen Experiences](https://developers.google.com/web/fundamentals/native-hardware/fullscreen/)
 ** Breaking the Mobile Web - [Home screen web apps for Android thanks to Chrome 31+](http://www.mobilexweb.com/blog/home-screen-web-apps-android-chrome-31)
