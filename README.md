# react-perfect-image
Renders an image that fills its container width and has the correct aspect ratio before the image source has loaded (no page reflow!). Also supports dynamic insertion of width and height values into src url so that you always fetch the correct image for the given screen size.

## Demo
<a href="https://unsplash.now.sh">unsplash.now.sh</a>

## Install
`npm install react-perfect-image --save`

## Props

Prop                       |    Description
---------------------------|----------------
`src`                      | Image src url
`widthHeightRatio`         | Ratio between width and height. A value of `2` or `2/1` would result in an image that's twice as wide as it is tall. We specify a ratio rather then an exact width and height because the image always fits its container while maintaining the correct aspect ratio.
`parseSrc`                 | Set to `true` if the supplied `src` prop contains the string `{width}` or `{height}` and we'd like this string replaced with the value of `parseSrcWidth`.
`parseSrcWidth`              | A width value that we'd like to insert into the src url. You'd detect the width in a parent component and pass it in via this prop.
`parseSrcAllowedWidths`           | An array of numeric width values. Rather then parse the url and insert the value of `parseSrcWidth` it will find the closest value within this array and use that instead. You'd want to use this if you have a specific set of image sizes (rather then a dynamic CDN that can return an image of any desired width).
`parseSrcDoubleForRetina`              | Set to `true` (default) if you'd like the `parseSrcWidth` value to be doubled on retina devices.
`children`                    | Elements or components that you'd like displayed directly after the `<img>` tag. This is useful if you'd like to absolutely position something over the image.

## Example
```js
import React from 'react';
import Image from 'react-perfect-image';

const Photo = ({ data, parentWidth }) => {

  const allowedSrcWidths = [ 200, 300, 400, 500 ];
 
  return (
    <a href={data.links.html}>
      <Image 
        src={`https://source.unsplash.com/${data.id}/{width}x{height}`} 
        parseSrc={true} 
        parseSrcWidth={parentWidth} 
        parseSrcAllowedWidths={allowedSrcWidths} 
        parseSrcDoubleForRetina={true}
        displaySrcWidth={true}
        widthHeightRatio={1/1}
        title={`A photo by ${data.user.name}`/>
    </a>
  );
  
};
```
