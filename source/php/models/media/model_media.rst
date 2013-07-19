Model_Media
###########

.. php:namespace:: Nos\Media

.. php:class:: Model_Media

	Extends :php:class:`Nos\\Orm\\Model`.

Relations
*********

.. php:attr:: folder

	* Relation type: :term:`belongs_to`.
	* Model: :php:class:`Model_Folder`

Behaviours
**********

* :php:class:`Virtual path <Nos\\Orm_Behaviour_Virtualpath>`

Methods
*******

.. php:method:: deleteFromDisk()

	Delete the original media file from the disk.

.. php:method:: deleteCache()

	Delete all the cached versions (thumbnails) of the media files from the disk.

.. php:method:: path()

	:returns: Private absolute media file path.

.. php:method:: htmlImg($params = array())

    :param array $params: the attributes array
    :returns: If the media file is an image, return an html image tag of the media.

    Sets width, height, alt attributes is not supplied.

.. php:method:: htmlImgResized($max_width = null, $max_height = null, $params = array())

    :param array $max_width: Max width of the image.
    :param array $max_height: Max height of the image.
    :param array $params: the attributes array
    :returns: If the media file is an image, return an html image tag of the media resized.

    Sets width, height, alt attributes is not supplied.

.. php:method:: htmlAnchor($attributes = array())

    :param array $attributes: | Array of attributes to be applied to the anchor tag.
                              | If key 'text' is set in $attributes parameter, its value replace media title
    :returns: Returns an HTML anchor tag with, by default, media URL in href and media title in text.

.. php:method:: url($absolute = true)

    :param bool $absolute: Default true, if false return relative URL
	:returns: Public media file URL.

.. php:method:: urlResized($max_width = 0, $max_height = 0, $absolute = true)

    :param array $max_width: Max width of the image.
    :param array $max_height: Max height of the image.
    :param bool $absolute: Default true, if false return relative URL
    :returns: If the media file is an image, media URL for specify size parameters. ``False`` otherwise.

.. php:method:: isImage()

	:returns: ``True`` or ``false``, depend if media is an image.
