

.. _decomposed-config-lang:

Configuration languages
=======================

.. _decomposed-config-lang-yaml:

Yaml syntax
-----------


`Yaml <https://en.wikipedia.org/wiki/YAML>`__ is not specific to TYPO3.

Yaml is very well readable for machines and humans. It is commonly used for configuration files,
but can be used for other things as well.

Yaml is used for example in the system extension rte_ckeditor, form
or the site module as configuration language.

.. _decomposed-config-lang-typoscript:

TypoScript syntax
-----------------

TypoScript has been excessively explained elsewhere. Please see the following
information for a description of the syntax:

More information:
   * :ref:`typoscript-syntax-syntax`
   * :ref:`typoscript-syntax-what-is-typoscript`


.. _decomposed-config-lang-typoscript-constants:

TypoScript constants syntax
---------------------------

Constants are a subset of TypoScript. The syntax is very similar to TypoScript syntax.
This can lead to confusion because the variables are often named similar, but constants
and TypoScript setup are changed in different places. By using constants, the TypoScript
can be kept general and later simply be configured differently by changing constants.

The constants have no effect by themselves. They are used in TypoScript setup as variables.

For example:

constant:

.. code-block:: none

    plugin.tx_extkey.form.spamCheck = default

Setup uses the constant:

.. code-block:: none

   plugin.tx_extkey.settings.form.spamCheck = {$plugin.tx_extkey.spamCheck}


Before each constant assignment, you should add a descriptive line that defines the data
type and adds a category and label. These are later used in the constant editor.

.. todo: show contant editor

Example:

.. code-block:: none

   # cat=plugin.tx_extkey/form; type=string; label=Configure spam checking (default|captcha|none)
   plugin.tx_extkey.form.spamCheck = default

More information:

   * :ref:`t3tsref:typoscript-syntax-constants`
   * :ref:`Constant comment syntax <t3tsref:typoscript-syntax-constant-editor-comments>`


.. _decomposed-config-lang-symfony-expressionlang:

Symfony ExpressionLanguage
--------------------------

The `Symfony ExpressionLanguage <https://symfony.com/doc/current/components/expression_language.html>`__
is not specific to TYPO3.

It can be used since TYPO3 9 LTS for TypoScript conditions.

More information:
   * `Feature #85829 - Implement symfony expression language for TypoScript conditions
     <https://docs.typo3.org/typo3cms/extensions/core/Changelog/9.4/Feature-85829-ImplementSymfonyExpressionLanguageForTypoScriptConditions.html>`__
     in Changelog
   * `use TYPO3 Blog (Daniel Goerz) <https://usetypo3.com/symfony-expression-language-in-typo3.html>`__
   * `What's new in TYPO3 v9 LTS <https://forge.typo3.org/attachments/download/33792/TYPO3-v9-LTS-whats-new.english.pdf>`__
