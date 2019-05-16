# Comparing images and videos with splits

## Basics

The comparison of elements is handled by inserting a div with class
compare in the document. No need to specify anything else, the javascript
will take care of resizing it to the content. Inside this compare div, the
compared elements can be either videos or images. They must be given the
compared class.

## Comparing two images

When comparing images, add two images in the compare div with class
compare. One image must be given class compared-left, the other one
compared right. A label can be given to the images using a data-compare
attribute.

```html
<div class="compare">
  <img class="compared compared-left" data-compare="standard" src="single-012.png"/>
  <img class="compared compared-right" data-compare="ours" src="multi-012.png"/>
</div>
```

## Comparing videos

Although videos could be compared as images with two videos, one
compared-left and the other one compared-right, if the videos are to be
kept synchronize, the above method will not work since frames can be
arbitrarily dropped independently on the videos, and actively maintaining
the synchronization is difficult. The alternative is to avoid
synchronization by using one single video.  Take the two videos, and
create a new video merging both side by side, either vertically or
horizontally.  If the two videos are stacked vertically, add the video
with classes compared and compared-vertical in the compare div. For
horizontal side by side, use compared-horizontal.  Labels can be given
using data-compare-top and data-compare-bottom attributes (vertical case)
or data-compare-left and data-compare-right (horizontal case). The video
should probably also be given loop and autoplay attributes, and muted
since some browsers prevent the autoplay of unmuted videos (thank them).

```html
<div class="compare">
  <video 
    class="compared compared-vertical" 
    data-compare-top="standard"
    data-compare-bottom="ours"
    loop muted autoplay
    >
    <source src="barber.webm" type="video/webm">
    <source src="barber.mp4" type="video/mp4">
    <p>Your browser doesn't support HTML5 video. Here is a <a href="barber.mp4">link to the video</a> instead.</p>
  </video>
</div>
```

## Styling

Styling is done through CSS. The important parts are that compare class
should have position relative since the magnifier placement depends on
that. The compared class should be hidden, since a canvas will be added,
and the compared elements will be splat on it. Its positioning is set to
absolute to remove it from the document flow, and prevent it from
occupying space. The magnifiers should be absolutely positioned. Their
size and shape is controlled with css. Round magnifiers can be obtained
using equal width and height, and a border-radius of half that size. The
overflow should be hidden to crop the (square) contained canvas to the
rounded corners. Do as you wish for the rest.
