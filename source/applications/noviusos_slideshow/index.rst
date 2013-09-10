.. _applications/noviusos_slideshow:

Slideshow Application
#####################

To modify configuration of slideshow, extend configuration file :file:`noviusos_slideshow::slideshow`.

Configuration
*************

:default_format: The default format. ``flexslider-big`` by default.
:formats:
    :flexslider-big:
        :view: The view use to display the slideshow. Default :file:`noviusos_slideshow::flexslider/slideshow`.
        :label: The label of the format, displayed in enhancer popup.
        :config:
            :slides_with_link: Boolean. Add a link on image if true and slide linked to a page. Default ``true``.
            :slides_preview: Boolean. Add a toolbar preview on the slideshow. Default ``true``.
            :width: Width in pixels of the slideshow. Default ``800``.
            :height: Height in pixels of the slideshow. Default ``600``.
            :class: CSS class add on the slideshow HTML container. Default ``slide-home``.
            :js:
                :jquery: Relative URL of jQuery script.
                :flexslider: Relative URL of Flexslider script.
                :flexpreview: Relative URL of Flexslider preview script.
            :css:
                :flexslider: Relative URL of Flexslider CSS file.
                :flexpreview: Relative URL of Flexslider preview CSS file.
    :flexslider-small:
        :view: The view use to display the slideshow. Default :file:`noviusos_slideshow::flexslider/slideshow`.
        :label: The label of the format, displayed in enhancer popup.
            :config:
            :slides_with_link: Boolean. Add a link on image if true and slide linked to a page. Default ``true``.
            :slides_preview: Boolean. Add a toolbar preview on the slideshow. Default ``true``.
            :width: Width in pixels of the slideshow. Default ``414``.
            :height: Height in pixels of the slideshow. Default ``300``.
            :class: CSS class add on the slideshow HTML container. Default ``slide-small``.
            :js:
                    :jquery: Relative URL of jQuery script.
                    :flexslider: Relative URL of Flexslider script.
                    :flexpreview: Relative URL of Flexslider preview script.
                :css:
                    :flexslider: Relative URL of Flexslider CSS file.
                    :flexpreview: Relative URL of Flexslider preview CSS file.

You can add your own formats. Keys ``view`` and ``label`` are required in your format. If defined, the key ``config`` is passed to the displaying view.


Flexslider
----------

You can configure Flexslider formats by extend configuration file :file:`noviusos_slideshow::formats/flexslider`.

:animation: Select your animation type, ``fade`` or ``slide``. Default ``fade``.
:slideDirection: Select the sliding direction, ``horizontal`` or ``vertical``.
:slideshow: Boolean, animate slider automatically. Default ``true``.
:slideshowSpeed: Integer, set the speed of the slideshow cycling, in milliseconds.
:animationDuration: Integer, set the speed of animations, in milliseconds.
:directionNav: Boolean, create navigation for previous/next navigation.
:controlNav: Boolean, create navigation for paging control of each slide. Note: Leave true for manualControls usage.
:keyboardNav: Boolean, allow slider navigating via keyboard left/right keys.
:mousewheel: Boolean, allow slider navigating via mousewheel.
:prevText: Set the text for the ``previous`` directionNav item.
:nextText: Set the text for the ``next`` directionNav item.
:pausePlay: Boolean, create pause/play dynamic element.
:pauseText: Set the text for the ``pause`` pausePlay item.
:playText: Set the text for the ``play`` pausePlay item.
:randomize: Boolean, randomize slide order.
:slideToStart: Integer, the slide that the slider should start on. Array notation (0 = first slide).
:animationLoop: Boolean, should the animation loop? If false, directionNav will received "disable" classes at either end.
:pauseOnAction: Boolean, pause the slideshow when interacting with control elements, highly recommended.
:pauseOnHover: Boolean, pause the slideshow when hovering over slider, then resume when no longer hovering.
:controlsContainer: Selector, declare which container the navigation elements should be appended too. Default container is the flexSlider element. Example use would be ``".flexslider-container", "#container"``, etc. If the given element is not found, the default action will be taken.
:manualControls: Selector, declare custom control navigation. Example would be ``".flex-control-nav li"`` or ``"#tabs-nav li img"``, etc. The number of elements in your controlNav should match the number of slides/tabs.
