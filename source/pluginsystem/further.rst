Going further with Simple Plugin
================================
Here, we'll see what Simple Plugin functions you can inherit in order to adjust the behavior of your plugin.

Because sometimes, you don't just want to edit LDAP fields.

simplePlugin special attributes
-------------------------------

There are some attributes that you can set in your class or in your constructor that will allow you to do more things:

* Set **displayHeader** to TRUE if you need this tab to be deactivable.
* Set **preInitAttributes** to an array of attributes names to be sure they'll be initialized before the others (it's used by workstationGeneric for the network attribute)

custom template
^^^^^^^^^^^^^^^
By default simplePlugin does a template for you, but if you want to add some elements to the template, or just render the sections in a different order, or that kind of things, here's what to do:
Change **templatePath** value to your custom template path (usually in the constructor, using get_template_path).

In your template, you'll be able to use the **$sections** array that contains each section render.
For instance:

.. code-block:: smarty

    <h1>Hello world!</h1>
    <div class="plugin_sections">
        {$sections.section1}
        {$sections.Mysection}
    </div>

    <input name="{$hiddenPostedInput}" value="1" type="hidden"/>

    <!-- Place cursor -->
    <script language="JavaScript" type="text/javascript">
      <!-- // First input field on page
        focus_field('{$focusedField}');
      -->
    </script>

You need to add the **hidden** input at the end in order for the POST analysis to work.
The script is needed if you want the auto-focusing of first field to work.

simplePlugin attributes values and methods
------------------------------------------

In all of these methods, you can access the attributes by using **$this->attributesAccess** as follows:
    $this->attributesAccess['attributeldapname']

Don't forget to look at the documentation of the Attribute classes to know who to use them.
For instance they offer a **setDisabled** method if you need to disable some of them, **hasChanged**
will allow you to know if an attribute has been modified, etc…
You can also easily access their value using **$this->attributeldapname**. Be aware that
this is not a real class attribute, accessing it will call the **getValue** and **setValue** methods of the attribute.
That means you can't create reference to it or call method that needs references like the array ones (array_push, …).
The [] operator for arrays do not work either.

execute
^^^^^^^

This method is the one that render the plugin.
You can change it, doing something that look like that:

.. code-block:: php

  <?php
  function execute ()
  {
    $smarty = get_smarty();
    parent::execute();
    // your code goes here
    if ($this->displayPlugin) {
      return $this->header.$smarty->fetch($this->templatePath);
    } else {
      return $this->header;
    }
  }

You can fetch any template but usually **$this->templatePath** is used, just remember to add **$this->header** at the beginning if you activated the display header feature.

Please avoid doing heavy things in the execute function as it is just the render function, it's not supposed to compute anything.

save_object
^^^^^^^^^^^

This function analyse the POST informations.
You can inherit it as follows:

.. code-block:: php

  <?php
  function save_object ()
  {
    parent::save_object();
    if (isset($_POST[get_class($this)."_posted"])) {
      // your code goes here
    }
  }

ldap_save
^^^^^^^^^

This function saves the informations into the LDAP.
You can inherit it and do some additionnal LDAP modifications when saving:

.. code-block:: php

  <?php
  protected function ldap_save (): array
  {
    $errors = parent::ldap_save();

    if (!empty($errors)) {
      return $errors;
    }

    // your code goes here

    return $errors;
  }

prepare_save
^^^^^^^^^^^^

**prepare_save** will fill the attribute **$this->attrs**, which is an array of what will be written into the LDAP.
Your code should modify **$this->attrs** as ldap_save will write it into the LDAP.

.. code-block:: php

  <?php
  protected function prepare_save (): array
  {
    $errors = parent::prepare_save();

    if (!empty($errors)) {
      return $errors;
    }

    // your code goes here

    return $errors;
  }

__construct
^^^^^^^^^^^

Of course, there is always the possibility to have your own constructor, just remember to call the parent one.
The simple plugin constructor have a 5th optional parameter which is the attributes information. If you don't give it, the **getAttributesInfo** static function will be used.
So you can do the following:

.. code-block:: php

  <?php
  function __construct (string $dn = NULL, $object = NULL, $parent = NULL, bool $mainTab = FALSE)
  {
    $attributesInfo = self::getAttributesInfo();
    // some modifications on $attributesInfo
    parent::__construct($dn, $object, $parent, $mainTab, $attributesInfo);
  }

An other method, often simpler, is to modify your attributes after being constructed. You can't do that for all modifications but for common cases like SelectAttribute choices modification, it's what you should do:

.. code-block:: php

  <?php
  function __construct (string $dn = NULL, $object = NULL, $parent = NULL, bool $mainTab = FALSE, array $attributesInfo = NULL)
  {
    parent::__construct($dn, $object, $parent, $mainTab, $attributesInfo);

    $array = ['node1','node2']; // some dummy array
    // After simplePlugin constructor, you must access attributes by their ldap name
    $this->attributesAccess['myattributeLdapName']->setChoices($array);
  }

is_this_account
^^^^^^^^^^^^^^^

This method is used to check if an object has your plugin tab activated or not.
By default it will just return TRUE if the objectClasses of your tab are present and FALSE otherwise, it is usually correct. If you need an other behaviour, you will have to override it.

  function is_this_account ($attrs)

Even if the method is not static, it’s not supposed to use the object attributes and should only use the information in the attrs parameter to tell if the LDAP node has this tab activated or not.

Section templates
-----------------

We've seen that you can use a specific template for your plugin instead of the default one, and that sections are pre-rendered in a sections array.
Here, we'll see how to use a specific template for a section, in order to modify its organization.
It's quite easy to do, all you have to do is adding a 'template' key to the section array in getAttributesInfo:

.. code-block:: php

      'my_section' => [
        'name'  => _('Great Section'),
        'attrs' => [
          new StringAttribute (_('Something'), _('This attribute does nothing'), 'someThing', FALSE, 'DefaultValue'),
          // other attributes…
        ],
        'template' => get_template_path('my_section_template.tpl', TRUE, dirname(__FILE__))
      ],

You need to use get_template_path as above in order to get an absolute path for the tpl file.
In this template file, you need to copy simpleplugin_section.tpl, the default template.
Please don't touch the fieldset, legend and table, just replace the foreach by what you want.
You need to use the attributes array, which contain for each attribute, indexed by its ldap name, its label and its input html code.
For instance, for the above section, doing the following would have the same result than the default template:

.. code-block:: smarty

    <fieldset id="{$sectionId}" class="plugin_section{$sectionClasses}">
      <legend>{$section}</legend>
      <table>
        <tr>
          <td title="{$attributes.someThing.description}"><label for="someThing">{eval var=$attributes.someThing.label}</label></td>
          <td>{eval var=$attributes.someThing.input}</td>
        </tr>
      </table>
    </fieldset>

You need to use 'eval' for label and HTML input as it contains some smarty code too (for ACL check for instance).

Managed attributes
------------------

In some case you want some attributes to be enabled/disabled depending on a checkbox or select state.
For this, you can use the **setManagedAttributes** method as follow:

.. code-block:: php

    $this->attributesAccess['boolean']->setManagedAttributes(
      [
        'disable' => [
          FALSE => [
            'attribute1',
            'attribute2',
          ]
        ]
      ]
    );

'disable' means that the attributes will be disabled but still saved into the LDAP.
you can use 'erase' instead if you want those to be remove from the LDAP.
FALSE means that when the value is FALSE, they'll be disabled.
You can also use this method with selectattributes:

.. code-block:: php

    $this->attributesAccess['select']->setManagedAttributes(
      [
        'multiplevalues' => ['darkcolors' => ['blue','black']],
        'erase' => [
          'darkcolors' => [
            'attribute1',
            'attribute2',
          ],
          'yellow' => [
            'attribute3',
            'attribute4',
          ],
        ]
      ]
    );

Note the **multiplevalues** special key in order to specify several values that disable the same attributes.
