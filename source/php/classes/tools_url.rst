Tools_Url
#########

.. php:namespace:: Nos

.. php:class:: Tools_Url

	Provides static methods for URL.

::page()
--------

.. php:staticmethod:: page($page_id)

	:param int $page_id: A :php:class:`Model_Page` ID.
	:returns: URL of the specified page.


::context()
-----------

.. php:staticmethod:: context($context)

	:param string $context: A context ID. See :doc:`/php/configuration/software/multi_context`.
	:returns: Home URL of the specified context.

::encodePath()
--------------

.. php:staticmethod:: encodePath($url)

	:param string $url:  Url to encode
	:returns: Encode the path part of an URL.
