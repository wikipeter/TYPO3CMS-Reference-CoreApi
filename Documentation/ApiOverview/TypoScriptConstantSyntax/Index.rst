.. include:: ../../Includes.txt


.. _typoscript-constant-syntax:


==========================
TypoScript constant syntax
==========================

TypoScript constant syntax is a syntax similar to :ref:`TypoScript syntax <typoscript-syntax-start>`.
But it differs in several ways:

* TypoScript constant syntax is based on a more restrictive subset of TypoScript syntax:

  * It is for example not possible to use conditions for constants

* A :ref:`constant declaration <ts-constant-syntax-constant-declaration>`
  can be used to define a constant.

Like TypoScript syntax, it is case sensitive.

Example 1: Simple variable / value assignment

    In its simplest form, we have a variable = value assignment:

    .. code-block:: typoscript

       variable = value


Example 2: Using a constant declaration


    .. code-block:: typoscript
       :linenos:

        # cat=Login; type=string; label=Login message;Some descriptive text (default: empty)
        loginMessage=

        # cat=Login; type=options[default,cas]; label=Login method; Use 'default' or 'cas'. Default is 'default'.
        loginType=default

        # cat=Login; type=boolean; label=Disable login; Login can be disabled
        loginDisable=0


    Line 1 is a constant declaration, which describes the constant `loginMessage`.
    The loginMessage is of the type string.

Example 3: Hierarchical variables (nested structure)

    Link in TypoScript, hierarchical variables can be used.

    .. code-block:: typoscript

    plugin.tx_indexedsearch {
        view {
                # cat=plugin.tx_indexedsearch/file; type=string; label=Path to template root (FE)
                templateRootPath = EXT:indexed_search/Resources/Private/Templates/

                # cat=plugin.tx_indexedsearch/file; type=string; label=Path to template partials (FE)
                partialRootPath = EXT:indexed_search/Resources/Private/Partials/
        }
    }



Where is constant syntax used?
==============================

TypoScript constant syntax is used in :ref:`constants in TypoScript templating <t3tsref:typoscript-syntax-constants>`
and in :ref:`Extension Configuration <extension-configuration>`.

.. _ts-constant-syntax-constant-declaration:

Constant declaration
====================

This is a line directly before the declaration which starts with a `#`
(like a comment in TypoScript).


.. code-block:: typoscript
   :linenos:

    # cat=Login; type=string; label=Login message;Some descriptive text (default: empty)
    loginMessage=


This line defines:

cat
    Category. This is used to group several options into one tab in the
    settings form in the backend.

type
    Data type: string | int | ...

    ============= ==========================
    Option type   Description
    ============= ==========================
    boolean       checkbox
    color         colorpicker
    int           integer value
    int+          positive integer value
    integer       integer value
    offset        offset
    options       option select
    small         small text field
    string        text field
    user          user function
    wrap          wrap field
    ============= ==========================


    Where user functions have to be written the following way:

.. code-block:: typoscript

   # cat=basic/enable/050; type=user[Vendor\MyExtensionKey\ViewHelpers\MyConfigurationClass->render]; label=MyLabel
   myVariable = 1

label
    A title and description of the option. The semicolon is used to separate
    the title and description.

Nested structure (hierarchical variables)
=========================================

You can also define nested options using the TypoScript notation:

.. code-block:: typoscript

    directories {
       # cat=basic/enable; type=string; label=Path to the temporary directory
       tmp =
       # cat=basic/enable; type=string; label=Path to the cache directory
       cache =
    }


Values
======

It is possible to assign values which refer to a file in an extension:

.. code-blocK:: typoscript

   # cat=plugin.tx_indexedsearch/file; type=string; label=Path to template root (FE)
   templateRootPath = EXT:indexed_search/Resources/Private/Templates/

This example was taken from the system extension indexed_search.