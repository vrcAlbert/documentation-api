nosMedia
########

.. js:function:: $container.nosMedia([options])

	Transforms an ``<input type="hidden">`` element into a media selector UI in Media Center using plugin `inputFileThumb <http://www.novius-labs.com/contributions/jquery-plugin-inputfile/documentation.html>`__.

	:param JSON options: Optional options

		:mode: ``string``. Can be ``image`` (default) or ``all``.
		:inputFileThumb: ``{}``. options for ``inputFileThumb`` plugin.

	.. code-block:: js

		$(:input).nosMedia();

		$(:input).nosMedia({
			mode: 'image',
			inputFileThumb: {
				title: 'a title'
			}
		});

	.. seealso:: :ref:`php/renderers/media`.

nosMediaVisualise
#################

.. js:function:: $.nosMediaVisualise(media)

	Displays a media, in a popup for images or in a new browser window for other documents (like PDF).

	:param JSON media: Media parameters

		:path: ``string``. Media URL.
		:image: ``boolean``.

	.. code-block:: js

		$.nosMediaVisualise({
			path: 'url/of/media/',
			image: true
		});
