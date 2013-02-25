nosDataReplace
##############

.. js:function:: $.nosDataReplace(object, data)

	Replaces placeholder defined by the ``{{placeholder}}`` pattern in a string or JSON.

	:param mixed object: A string or a JSON, where to search placeholder to replace.
	:param JSON data:    A JSON, ``placeholder => replacement value``.
	:returns:            Initial object with placeholders replaced.

	.. code-block:: js

		$.nosDataReplace(obj, data);

		$.nosDataReplace('exemple {{foo}}', {foo : 'bar'});
		// returns 'exemple bar'

		$.nosDataReplace({
			astring: 'example {{foo}}',
			json: {
				string: 'sample {{bar}}',
			}
		},
		{
			foo : 'bar',
			bar : 'foo'
		});
		//returns {
		//	astring: 'example bar',
		//	json: {
		//		string: 'sample foo',
		//}

