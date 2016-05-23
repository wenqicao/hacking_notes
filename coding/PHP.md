# PHP

Switch
------
```
$favcolor = "red";

switch ($favcolor) {
    case "red":
        echo "Your favorite color is red!";
        break;
    case "blue":
        echo "Your favorite color is blue!";
        break;
    case "green":
        echo "Your favorite color is green!";
        break;
    default:
        echo "Your favorite color is neither red, blue, nor green!";
}
```

Arrays
------

Arrays in PHP are zero-based (counting starts from 0).  
```
$myArray = array(1, 2, 3);
```

An associative array makes use of (key => value) pairs. An associative array is also called a map.
```
$myAssocArray = array('year' => 2012,
                        'colour' => 'blue',
                        'doors' => 5,
                        'make' => 'BMW');
```

Multidimensional arrays - arrays stored in arrays.
```
<?php
        $deck = array(array('2 of Diamonds', 2),
                      array('5 of Diamonds', 5),
                      array('7 of Diamonds', 7));

      // Imagine the first chosen card was the 7 of Diamonds.
      // This is how we would show the user what they have:
      echo 'You have the ' . $deck[2][0] . '!';
      ?>
```

Iterating through associative arrays:
```
<p>
     <?php
     // On the line below, create your own associative array:
       $myArray = array("sun" => "good", "rain" => "bad");


     // On the line below, output one of the values to the page:


     // On the line below, loop through the array and output
     // *all* of the values to the page:
    echo $myArray["sun"];
    // Loop through an associative array using "foreach":
     foreach ($myArray as $weather=>$isgood) {
       echo 'Today we have ' . $weather . '. Thats ' . $isgood . '.';
     }
     ?>
```

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

Inheritance
-----------
```
<?php
        class Shape {
          public $hasSides = true;
        }

        class Square extends Shape {

        }

        $square = new Square();
        // Add your code below!
        if (property_exists($square, "hasSides")) {
          echo "I have sides!";
        }
      ?>
```

Static Keywords
---------------
```
class Person {
  public static $isAlive = "Yep!"
  public static function greet() {
    echo "Hello there!";
  }
}

echo Person::$isAlive;
// prints "Yep!"
Person::greet();
// prints "Hello there!"
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
