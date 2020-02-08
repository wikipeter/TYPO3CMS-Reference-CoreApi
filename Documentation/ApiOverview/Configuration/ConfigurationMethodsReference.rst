.. include:: ../../Includes.txt


.. _configuration-reference:

===============================
Configuration methods reference
===============================

This section is a quick overview of "configuration methods". We will not
describe the method in detail but refer you to the relevant sections
in this manual or in another manual.

The glossary section :ref:`glossary-configuration-method` describes what a
"configuration method" is and what it is comprised of.

The various configuration syntaxes used in TYPO3 are not listed on this
page. See :ref:`configuration-syntax` for an overview.


.. _config-ref-global-configuration:

Global Configuration (TYPO3_CONF_VARS)
======================================


.. rst-class:: dl-parameters

Global Configuration
   :sep:`|` :aspect:`Schema Language:` YAML
   :sep:`|` :aspect:`Language:` PHP
   :sep:`|` :aspect:`Scope:` global
   :sep:`|` :aspect:`Persistence:` PHP file
   :sep:`|` :aspect:`Extendable:` core
   :sep:`|` :aspect:`Change values in BE:` most settings
   :sep:`|` :aspect:`Required privilege:` system maintainer
   :sep:`|` :aspect:`TYPO3 version:` since before 6.2

.. rst-class:: clear

Used for:
    System wide global configuration.

Global configuration uses a global PHP array :php:`$GLOBALS['TYPO3_CONF_VARS']`
for installation-wide setings. The settings can be changed in the backend.


Schema
------

* Default values: :file:`typo3/sysext/core/Configuration/DefaultConfiguration.php`
* Schema definition: :file:`typo3/sysext/core/Configuration/DefaultConfigurationDescription.yaml`

Persistence
-----------

Automatically generated file is :file:`typo3conf/LocalConfiguration.php`.

You can use :file:`typo3conf/AdditionalConfiguration.php` to extend the settings.


Example
-------

Change value :php:`$GLOBALS['TYPO3_CONF_VARS']['FE']'lockIP']`:

.. image:: _images/typo3_conf_vars.png
    :class: with-shadow


View settings
-------------

Backend: *Configuration* >> *Global Configuration*.

Debug: :php:`$GLOBALS['TYPO3_CONF_VARS']`

Change settings
---------------

You can change the global configuration values in the backend in
:guilabel:`"Settings" > "Configure Installation-Wide Options"`.

Additionally, it is possible to change settings in the file
:file:`typo3conf/AdditionalConfiguration.php`.

It is not possible to change all settings in the backend. In particular some
settings consists of variable settings in a hierarchical array. This is the
case for the caching configuration and logging framework configuration.

The :ref:`Caching Framework <caching>` can be configured by setting
:php:`$GLOBAL['TYPO3_CONF_VARS']['SYS']['caching']` in the file
:file:`typo3conf/AdditionalConfiguration.php`.

The `logging framework <caching-configuration-cache>` can be configured by
setting :php:`$GLOBALS['TYPO3_CONF_VARS']['LOG']` in :file:`typo3conf/AdditionalConfiguration.php`


Extend settings
---------------

The settings should only be extended in the core.


More information
----------------

.. rst-class:: horizbuttons-tip-m

* :ref:`Global Configuration <typo3ConfVars>`
* :ref:`t3start:system-modules-configuration` in "Getting Started"
* :ref:`caching-configuration-cache`.
* :ref:`logging-configuration`

.. rst-class:: clear

.. _config-ref-yaml:

YAML configuration methods
==========================


.. rst-class:: dl-parameters

Extension Configuration
   :sep:`|` :aspect:`Schema Language:` -
   :sep:`|` :aspect:`Language:` YAML
   :sep:`|` :aspect:`Scope:` various (see below)
   :sep:`|` :aspect:`Persistence:` YAML files
   :sep:`|` :aspect:`Extendable:` -
   :sep:`|` :aspect:`Change values in BE:` site only
   :sep:`|` :aspect:`Required privilege:` system maintainer
   :sep:`|` :aspect:`TYPO3 version:` since 9 (site)

.. rst-class:: clear


Used for:
   Various

Configuration using YAML has been increasingly used in the core
instead of other configuration methods like TSconfig, TypoScript
or Extension Configuration.

It is now used in the system extensions rte_ckeditor, form and
in the sites module.

The sites module features a combination: Parts of the configuration
can be configured in the sites module. The configuration is stored
as YAML files. The configuration can also be directly modfied in the
YAML file.

Here, we will list some general things and refer you to the
respective configuration documentation.


Schema
------

Currently, no schema is being used.

Persistence
-----------

sites module:

    file:`typo3conf/sites/<site shortcut>/config.yaml

form:

    The location of the configuration files are defined in TypoScript
    in :ts:`plugin.tx_form.settings.yamlConfiguration`. By default, this
    is :file:`EXT:form/Configuration/Yaml/FormSetup.yaml`. Several
    configurations can be setup with TypoScript and configuration files
    can import other configuration files.

rte_ckeditor:

    The configuration files are setup by adding presets to the Global
    Configuration $GLOBALS['TYPO3_CONF_VARS']['RTE']['Presets]'. Each
    preset can refer to one configuration file (which may also import
    others). By default, these are:

    * default: EXT:rte_ckeditor/Configuration/RTE/Default.yaml
    * full: EXT:rte_ckeditor/Configuration/RTE/Full.yaml
    * minimal: EXT:rte_ckeditor/Configuration/RTE/Minimal.yaml


Example
-------

View settings
-------------

Site:

    :guilabel:`Configuration > Site Configuration`

rte_ckeditor



Change settings
---------------

Extend settings
---------------

More information
----------------

.. rst-class:: horizbuttons-tip-m

* :ref:`Site configuration <sitehandling>`
* form: :ref:`Configuration introduction <form:concepts:configuration>`
* form: :ref:`Configuration reference <form:configurationreference>`
* rte_ckeditor:

.. rst-class:: clear


.. _config-ref-extconf:

Extension Configuration
=======================

.. rst-class:: dl-parameters

Extension Configuration
   :sep:`|` :aspect:`Schema Language:` TypoScript constants
   :sep:`|` :aspect:`Language:` PHP
   :sep:`|` :aspect:`Scope:` extension
   :sep:`|` :aspect:`Persistence:` PHP file
   :sep:`|` :aspect:`Extendable:` extension
   :sep:`|` :aspect:`Change values in BE:` yes
   :sep:`|` :aspect:`Required privilege:` system maintainer
   :sep:`|` :aspect:`TYPO3 version:` since before 6.2

.. rst-class:: clear


Used for:
   Configuration specific to an extension.


Extension configuration uses the same global PHP array as global
configuration. The values are stored in
`$GLOBALS['TYPO3_CONF_VARS']['EXTENSIONS']`.

The configuration is defined in an extension in the file :file:`ext_conf_template.txt`
It uses TypoScript constant syntax to define the properties.
The configuration can be changed in the backend.


Schema
------

Definition, description and default values in file `<extkey>/ext_conf_template.txt`

Persistence
-----------

The same as in Global Configuration. The values are stored in :file:`typo3conf/LocalConfiguration.php`.

Example
-------


Configuration of system extension "backend".

.. code-block:: typoscript

  # cat=Login; type=string; label=LLL:EXT:backend/Resources/Private/Language/locallang.xlf:config.loginLogo
  loginLogo =

  # cat=Login; type=color; label=LLL:EXT:backend/Resources/Private/Language/locallang.xlf:config.loginHighlightColor
  loginHighlightColor =

  # cat=Login; type=string; label=LLL:EXT:backend/Resources/Private/Language/locallang.xlf:config.loginBackgroundImage
  loginBackgroundImage =

  # cat=Login; type=string; label=LLL:EXT:backend/Resources/Private/Language/locallang.xlf:config.loginFootnote
  loginFootnote =

  # cat=Backend; type=string; label=LLL:EXT:backend/Resources/Private/Language/locallang.xlf:config.backendLogo
  backendLogo =

  # cat=Backend; type=string; label=LLL:EXT:backend/Resources/Private/Language/locallang.xlf:config.backendFavicon
  backendFavicon =


View settings
-------------

Backend: *Configuration* >> *Global Configuration*.

Debug: :php:`$GLOBALS['TYPO3_CONF_VARS']['EXT']['EXTENSION']`


Change settings
---------------

Backend: *Settings* >> *Extension Configuration*

Define / extend settings
------------------------

The configuration is defined in the file :file:`ext_conf_template.txt`
in the extension.

More information
----------------

.. rst-class:: horizbuttons-tip-m

* :ref:`extension-reserved-filenames`
* :ref:`extension-options`
* :ref:`Constant comment syntax <t3tsref:typoscript-syntax-constant-editor-comments>`

.. rst-class:: clear



.. _config-ref-tca:

TCA
===

.. rst-class:: dl-parameters

TCA
   :sep:`|` :aspect:`Language:` PHP
   :sep:`|` :aspect:`Scope:` global
   :sep:`|` :aspect:`Persistence:` PHP files
   :sep:`|` :aspect:`Extendable:` core, extensions
   :sep:`|` :aspect:`Change values in BE:` no
   :sep:`|` :aspect:`Required privilege:` -
   :sep:`|` :aspect:`TYPO3 version:` since before 6.2

.. rst-class:: clear

Used for:
   Change behaviour of database fields in the Backend.

The Table Configuration Array (TCA) is a PHP array :php:`$GLOBALS['TCA']`, which is used
to define database fields (beyond what is defined in the SQL scheam) and how they behave
and can be edited in the backend

Schema
------

* none, the schema is implicitly defined by filling the $GLOBALS['TCA'] array
* Default values in `<extkey>/Configuration/TCA`

Persistence
-----------

Example
-------


Field 'link' is defined to be an input field (type='input') of renderType
'inputLink' which adds button to open link wizard when editing this field
in the Backend.

.. code-block:: php

   'link' => array(
        'exclude' => 1,
        'label' => 'Link',
        'config' => array(
            'type' => 'input',
            'renderType' => 'inputLink',
        ),
    ),

.. image:: _images/linkwizard.png
  :class: with-shadow

See :ref:`t3tca:start` for more examples, for example :ref:`t3tca:columns-input-examples`
for examples for input fields.


View settings
-------------

Backend: *Configuration* >> *Global Configuration*.

Debug: :php:`$GLOBALS['TCA']`


Change settings
---------------

You can change values in extensions in a file
:file:`<extkey>/Configuration/TCA/Overrides/<tablename>.php`. This is explained
in detail in :ref:`extending`.


Extend settings
---------------

Extensions can define their own TCA in files in
:file:`<extkey>/Configuration/TCA/.

More information
----------------

.. rst-class:: horizbuttons-tip-m

* :ref:`extending`
* :ref:`t3tca:start`


.. rst-class:: clear



.. _config-ref-typoscript-method:

TypoScript
==========

.. rst-class:: dl-parameters

TypoScript
   :sep:`|` :aspect:`Schema Language:` none
   :sep:`|` :aspect:`Language:` TypoScript
   :sep:`|` :aspect:`Scope:` global | page
   :sep:`|` :aspect:`Persistence:` PHP files
   :sep:`|` :aspect:`Change values in BE:` yes
   :sep:`|` :aspect:`Extendable:` core, extensions
   :sep:`|` :aspect:`Required privilege:` admin
   :sep:`|` :aspect:`TYPO3 version:` since before 6.2

.. rst-class:: clear

Used for:
    Configuration of plugins (Frontend), Modules (Backend) and some global configuration
    used in the Frontend (:ref:`config. <tsref:config>`).

TypoScript is a configuration method that uses the configuration language TypoScript.

.. important::

   TypoScript is a configuration syntax **and** configuration method: The configuration syntax
   TypoScript can be used in TSconfig and TypoScript. A syntax variant, TypoScript constants is used in
   Extension Configuration and TypoScript constants.


Schema
------

* none
* Default values `<extkey>/Configuration/TypoScript`, typically in file
 setup.typoscript

Persistence
-----------

.. todo: Persistence

Example
-------

.. todo: Example:

View settings
-------------

Backend: *Template* : *TypoScript Object Browser*

Change settings
---------------

* Backend: *Template* >> *Info / Modify*
* Files: *<extkey>/Configuration/TypoScript/*

Extend settings
---------------

.. todo: Example:

More information
----------------

.. rst-class:: horizbuttons-tip-m

* :ref:`tsref:start`

.. rst-class:: clear


.. _config-ref-tsconfig:

TSconfig
========


.. rst-class:: dl-parameters

TSconfig
   :sep:`|` :aspect:`Schema Language:` none
   :sep:`|` :aspect:`Language:` TypoScript
   :sep:`|` :aspect:`Scope:` pages | user | usergroup
   :sep:`|` :aspect:`Persistence:` database, tsconfig files
   :sep:`|` :aspect:`Change values in BE:` yes
   :sep:`|` :aspect:`Extendable:` core
   :sep:`|` :aspect:`Required privilege:` admin
   :sep:`|` :aspect:`TYPO3 version:` since before 6.2

.. rst-class:: clear


Used for:
   TSconfig is used in TYPO3 to configure and customize the backend on a page
   and a user or group basis.


Values can be modified in the backend or in an extension, by supplying configuration files.


Schema
------

* none
* Default values `<extkey>/Configuration/TypoScript`, typically in file setup.txt or
 setup.typoscript


Persistence
-----------

Example
-------

.. todo:: Example:

View settings
-------------

To view Page TSconfig, use Backend: :guilabel:`"WEB" > "Info" > "Page TSconfig"`

Change settings
---------------

* Page TSconfig

 * Backend: *Page properties* >> *Resources* >> *Page TSconfig*
 * Files: `<extkey>/Configuration/TSconfig/`

* User TSconfig

 * Backend: *Backend users* >> Select *Backend users* in Combobox >> Edit user >> *Options* >> *TSconfig*
 * Backend: *Backend users* >> Select *Backend user groups* in Combobox >> Edit group >> *Options* >> *TSconfig*
 * Files in `<extkey>/Configuration/TSConfig`


Extend settings
---------------

.. todo:: extend settings TSconfig

More information
----------------

.. rst-class:: horizbuttons-tip-m

* :ref:`TSconfig <t3tsconfig:introduction>` in TSconfig Reference
* :ref:`tsconfig` in TYPO3 Explained


.. rst-class:: clear


.. _config-ref-flexform:

FlexForm
========

.. rst-class:: dl-parameters

Global Configuration
   :sep:`|` :aspect:`Schema Language:` XML
   :sep:`|` :aspect:`Language:` XML
   :sep:`|` :aspect:`Scope:` contentrecord
   :sep:`|` :aspect:`Persistence:` database
   :sep:`|` :aspect:`Extendable:` is defined in extension
   :sep:`|` :aspect:`Change values in BE:` yes
   :sep:`|` :aspect:`Required privilege:` editor
   :sep:`|` :aspect:`TYPO3 version:` since before 6.2

.. rst-class:: clear


Used for:
   Change behaviour of plugin on specific page.

A set of configurations for a plugin that is stored in the DB records
of the content record in the field tt_content.pi_flexform.


Schema
------

Definition + Default values in `<extkey>/Configuration/FlexForm/<filename>.xml`



Automatically generated:
    Database: `tt_content.pi_flexform`


Persistence
-----------

The settings are stored in the database field `tt_content.pi_flexform` of the
content record.

Example
-------

.. todo:: example FlexForm

View settings
-------------

?

.. todo:: view settings FlexForm

Change settings
---------------

The settings can be changed in the backend when editing the content element record. This
is possible for any backend user who has write permission to edit the the content element.


Extend settings
---------------

More information
----------------

.. rst-class:: horizbuttons-tip-m


.. rst-class:: clear


.. _config-ref-feature-toggles:

Feature toggles
===============

.. rst-class:: dl-parameters

Feature Toggles
   :sep:`|` :aspect:`Schema Language:`
   :sep:`|` :aspect:`Language:` PHP
   :sep:`|` :aspect:`Scope:` global, used in core
   :sep:`|` :aspect:`Persistence:` PHP file
   :sep:`|` :aspect:`Extendable:` core
   :sep:`|` :aspect:`Change values in BE:` yes
   :sep:`|` :aspect:`Required privilege:` system maintainer
   :sep:`|` :aspect:`TYPO3 version:` since 9.1, configuration in BE since 9.4

.. rst-class:: clear

Used for:
    Turn a feature on or off in the core.

Feature toggles are often used for new features that are not yet meant to be
turned on by default or older features that should still be supported.

The values are stored - like Global Configuration - in the :php:`$GLOBALS['TYPO3_CONF_VARS']`,
but the settings must be changed in a different card "Feature Toggles" in the backend.

Schema
------

* Default values `typo3/sysext/core/Configuration/DefaultConfiguration.php`
* Description + Definition: `typo3/sysext/core/Configuration/DefaultConfigurationDescription.yaml`

Persistence
-----------

The settings are stored in the automatically generated file :file:`typo3conf/LocalConfiguration.php`
- just like the other :php:`$GLOBALS['TYPO3_CONF']` settings.


Example
-------

View settings
-------------

In the backend: :guilabel:`SYSTEM > Configuration > Global Configuration > SYS > features`

Change settings
---------------

In the backend: :guilabel:`ADMIN TOOLS > Settings > Feature Toggles`

The feature toggles can additionally be changed by overriding
:php:``$GLOBALS['TYPO3_CONF']['SYS']['features']`

Extend settings
---------------

The settings are not meant to be extended by extensions.

More information
----------------


.. rst-class:: horizbuttons-tip-m

* :ref:`feature-toggles` in "TYPO3 Explained"
* `Feature: #83429 - Feature Toggles <https://docs.typo3.org/typo3cms/extensions/core/latest/Changelog/9.1/Feature-83429-FeatureToggles.html>`__ (in Changelog)
* `Feature: #83556 - Add toggle switches to FormEngine <https://docs.typo3.org/typo3cms/extensions/core/latest/Changelog/9.2/Feature-83556-AddToggleSwitchesToFormEngine.html>`__ (in Changelog)

.. rst-class:: clear


Further Resources
=================


* `Stackoverflow: In TYPO3, what is the difference between setup, constants, and TSConfig
  <https://stackoverflow.com/questions/5033306/in-typo3-what-is-the-difference-between-setup-constants-and-tsconfig>`__



.. ----------------------------------

.. rst-class:: dl-parameters

Global Configuration
   :sep:`|` :aspect:`Schema Language:` Yaml
   :sep:`|` :aspect:`Language:` PHP
   :sep:`|` :aspect:`Scope:` global
   :sep:`|` :aspect:`Persistence:` PHP files
   :sep:`|` :aspect:`Extendable:` core
   :sep:`|` :aspect:`Change values in BE:` most settings
   :sep:`|` :aspect:`Required privilege:` system maintainer
   :sep:`|` :aspect:`TYPO3 version:` since before 6.2

.. rst-class:: clear

Used for:
    System wide global configuration.

description ...

Schema
------

Persistence
-----------

Example
-------

View settings
-------------

Change settings
---------------

Extend settings
---------------

More information
----------------

.. rst-class:: horizbuttons-tip-m


.. rst-class:: clear
