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

.. php:method:: delete_from_disk()

	:returns: ``True`` or ``false`` depending on whether the deletion was successful.

	Delete the original media file from the disk.

.. php:method:: delete_public_cache()

	:returns: ``True`` or ``false`` depending on whether the deletion was successful.

	Delete all the cached versions (thumbnails) of the media files from the disk.

.. php:method:: get_path()

	:returns: Relative media file virtual path.

.. php:method:: get_public_path()

	:returns: Public media file URL relative to base href.

.. php:method:: get_private_path()

	:returns: Private media file path relative to Novius OS root directory.

.. php:method:: get_img_tag($params = array())

	:param array $params:

		:max_width:  Max width of the image.
		:max_height: Max height of the image.

	:returns: If the media file is an image, a HTML ``<img>`` tag with ``src``, ``width`` and ``height`` attributes, depends of ``$params``. ``False`` otherwise.

.. php:method:: get_img_tag_resized($max_width = null, $max_height = null)

	:param array $max_width: Max width of the image.
	:param array $max_height: Max height of the image.
	:returns: If the media file is an image, a HTML ``<img>`` tag with ``src``, ``width`` and ``height`` attributes. ``False`` otherwise.

	Alias of ``get_img_tag(array('width' => $max_width, 'height' => $max_height))``.

.. php:method:: get_img_infos($max_width = null, $max_height = null)

	:param array $max_width: Max width of the image.
	:param array $max_height: Max height of the image.
	:returns: If the media file is an image, an associative array with keys ``src``, ``width`` and ``height`` depends of size parameters. ``False`` otherwise.

.. php:method:: get_public_path_resized($max_width = 0, $max_height = 0)

	:param array $max_width: Max width of the image.
	:param array $max_height: Max height of the image.
	:returns: If the media file is an image, media URL relative to base href for specify size parameters. ``False`` otherwise.

.. php:method:: is_image()

	:returns: ``True`` or ``false``, depend if media is an image.
