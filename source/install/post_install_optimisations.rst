Optimisations après installation
================================


Configuration et activation de XSendFile
----------------------------------------

Pour comprendre ce qu'est XSendFile et à quoi il sert, c'est par ici : :doc:`/understand/media_centre`.


Apache
~~~~~~

Dans **Apache**, il existe un module **mod_xsendfile** qui fournit la fonctionnalité. Ensuite, il faut modifier votre
fichier .htaccess pour l'activer.

.. code-block:: apache

    # Post-installation optimisation
    <IfModule xsendfile_module>
        XSendFile On

        # Replace "novius-os-install-dir" by the real Novius OS installed directory
        XSendFilePath /novius-os-install-dir/local/data

    </IfModule>

Novius OS détecte tout seul la présence du module et active automatiquement l'envoi de fichiers avec XSendFile.


nginx
~~~~~

Dans **nginx**, XSendFile est activé par défaut, mais l'entête à utiliser est ``X-Accel-Redirect``. Dans ce cas, il
faut éditer votre fichier de configuration :file:`config.php` pour y renseigner cet entête :


.. code-block:: php
    :emphasize-lines: 6

    <?php
    return array(
        // ...
        'novius-os' => array(
            // ...
            'use_xsendfile' => 'X-Accel-Redirect',
        ),
    );


