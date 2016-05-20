# PHP

Hello World
-----------
```php
<?php echo "Hello World!"; ?>
```

Arrays
------

Counting starts from 0.

Objects, Classes, Constructors
------------------------------

A method is a function bundled into object.

```
<?php
        class Person {
            public function __construct($firstname, $lastname, $age) {
                $this->firstname = $firstname;
                $this->lastname = $lastname;
                $this->age = $age;
            }
            public $isAlive = true;

            public function greet() {
                return "Hello, my name is " . $this->firstname . " " . $this->lastname . "                         . Nice to meet you! :-)";
            }
        }

        $teacher = new Person("boring", "12345", 12345);
        $student = new Person("what", "the", 177);

        echo $student->age;
        echo $teacher -> greet();
        echo $student -> greet();
        ?>
  ```


Syntax
------

* `<<<` - [heredoc](http://www.php.net/manual/en/language.types.string.php#language.types.string.syntax.heredoc) syntax. Example:
```
$sql = <<<MySQL_QUERY
SELECT *
FROM TAB
WHERE A = 1 AND B = 2
MySQL_QUERY;   
```
