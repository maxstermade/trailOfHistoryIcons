# Trail of Crumbs

#### Some things I have learned

### Sketch to SVG to XML

Exporting vectors to SVG in Sketch can be a bit complicated. By default, Sketch preserves any edits to a shape like a smart object in Photoshop. Say you have a simple rectangle and rotated it 90 degrees. That change is outputted in the SVG as a transform. This can be helpful if you are scaffolding out frames of an animation. But otherwise, you want to flatten every layer.

Another bit of confusion was comparing the SVG and the converted XML document. Sketch outputs shapes as vector primitives.

```xml
<g id="map">
    <polygon id="mapBG" fill="#D0011B" points="0 20 35 6.13000011 65 20 100.001885 5 100.001885 80.4999987 65 95 35 81.8499985 0 95.5999985"></polygon>
    <polygon id="leftFold" fill="#FFFFFF" points="4 23 33 11 33 78 4 89"></polygon>
    <polygon id="midFold" fill="#FFFFFF" points="64 24 36 11 36 78 63.5147108 90"></polygon>
    <polygon id="rightFold" fill="#FFFFFF" points="67 24 96 11 96 78 67 90"></polygon>
</g>
```

For the particular animation we were trying to produce, we needed all of the objects to export as paths. I was using [Inloop's svg2android](http://inloop.github.io/svg2android/) to convert it. It changes everything over to paths"

```xml
<?xml version="1.0" encoding="utf-8"?>
<vector xmlns:android="http://schemas.android.com/apk/res/android"
    android:width="100dp"
    android:height="100dp"
    android:viewportWidth="100"
    android:viewportHeight="100">

    <path
        android:name="mapBG"
        android:fillColor="#D0011B"
        android:strokeWidth="1"
        android:pathData="M 34 122.555267 L 186.537428 61.568943 L 325.436274 116.888454 L 478 56 L 478 391.169983 L 325.462268 452.058437 L 186.510643 396.738926 L 34 457.72525 Z" />
    <path
        android:name="leftFold"
        android:fillColor="#FFFFFF"
        android:strokeWidth="1"
        android:pathData="M 59 137.563841 L 179.079605 89 L 179.079605 374 L 59 422.563841 Z" />
    <path
        android:name="midFold"
        android:fillColor="#FFFFFF"
        android:strokeWidth="1"
        android:pathData="M 316.079605 137.563841 L 196 89 L 196 374 L 316.079605 422.563841 Z" />
    <path
        android:name="rightFold"
        android:fillColor="#FFFFFF"
        android:strokeWidth="1"
        android:pathData="M 333 137.563841 L 453.079605 89 L 453.079605 374 L 333 422.563841 Z" />
</vector>
```

To output the Sketch vector file as a path instead of a polygon shape I had to switch to Illustrator. By default, Illustrator also chooses to output SVG primitives. But you can work around this by changing each shape into a compound path in the Objects menu.

```xml
<svg width="100" height="100" viewBox="0 0 100 100"> style="enable-background:new 0 0 100 100;" xml:space="preserve">
<style type="text/css">
	.st0{fill:#D0011B;}
	.st1{fill:#FFFFFF;}
</style>
<path id="mapBG_1_" class="st0" d="M99,79.8L65,93.9l-29.6-13L35,80.8l-0.4,0.2L1,94.1V20.7L35,7.2l29.6,13.7l0.4,0.2l0.4-0.2
	L99,6.5V79.8z"/>
<path class="st1" d="M33, 78 L4, 89 V23 l29-12 V78z"/>
<path class="st1" d="M64, 24 L36, 11 v67 l27.5, 12 L64, 24z"/>
<path class="st1" d="M96, 78 L67, 90 V24 l29-12 V78z"/>
</svg>
```
