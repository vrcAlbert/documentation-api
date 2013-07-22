.. _php/classes/toolkit_image:

Toolkit Image
#############

.. php:namespace:: Nos

.. php:class:: Toolkit_Image

	Toolkit for image manipulation.

Usage
*****

To get a Toolkit_Image, use method getToolkitImage on classes supporting it.

* :php:meth:`Nos\\Media\\Model_Media::getToolkitImage()`
* :php:meth:`Nos\\Attachment::getToolkitImage()`

Methods
*******

.. php:method:: transformations($transformations)

    Add multiple transformations to the image.

    :param array $transformations:
        | Transformations to add to the image.
        | A transformation is an array where first value is the method name, others values are method arguments.
    :returns: The current Toolkit_Image for chaining.

.. php:method:: crop($x1, $y1, $x2, $y2)

    Add a crop transformation to the image.

    :param integer $x1: X-Coordinate based from the top-left corner.
    :param integer $y1: Y-Coordinate based from the top-left corner.
    :param integer $x2: X-Coordinate based from the bottom-right corner.
    :param integer $y2: Y-Coordinate based from the bottom-right corner.
    :returns: The current Toolkit_Image for chaining.


.. php:method:: resize($width, $height, $keepar = true, $pad = false)

    Resizes the image. If the width or height is ``null``, it will resize retaining the original aspect ratio.

    :param integer $width:  The new width of the image.
    :param integer $height: The new height of the image.
    :param boolean $keepar: Defaults to true. If ``false``, allows resizing without keeping aspect ratio.
    :param boolean $pad:    If set to true and ``$keepar`` is ``true``, it will pad the image with the configured background color.
    :returns: The current Toolkit_Image for chaining.

.. php:method:: shrink($max_width, $max_height)

    Resizes the image only if too big

    :param integer $max_width:   The max width of the image.
    :param integer $max_height:  The max height of the image.
    :returns: The current Toolkit_Image for chaining.

.. php:method:: crop_resize($width, $height)

    Resizes the image. If the width or height is ``null``, it will resize retaining the original aspect ratio.

    :param integer $width:   The new width of the image.
    :param integer $height:  The new height of the image.
    :returns: The current Toolkit_Image for chaining.

.. php:method:: rotate($degrees)

    Rotates the image

    :param integer $degrees: The degrees to rotate, negatives integers allowed.
    :returns: The current Toolkit_Image for chaining.

.. php:method:: flip($direction)

    Creates a vertical / horizontal or both mirror image.

    :param string $direction: ``vertical``, ``horizontal``, ``both``
    :returns: The current Toolkit_Image for chaining.

.. php:method:: watermark($filename, $position, $padding = 5)

    Adds a watermark to the image.

    :param string  $filename:  The filename of the watermark file to use.
    :param string  $position:  The position of the watermark, ex: ``bottom right``, ``center center``, ``top left``
    :param integer $padding:   The spacing between the edge of the image.
    :returns: The current Toolkit_Image for chaining.

.. php:method:: border($size, $color = null)

    Adds a border to the image.

    :param integer $size:   The side of the border, in pixels.
    :param string  $color:  A hexidecimal color.
    :returns: The current Toolkit_Image for chaining.

.. php:method:: mask($maskimage)

    Masks the image using the alpha channel of the image input.

    :param string $maskimage:  The location of the image to use as the mask
    :returns: The current Toolkit_Image for chaining.

.. php:method:: rounded($radius, $sides = null, $antialias = null)

    Adds rounded corners to the image.

    :param integer $radius:
    :param integer $sides:      Accepts any combination of ``tl tr bl br`` seperated by spaces, or null for all sides
    :param integer $antialias:  Sets the antialias range.
    :returns: The current Toolkit_Image for chaining.

.. php:method:: grayscale()

    Turns the image into a grayscale version

    :returns: The current Toolkit_Image for chaining.

.. php:method:: url($absolute = true)

    Build and return the URL of the modify image

    :param bool $absolute: Default ``true``, if ``false`` return relative URL
    :return: The URL of the modify image.

.. php:method:: sizes()

    :return: The dimensions of the modify image (an object containing width and height variables).

.. php:method:: html($params = array())

    Creates an html image tag of the modify image

    Sets width, height, alt attributes if not supplied.

    :param array $params: The attributes array
    :return: The image tag

.. php:method:: save()

    Apply transformations of the Image_URL instance on a file and save it

    :return: The save file path

.. php:method:: parse($image_url)

    Parse an existing modify URL and set transformations in queue. Check if the hash part of the URL match.

    :param string $image_url: Modify URL of the image
    :return: ``True`` or ``false`` if the hash part of the URL not match.


Example
*******

.. code-block:: php

    <?php

    $all_media_png = \Nos\Media\Model_Media::find('all', array(
        'where' => array(
            array('media_ext', 'png'),
        ),
    )); // Get all images PNG in media

    // Display all PNG, shrinked in 200x100, grayscale and rounded with a 5px radius, in a <img class="css_class" /> tag.
    foreach ($all_media_png as $media) {
        echo $media->getToolkitImage()->shrink(200, 100)->grayscale()->rounded(5)->html(array(
            'class' => 'css_class',
        ));
    }
