Attachment
##########

.. php:class:: Attachment

	| Binds a file to an object.
	| Belongs to the namespace :php:ns:`Nos`

Configuration
*************

.. php:attr:: attached

	Required.
	The attached ID.

.. php:attr:: dir

	Required.
	Directory path, relative to :file:`local/data/files`, where the attachment is stored.

.. php:attr:: alias

	An URL alias for directory path.

.. php:attr:: extensions

	Array of valid files extensions.

.. php:attr:: image

	If ``true``, accepts only files with an image extension. Same that ``extensions`` set to ``array('jpg', 'gif', 'png', 'jpeg')``.

.. php:attr:: check

	A callback function if file not in public access. Function take the Attachement object for single parameter.

Methods
*******

.. php:staticmethod:: forge($attached, $config)

	:params string $attached: The attached ID.
	:params mixed $config: If is a ``string``, use it to load configuration array. ``Array`` otherwise:

		:dir: :php:attr:`Attachment::$dir`
		:alias: :php:attr:`Attachment::$alias`
		:extensions: :php:attr:`Attachment::$extensions`
		:image: :php:attr:`Attachment::$image`
		:check: :php:attr:`Attachment::$check`

	:returns: A new :php:class:`Attachment`.

.. php:method:: newFile()

	:returns: Get the new attachment file path if one, ``false`` if no.

.. php:method:: path()

	:returns: Get the attachment file path or ``false`` if no file.

.. php:method:: filename()

	:returns: Get the attachment filename or ``false`` if no file.

.. php:method:: extension()

	:returns: Get the attachment extension or ``false`` if no file.

.. php:method:: isImage()

	:returns: ``True`` if the Attachment is an image, ``false`` otherwise.

.. php:method:: url()

	:returns: Get the attachment url or ``false`` if no file.

.. php:method:: urlResized($max_width = 0, $max_height = 0)

	:params array $max_width: Max width of the image.
	:params array $max_height: Max height of the image.
	:returns: Get the url of Attachment resized or ``false`` if no file or not an image.

.. php:method:: set($file, $filename = null)

	:params array $file: File path
	:params array $filename: File name
	:returns: Set a new Attachment file.
	:throws: \Fuel\Core\FileAccessException if new file have a not allowed extension.

.. php:method:: save()

	Save a new Attachment file

.. php:method:: delete()

	Delete the Attachment file

Example
*******

.. code-block:: php

	<?php

	$attachment = \Nos\Attachment::forge('my_id', array(
		'dir' => 'apps'.DS.'myapps',
		'alias' => 'myapps-attachment',
		'extensions' => array('pdf'),
		'check' => 'check_attachment',
	));

	// It's for example, USED GLOBALS IS EVIL
	$GLOBALS['user_connected'] = true;

	function check_attachment($attachment) {
		return $GLOBALS['user_connected'];
	}

	try {
		$attachment->set('/path/a_doc.doc');
	} catch (\Fuel\Core\FileAccessException $e) {
		// Exception will be throw, extension is doc, not a pdf.
	}

	$attachment->set('/path/a_pdf.pdf');
	$attachment->save();

	// Now file saved in local/data/files/apps/myapps/my_id/a_pdf.pdf

	echo $attachment->url();
	// Echo data/files/myapps-attachment/my_id/a_pdf.pdf

	$GLOBALS['user_connected'] = false;
	// Now URL data/files/myapps-attachment/my_id/a_pdf.pdf return 404

	$attachment->delete();
