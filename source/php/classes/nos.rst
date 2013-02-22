Nos
####

.. php:namespace:: Nos

.. php:class:: Nos

	Provides static methods useful in Novius OS.

::main_controller()
-------------------

.. php:staticmethod:: main_controller()

	:returns: Instance of the main :term:`controller <Controller>`.

::hmvc()
--------

.. php:staticmethod:: hmvc($where, $args = null)

	:param mixed $where: Route for the request.
	:param array $args: The method parameters.

	Executes an :term:`HMVC` request.

::parse_wysiwyg()
-----------------

.. php:staticmethod:: parse_wysiwyg($content)

	:param string $content: A :php:class:`Nos\\Model_Wysiwyg` content.
	:returns: Prepare wysiwyg content for display.

	| Replace enhancers by their content.
	| Replace :php:class:`Model_Page` and :php:class:`Model_Media` IDs by theirs URLs
	| Add URL prefix on anchors (to work with ``<base href="">``).
