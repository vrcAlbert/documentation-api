$container functions
####################

.. js:data:: $container

	In this documentation, ``$container`` means a jQuery collection of DOM elements.

	.. code-block:: js

		$('#id').nosTabs('open', {
			url: 'url',
			iframe: false,
			label: 'Title',
			labelDisplay: true,
			iconUrl: 'icon.png',
			iconSize: 16
		});


.. glossary::

	Function with sub-functions
		Many functions of the Novius OS Javascript API have sub-functions. The first parameter is the name of a sub-function.
		If this parameter is omitted, the default sub-function is called.

			.. code-block:: js

				$('#id').nosTabs('open', {
					url: 'url',
					iframe: false,
					label: 'Title',
					labelDisplay: true,
					iconUrl: 'icon.png',
					iconSize: 16
				});

				// This call do the same thing that the previous
				$('#id').nosTabs({
					url: 'url',
					iframe: false,
					label: 'Title',
					labelDisplay: true,
					iconUrl: 'icon.png',
					iconSize: 16
				});

Functions
*********

.. toctree::
	:glob:

	nos*
