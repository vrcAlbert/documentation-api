.. _php/classes/controller_front:

Front controller
################

.. php:namespace:: Nos

.. php:class:: Controller_Front

	Novius OS front-office controller

	Use :php:meth:`Nos::main_controller` to retrieve its instance and call the methods.

Methods
*******

.. php:method:: getContext()

	:returns: The current :doc:`context <../configuration/software/multi_context>`.

.. php:method:: getContextUrl()

	:returns: Absolute URL of the current :doc:`context <../configuration/software/multi_context>`.

.. php:method:: getPage()

	:returns: Current :php:class:`Model_Page` displayed.

.. php:method:: getWysiwygName()

	:returns: Current :php:class:`wysiwyg <Model_Wysiwyg>` ID processed.

.. php:method:: getUrl()

	:returns: Current absolute URL.

.. php:method:: getPageUrl()

	:returns: Relative (to :php:meth:`Controller_Front::getContextUrl`) URL of the current page.

.. php:method:: getEnhancedUrlPath()

	:returns: | Relative (to :php:meth:`Controller_Front::getContextUrl`) URL of the current :ref:`URL enhancer <metadata/enhancers>`.
			  | ``False`` if no current :ref:`URL enhancer <metadata/enhancers>`.

	Same that :php:meth:`Controller_Front::getPageUrl` ending with ``/`` instead of ``.html``.

.. php:method:: getEnhancerUrl()

	:returns: | Part of the URL processed by the :ref:`URL enhancer <metadata/enhancers>`.
			  | ``False`` if no current :ref:`URL enhancer <metadata/enhancers>`.

.. php:method:: setBaseHref($base_href)

	:param string $base_href: Sets a new ``<base href="">`` for the current HTML output.

.. php:method:: setTitle($title, $template = null)

	:param string $title: Set a new ``title`` for the current HTML.
	:param string $template: If set, use it to calculate the title. Placeholder ``:title`` will be replaced by ``$title``.

.. php:method:: setMetaDescription($meta_description)

	:param string $meta_description: Set a meta description for the current HTML output.

.. php:method:: setMetaKeywords($meta_keywords)

	:param string $meta_keywords: Set a meta keywords for the current HTML output.

.. php:method:: setMetaRobots($meta_robots)

	:param string $meta_robots: Set a meta robots for the current HTML output.

.. php:method:: addMeta($meta)

	:param string $meta: A HTML meta tag to add in the current HTML output.

.. php:method:: addJavascript($url, $footer = true)

	:param string $url: URL of a JavaScript library to add in the current HTML output.
	:param boolean $footer: If ``true``, add ``script`` at the end of HTML output. If ``false``, add in the ``<head>``.

.. php:method:: addJavascriptInline($js, $footer = true)

	:param string $js: Javascript code to add in the current HTML output.
	:param boolean $footer: If ``true``, add at the end of HTML output. If ``false``, add in the ``<head>``.

.. php:method:: addCss($url)

	:param string $url: URL of a CSS file to add in the current HTML output.

.. php:method:: addCssInline($css)

	:param string $css: CSS code to add in the current HTML output.

.. php:method:: isPreview()

	:returns: Boolean, ``true`` if current page is requested in the preview mode.

.. php:method:: disableCaching()

	Disable caching and cache retrieve of the current page.

.. php:method:: setCacheDuration($cache_duration)

	:param int $cache_duration: Set a new cache duration of the current cache saving.

.. php:method:: setStatus($status)

	:param int $cache_duration: Set a new response status of the current response. This status will be saved in cache.

.. php:method:: setHeader($name, $value, $replace = true)

    Add or replace a header to current response. Headers will be saved in cache.

    :param string $name: The header name
    :param string $value: The header value
    :param boolean $replace: Whether to replace existing value for the header, will never overwrite/be overwritten when false


.. php:method:: getCustomData($item, $default = null)

    Returns a (dot notated) custom data of the current process.

    :param string $item: Name of the custom data, can be dot notated.
    :param mixed $default: The return value if the custom data isn't found.
    :returns: The custom data or default if not found.

.. php:method:: setCustomData($item, $value, $cached = false)

    Sets a (dot notated) custom data to the current process.

    :param string $item: A (dot notated) custom data key
    :param mixed $value: The custom data value
    :param boolean $cached: If custom data have to be cached

.. php:method:: sendContent($content)

    Replace the template by a specific content and stop treatments

    :param mixed $content: The new content, can be a string or a View.

.. php:method:: addCacheSuffixHandler($handler)

    Add a cache suffix handler for the current page

    :param array $handler: The cache suffix handler
    :returns: The cache instance if the cache path have changed, null otherwise.

