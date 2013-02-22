.. _php/classes/controller_front:

Front controller
################

.. php:namespace:: Nos

.. php:class:: Controller_Front

	Novius OS front-office controller

	Use :php:meth:`Nos::main_controller` to retrieve its instance and call the static methods.

Methods
*******

.. php:staticmethod:: getContextUrl()

	:returns: Absolute URL of the current :doc:`context <../configuration/software/multi_context>`.


.. php:staticmethod:: getPage()

	:returns: Current :php:class:`Model_Page` displayed.

.. php:staticmethod:: getWysiwygName()

	:returns: Current :php:class:`wysiwyg <Model_Wysiwyg>` ID processed.

.. php:staticmethod:: getUrl()

	:returns: Current absolute URL.

.. php:staticmethod:: getPageUrl()

	:returns: Relative (to :php:meth:`Controller_Front::getContextUrl`) URL of the current page.

.. php:staticmethod:: getEnhancedUrlPath()

	:returns: | Relative (to :php:meth:`Controller_Front::getContextUrl`) URL of the current :ref:`URL enhancer <metadata/enhancers>`.
			  | ``False`` if no current :ref:`URL enhancer <metadata/enhancers>`.

	Same that :php:meth:`Controller_Front::getPageUrl` ending with ``/`` instead of ``.html``.

.. php:staticmethod:: getEnhancerUrl()

	:returns: | Part of the URL processed by the :ref:`URL enhancer <metadata/enhancers>`.
			  | ``False`` if no current :ref:`URL enhancer <metadata/enhancers>`.

.. php:staticmethod:: setBaseHref($base_href)

	:param string $base_href: Sets a new ``<base href="">`` for the current HTML output.

.. php:staticmethod:: setTitle($title, $template = null)

	:param string $title: Set a new ``title`` for the current HTML.
	:param string $template: If set, use it to calculate the title. Placeholder ``:title`` will be replaced by ``$title``.

.. php:staticmethod:: setMetaDescription($meta_description)

	:param string $meta_description: Set a meta description for the current HTML output.

.. php:staticmethod:: setMetaKeywords($meta_keywords)

	:param string $meta_keywords: Set a meta keywords for the current HTML output.

.. php:staticmethod:: setMetaRobots($meta_robots)

	:param string $meta_robots: Set a meta robots for the current HTML output.

.. php:staticmethod:: addMeta($meta)

	:param string $meta: A HTML meta tag to add in the current HTML output.

.. php:staticmethod:: addJavascript($url, $footer = true)

	:param string $url: URL of a JavaScript library to add in the current HTML output.
	:param boolea $footer: If ``true``, add ``script`` at the end of HTML output. If ``false``, add in the ``<head>``.

.. php:staticmethod:: addJavascriptInline($js, $footer = true)

	:param string $url: Javascript code to add in the current HTML output.
	:param boolea $footer: If ``true``, add ``script`` at the end of HTML output. If ``false``, add in the ``<head>``.

.. php:staticmethod:: addCss($url)

	:param string $url: URL of a CSS file to add in the current HTML output.

.. php:staticmethod:: addCssInline($css)

	:param string $css: CSS code to add in the current HTML output.

.. php:staticmethod:: isPreview()

	:returns: Boolean, ``true`` if current page is requested in the preview mode.
