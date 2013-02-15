.. _php/classes/controller_front:

Front controller
################

.. php:namespace:: Nos

.. php:class:: Controller_Front

	Novius OS front-office controller

	Use :php:meth:`Nos::main_controller` to retrieve his instance and then use its static methods.

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
			  | ``False`` if not current :ref:`URL enhancer <metadata/enhancers>`.

	Same that :php:meth:`Controller_Front::getPageUrl` but ``/`` ending instead of ``.html``.

.. php:staticmethod:: getEnhancerUrl()

	:returns: | Part of the URL processed by the :ref:`URL enhancer <metadata/enhancers>`.
			  | ``False`` if not current :ref:`URL enhancer <metadata/enhancers>`.

.. php:staticmethod:: setBaseHref($base_href)

	:params string $base_href: Set a new ``base_href`` for current webpage HTML output.

.. php:staticmethod:: setTitle($title, $template = null)

	:params string $title: Set a new title for current webpage HTML output.
	:params string $template: If set, use it for calculate title. Placeholder ``:title`` will be replaced by ``$title``.

.. php:staticmethod:: setMetaDescription($meta_description)

	:params string $meta_description: Set a meta description for current webpage HTML output.

.. php:staticmethod:: setMetaKeywords($meta_keywords)

	:params string $meta_keywords: Set a meta keywords for current webpage HTML output.

.. php:staticmethod:: setMetaRobots($meta_robots)

	:params string $meta_robots: Set a meta robots for current webpage HTML output.

.. php:staticmethod:: addMeta($meta)

	:params string $meta: A HTML meta tag to add at the current webpage HTML output.

.. php:staticmethod:: addJavascript($url, $footer = true)

	:params string $url: URL of a Javascript library to add at the current webpage HTML output.
	:params boolea $footer: If ``true``, add ``script`` at the end of HTML output. If ``false``, add in the ``<head>``.

.. php:staticmethod:: addJavascriptInline($js, $footer = true)

	:params string $url: Javascript code to add at the current webpage HTML output.
	:params boolea $footer: If ``true``, add ``script`` at the end of HTML output. If ``false``, add in the ``<head>``.

.. php:staticmethod:: addCss($url)

	:params string $url: URL of a CSS file to add at the current webpage HTML output.

.. php:staticmethod:: addCssInline($css)

	:params string $css: CSS code to add at the current webpage HTML output.

.. php:staticmethod:: isPreview()

	:returns: Boolean, ``true`` if current webpage is requested in preview mode.
