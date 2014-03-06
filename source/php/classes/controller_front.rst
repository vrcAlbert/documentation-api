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

.. php:method:: getItemDisplayed()

    :returns:  The current item displayed.

    .. versionadded:: 4.1

.. php:method:: setItemDisplayed(Orm\Model $item, array $properties = array(), array $templates = array())

	:param Model $item: The current Model instance displayed.
	:param array $properties: Array of properties
	:param array $templates: Array of templates use to set properties

    .. versionadded:: 4.1

	Set de current item displayed, by default this item is the page displayed, but can be call by an URL enhancer.
	This method set automatically ``title``, ``h1``, ``meta_description`` and ``meta_keywords`` for the current HTML.

.. php:method:: setBaseHref($base_href)

	:param string $base_href: Sets a new ``<base href="">`` for the current HTML output.

.. php:method:: setTitle($title, $template = null)

	:param string $title: Set a new ``title`` for the current HTML.
	:param string $template: If set, use it to calculate the title. Placeholders ``:title`` will be replaced by ``$title``, ``:page_title`` will be replace by the curent page title.

.. php:method:: setH1($title, $template = null)

	:param string $title: Set a new ``H1`` for the current HTML.
	:param string $template: If set, use it to calculate the H1. Placeholders ``:h1`` will be replaced by ``$h1``.

    .. versionadded:: 4.1

.. php:method:: setMetaDescription($meta_description, $template = null)

    :param string $meta_description: Set a meta description for the current HTML output.
    :param string $template: If set, use it to calculate the meta_description. Placeholders ``:meta_description`` will be replaced by ``$meta_description``, ``:page_meta_description`` will be replace by the curent page meta_description.

.. php:method:: setMetaKeywords($meta_keywords, $template = null)

    :param string $meta_keywords: Set a meta keywords for the current HTML output.
    :param string $template: If set, use it to calculate the meta_keywords. Placeholders ``:meta_keywords`` will be replaced by ``$meta_keywords``, ``:page_meta_keywords`` will be replace by the curent page meta_keywords.

.. php:method:: setMetaRobots($meta_robots, $template = null)

    :param string $meta_robots: Set a meta robots for the current HTML output.
    :param string $template: If set, use it to calculate the meta_robots. Placeholders ``:meta_robots`` will be replaced by ``$meta_robots``, ``:page_meta_robots`` will be replace by the curent page meta_robots.

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

