Tools_Context
#############

.. php:namespace:: Nos

.. php:class:: Tools_Context

	Provide static methods for work with yours contexts, sites and languages.

.. seealso::

	:doc:`/php/configuration/software/multi_context`

::contexts()
------------

.. php:staticmethod:: contexts()

	:returns: An array of all your valid contexts.

	.. code-block:: php

		$containers = \Nos\Tools_Context::contexts();
		foreach ($containers as $container_key => $container_urls) {
			// ....
		}

::sites()
-----------

.. php:staticmethod:: sites()

	:returns: An array of all your valid sites. Each site has a ``title`` and an ``alias``.

	.. code-block:: php

		$sites = \Nos\Tools_Context::sites();
		foreach ($sites as $site_key => $site_params) {
			$title = $site_params['title'];
			$alias = $site_params['alias'];
		}

::locales()
-----------

.. php:staticmethod:: locales()

	:returns: An array of all your valid locales. Each locale has a ``title`` and a flag's code ``flag``.

	.. code-block:: php

		$locales = \Nos\Tools_Context::locales();
		foreach ($locales as $locale_key => $locale_params) {
			$title = $locale_params['title'];
			$flag = $locale_params['flag'];
		}

::defaultContext()
------------------

.. php:staticmethod:: defaultContext()

	:returns: The code of default context of your Novius OS instance.

	.. code-block:: php

		$default_context_code = \Nos\Tools_Context::defaultContext();

::locale($container)
--------------------

.. php:staticmethod:: locale($container)

	:param string $container: A context code.

	:returns: Array of context's locale.

	.. code-block:: php

		$locale = \Nos\Tools_Context::locale('main::en_GB');
		$title = $locale['title'];
		$code_flag = $locale['flag'];

::site($container)
------------------

.. php:staticmethod:: site($container)

	:param string $container: A context code.

	:returns: Array of context's site.

	.. code-block:: php

		$site = \Nos\Tools_Context::site('main::en_GB');
		$title = $site['title'];
		$alias = $site['alias'];





