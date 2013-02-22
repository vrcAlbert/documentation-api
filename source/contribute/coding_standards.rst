Normes de codage
=====================================

Ces normes pour le formatage du code doivent être suivies par toute personne contribuant à Novius OS.

Vous pouvez utiliser le `ruleset.xml for PHP_CodeSniffer <https://github.com/novius-os/ci/blob/dev/phpcs/ruleset.xml>`_ fait pour Novius OS.

Case
----

Tous les mots clés sont en minuscule (``class``, ``interface``, ``extends``, ``implements``, ``abstract``, ``final``, ``var``, ``const``, ``function``, ``public``, ``private``, ``protected``, ``static``, ``if``, ``else``, ``elseif``, ``foreach``, ``for``, ``do``, ``switch``, ``while``, ``try``, ``catch``, ``true``, ``false`` et ``null``).

Toutes les constantes sont majuscules (constante globale ou de classe).

Signature des structures de contrôle
------------------------------------

.. code-block:: php

	try {
	    ...
	} catch (...) {
	    ...
	}

	do {
	    ...
	} while (...);

	while (...) {
	    ...
	}

	// Un seul espace entre chaque condition des boucles 'for'.
	for ($i = 0; $i < 10; $i++) {
	    ...
	}

	// Un seul espace entre chaque condition des boucles 'foreach'.
	foreach ($array as $key => $item) {
	    ...
	}

	if (...) {
	    ...
	} else if (...) {
	    ...
	} else {
	    ...
	}

	// Un seul espace après un cast.
	$variable = (array) $variable;


Déclaration de fonction
-----------------------

.. code-block:: php

	/*
	L'accolade d'ouverture d'une fonction est sur la ligne suivant la déclaration de la fonction.
	Pas d'espace avant les virgules.
	Un seul espace après les virgules.
	Un seul espace entre le type et l'argument.
	Un seul espace avant le signe '=' de la valeur par défaut.
	Un seul espace après le signe '=' de la valeur par défaut.
	Les paramètres avec une valeur par défaut doivent être à la fin de la signature de la fonction.
	*/
	function myfunction(array $first, $second, $third = array())
	{
		...
	}

Appel de fonction
-----------------

.. code-block:: php

	/*
	Pas d'espace avant les virgules.
	Un seul espace après les virgules.
	*/
	$value = myfunction($first, $second, $third);


Classe
------

.. code-block:: php

	/*
	L'accolade d'ouverture d'une classe est sur la ligne suivant la déclaration de la classe.
	Il doit y avoir une ligne vide après la déclaration du namespace.
	Toutes les propriétés de la classe doivent avoir une portée (variables, functions and methods).
	A single space after scope keywords (private, public, protected, static).
	*/
	namespace Name\Space;

	class MyClass
	{
		private $variable1 = null;

		protected static $variable1 = true;

		const MY_CONSTANT = false;

		public static function myfunction()
		{
			...
		}
	}

Fichier
-------

Les caractères de fin de ligne doivent être un \n.
Les fichiers ne doivent pas se finir par un tag de fermeture PHP.

Seulement une instruction par ligne.

Le code PHP doit utilisé les tags longs <?php ?> ou les tags courts d'affichage <?= ?>; aucune autre forme de tag ne doit être utilisée.

Les accolades de fermeture de même portée doivent être alignées.
Les structures de contrôles sont correctement indentées (4 espaces, pas de tabulation).

Pas d'espace en début et fin de fichier.
