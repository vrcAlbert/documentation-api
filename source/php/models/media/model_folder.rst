Model_Folder
############

.. php:namespace:: Nos\Media

.. php:class:: Model_Folder

	Extends :php:class:`Nos\\Orm\\Model`.

Relations
*********

.. php:attr:: children

	* Relation type: :term:`has_many`.
	* Model: :php:class:`Model_Folder`

.. php:attr:: media

	* Relation type: :term:`has_many`.
	* Model: :php:class:`Model_Media`


.. php:attr:: parent

	* Relation type: :term:`belongs_to`.
	* Model: :php:class:`Model_Folder`

Behaviours
**********

* :php:class:`Tree <Nos\\Orm_Behaviour_Tree>`
* :php:class:`Virtual path <Nos\\Orm_Behaviour_Virtualpath>`

Methods
*******

.. php:method:: delete_from_disk()

	:returns: ``True`` or ``false`` depending on whether the deletion was successful.

	Delete the folder and all its content (recursively).

.. php:method:: delete_public_cache()

	:returns: ``True`` or ``false`` depending on whether the deletion was successful.

	Delete all the public and cached entries (image thumbnails) of this folder

.. php:method:: path($file = '')

	:param string $file: A file name to append to the path.
	:returns: Absolute folder path.

.. php:method:: count_media()

	:returns: Number of media contained in the folder and all its sub-folders.

.. php:method:: count_media_usage()

	:returns: Number of media in use (by the applications) contained in this folder and all its sub-folders.
