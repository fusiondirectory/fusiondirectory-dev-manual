\\FusionDirectory\\Cli
======================

This library provides a base class to build cli tools that support various options and arguments.

Requirements
------------

This library needs PHP 7.3 or newer.

Installation
------------

You must put the src/FusionDirectory folder in the include_path of your PHP configuration.

Example
-------

.. code-block:: php

    #!/bin/php
    <?php
      require 'FusionDirectory/Cli/autoload.php';
    
      use \FusionDirectory\Cli;
    
      class MyTool extends Cli\Application
      {
        public function __construct ()
        {
          parent::__construct();
    
          $this->options  = [
            'list-fruits'    => [
              'help'        => 'List supported fruits',
              'command'     => 'listFruits',
              'short'       => 'l',
            ],
            'show-color:'  => [
              'help'        => 'Show color of a fruit',
              'command'     => 'showColor',
            ],
            'help'          => [
              'help'        => 'Show this help',
              'short'       => 'h',
            ],
          ];
    
          $this->args = [
            'header'  => [
              'help'    => 'Header to show at beginning',
              'handler' => 'strtoupper',
            ],
          ];
        }
    
        public function run (array $argv): void
        {
          parent::run($argv);
    
          echo $this->args['header']['value']."\n";
    
          $this->runCommands();
        }
    
        protected function listFruits (): void
        {
          echo "Banana\nStrawberry\n";
        }
    
        protected function showColor (array $fruits): void
        {
          foreach ($fruits as $fruit) {
            switch ($fruit) {
              case 'Banana':
                echo 'Yellow';
                break;
              case 'Strawberry':
                echo 'Red';
                break;
              default:
                echo 'Unsupported fruit "'.$fruit.'". See --list-fruits';
                break;
            }
            echo "\n";
          }
        }
      }
    
      $tool = new MyTool();
    
      $tool->run($argv);


Example usage of this tool
--------------------------

.. code-block:: sh

    $ mytool -h
    Usage: mytool --list-fruits --show-color VALUE --help HEADER
    
            --list-fruits, -l               List supported fruits
            --show-color:                   Show color of a fruit
            --help, -h                      Show this help
            HEADER                   :      Header to show at beginning
    $ mytool --list-fruits Fruits:
    FRUITS:
    Banana
    Strawberry
    $ mytool --show-color Banana --show-color Strawberry Colors:
    COLORS:
    Yellow
    Red
    $ mytool -l fruits
    FRUITS
    Banana
    Strawberry
    $ mytool --what
    Unrecognized option --what
    Usage: mytool --list-fruits --show-color VALUE --help HEADER
    
            --list-fruits, -l               List supported fruits
            --show-color:                   Show color of a fruit
            --help, -h                      Show this help
            HEADER                   :      Header to show at beginning

