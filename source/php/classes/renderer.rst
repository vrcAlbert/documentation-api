Renderer
########

.. php:namespace:: Nos

.. php:class:: Renderer

    Extends the class ``Fieldset_Field`` of FuelPHP.

Configuration
*************

.. php:attr:: DEFAULT_RENDERER_OPTIONS

	Static and protected. The default renderer options.

.. php:attr:: renderer_options

	Protected. The renderer options.

Methods
*******

.. php:method:: setRendererOptions($options)

	:param array $options: Options merged with current renderer options.

.. php:staticmethod:: parseOptions($renderer = array())

	:param array $renderer: The renderer configuration.
	:returns: array 0: attributes, 1: renderer options
