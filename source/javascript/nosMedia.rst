nosMedia
########

.. js:function:: $context.nosMedia([options])

	Transform an ``<input type="hidden">`` element to a media selector UI in Media Center using plugin `inputFileThumb <http://www.novius-labs.com/contributions/jquery-plugin-inputfile/documentation.html>`_.

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

nosMediaVisualise
#################

.. js:function:: $.nosMediaVisualise(media)

	Display a media, in a popup for images or in a new browser window for others.

	:param JSON media: Media parameters

		:path: ``string``. Media URL.
		:image: ``boolean``.

	.. code-block:: js

		$.nosMediaVisualise({
			path: 'url/of/media/',
			image: true
		});
