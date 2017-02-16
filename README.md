# imageLightbox.js
A JavaScript plugin for touch-friendly image lightbox.

## Usage and Demo
Read [how to use it](https://osvaldas.info/image-lightbox-responsive-touch-friendly).
Check the [demo](https://osvaldas.info/examples/image-lightbox-responsive-touch-friendly).

## Features

1. Ascetic. No captions, navigation buttons or background cover by default. Nothing that would distract user from the main purpose. That’s why I enjoy pointing out Jony Ive’s observation: “An indicator has a value when it’s indicating something, but if it’s not indicating something, it shouldn’t be there”. I think it is the most common thing that designers forget to solve.
2. Minimalistic. No bunch of default raster image files that fail on higher resolution screens. Just one source file which is only 4kb in size when minified.
3. No messy markup. Just one simple element – <img>.
4. Extensible & configurable. If the default functionality is not enough, you can easily extend the plugin with custom JavaScript functions, change the settings or use a couple of useful method functions.
5. Responsive and touch-friendly. The most trending topics in web design and they are here. Images fit to any screen size and are swipe-able (native behavior) on touch capable devices.
6. iOS, Android and Windows Phone compatible. As well as desktop versions of Safari, Chrome, Firefox, Opera and Internet Explorer.
7. jQuery 1.x, 2.x, 3.x compatible. Just saying.
8. Preloads next image. While user is viewing the current picture, the plugin silently preloads the next picture which shows up without any delay when respective action is triggered.
9. Uses CSS transform and transition for moving images. Turns out CSS’s transform performs better than left (as well as right, top, bottom). But the plugin falls back on left if a browser does not support transform.
10. Interacts with keyboard. Standard, but essential Arrow Left, Arrow Right to switch images and Esc to quit the lightbox.

## HTML

As I mentioned earlier, the plugin produces a single-element markup by default:

    <img src="picture.jpg" id="imagelightbox" />

## CSS

No default CSS. Everything is up to you. The minimal configuration I recommend is:

    #imagelightbox
    {
        position: fixed;
        z-index: 9999;

        -ms-touch-action: none;
        touch-action: none;
    }
    
position value can be anything, but in most cases fixed will produce what’s expected. Configure z-index to anything that fits your ecosystem best. touch-action: none removes the default touch manipulation from the element.

## JavaScript

Source: imagelightbox.js https://osvaldas.info/examples/image-lightbox-responsive-touch-friendly/imagelightbox.js (uncompressed; 9kb) and imagelightbox.min.js https://osvaldas.info/examples/image-lightbox-responsive-touch-friendly/imagelightbox.min.js (minified; 4kb).

The plugin takes the advantage of jQuery. That means the plugin code or file must follow jQuery code or file. An example of the basic implementation:

    <script src="jquery.js"></script>
    <script src="imagelightbox.js"></script>
    <script>
        $( function()
        {
            $( 'a' ).imageLightbox();
        });
    </script>

ImageLightbox() accepts some options. The defaults are:

    $( selector ).imageLightbox(
    {
        selector:       'id="imagelightbox"',   // string;
        allowedTypes:   'png|jpg|jpeg|gif',     // string;
        animationSpeed: 250,                    // integer;
        preloadNext:    true,                   // bool;            silently preload the next image
        enableKeyboard: true,                   // bool;            enable keyboard shortcuts (arrows Left/Right and Esc)
        quitOnEnd:      false,                  // bool;            quit after viewing the last image
        quitOnImgClick: false,                  // bool;            quit when the viewed image is clicked
        quitOnDocClick: true,                   // bool;            quit when anything but the viewed image is clicked
        onStart:        false,                  // function/bool;   calls function when the lightbox starts
        onEnd:          false,                  // function/bool;   calls function when the lightbox quits
        onLoadStart:    false,                  // function/bool;   calls function when the image load begins
        onLoadEnd:      false                   // function/bool;   calls function when the image finishes loading
    });

It also has a couple of method functions, as mentioned:

    var $instance = $( selector ).imageLightbox();

    $instance.switchImageLightbox( index );
    // switches to the other image; accepts integer argument (an index of the desired image)

    $instance.quitImageLightbox();
    // quits the lightbox

    $instance.addToImageLightbox( $( 'a.is-new' ) );
    // quits the lightbox
