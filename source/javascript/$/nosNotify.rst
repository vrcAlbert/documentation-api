nosNotify
#########

.. js:function:: $.nosNotify(message[, type])

	Displays notification(s) to the user. This is a wrapper of the jQuery plugin `Pines Notify <http://pinesframework.org/pnotify/>`__.

	:param mixed message: ``string`` The message to display or a JSON for special configuration.
	:param string type:   Type of the message. Can be ``notice`` (default), ``info``, ``success`` or ``error``.

	.. code-block:: js

		$.nosNotify('message');

		$.nosNotify('message', 'error');

		$.nosNotify({
			title: 'It\'s working',
			type: 'success'
			sticker: false, // Don't provide a button for the user to manually stick the notice.
			hide: false, // Don't remove the notification after a delay.
		});

