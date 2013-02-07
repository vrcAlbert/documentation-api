Conventions
###########

jQuery
------

.. js:data:: $

	In this documentation, ``$`` mean jQuery object itself.

	.. code-block:: js

		$.nosNotify('message');

.. js:data:: $context

	In this documentation, ``$context`` mean a jQuery collection of DOM elements.

	.. code-block:: js

		$('#id').nosTabs('open', {
			url: 'url',
			iframe: false,
			label: 'title',
			labelDisplay: true,
			iconUrl: 'icon.png',
			iconSize: 16
		});


.. _javascript/sub_function:

Function with sub-functions
---------------------------

Many functions of the Novius OS Javascript API have sub-functions. The first parameter is the name of a sub-function.
If this parameter is omit, sub-function default is called.

	.. code-block:: js

		$('#id').nosTabs('open', {
			url: 'url',
			iframe: false,
			label: 'title',
			labelDisplay: true,
			iconUrl: 'icon.png',
			iconSize: 16
		});

		// This call do the same thing that the prevent
		$('#id').nosTabs({
			url: 'url',
			iframe: false,
			label: 'title',
			labelDisplay: true,
			iconUrl: 'icon.png',
			iconSize: 16
		});
