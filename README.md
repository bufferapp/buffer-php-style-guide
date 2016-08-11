Buffer PHP Coding Style Guide
==================
Our PHP coding guide very much derived from [PSR-2](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md). We follow PSR-2 coding standard.

The goal of this guide is to make our code more consistent and improve code readability.

1. Overview and Important Points
-----------
- Code MUST use 4 spaces for indenting, not tabs.

- Opening braces for classes/methods MUST go to the next line, and closing braces MUST
  go on the next line after the body.

- New controllers and models are also CamelCase. E.g. `InteractionsController.php`.

- Camel case for classes and methods. E.g. `class SampleClassName` and `public function getTeamMembers()`

- Camel case for all instance, global and local variables, properties defined within the class or file.

I think keeping all the foundational rules above is a great start to keep our code consistent. **Those were the points we all should remember.**

### 1.1. Example

Here is an example snippet that illustrates the main points above.

```php
<?php
namespace Vendor\Package;

use FooInterface;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class Foo extends Bar implements FooInterface
{
    public function sampleFunction($a, $b = null)
    {
        if ($a === $b) {
            bar();
        } elseif ($a > $b) {
            $foo->bar($arg1);
        } else {
            BazClass::bar($arg2, $arg3);
        }
    }

    final public static function bar()
    {
        // method body
    }
}
```
## Goal

To establish more consistency and readability across the Buffer team and our
open source projects.

## Ideals

> **Have a bias toward clarity** - from [The Buffer Values](http://www.slideshare.net/Bufferapp/buffer-culture-04)

  - We should always aim to write code that is clear and readable.
  - Use whitespace. Add comments liberally where needed, but strive to write code that's clear and self documenting
  - Always try to write code that clearly demonstrates and communicates it's intent.
  - If you write a very long comment for your code it means that something is possible off with the code. Long comments may add noise sometimes.


## Indenting and Line Length
- Use an indent of one tabs character. This helps to avoid problems with diffs, patches, git history and annotations.
- Try to keep line within 75-85 characters long for better code readability.
- PSR-2 requires that the line be less than 120 characters.

## Control Structures
These include ``if``, ``for``, ``while``, ``switch``, etc.
Here is an example if statement, since it is the most complicated of them:

```php
<?php
if (condition1 || (condition2) {
    action1;
}
elseif (condition3 && condition4) {
    action2;
} else {
    defaultaction;
}
?>
```
Control statements should have one space between the control keyword and opening parenthesis, to distinguish them from function calls. Curly braces should be used on new lines.
You are strongly encouraged to always use curly braces even in situations where they are technically optional. Having them increases readability and decreases the likelihood of logic errors being introduced when new lines are added.
For switch statements:

```php
<?php
switch (condition) {
  case 1:
      action1;
      break;

  case 2:
      action2;
      break;

  default:
      defaultaction;
      break;
}
?>
```

Split long if statements onto several lines.
Long ``if`` statements may be split onto several lines when the character/line limit
would be exceeded. The conditions have to be positioned onto the following line,
and indented. The logical operators (``&&``, ``||``, etc.) should be at the
beginning of the line to make it easier to comment (and exclude) the condition.
The closing parenthesis gets its own line at the end of the conditions.



##Ternary operators
The same rule as for if clauses also applies for the ternary operator:
 It may be split onto several lines, keeping the question mark and the colon at
 the front.
 
```php
<?php

$a = $condition1 && $condition2 ? $foo : $bar;

$b = $condition3 && $condition4
    ? $foo_man_this_is_too_long_what_should_i_do
    : $bar;
?>
```

## Function Calls
Functions should be called with no spaces between the function name, the opening
parenthesis, and the first parameter; spaces between commas and each parameter,
and no space between the last parameter, the closing parenthesis, and the semicolon.
Here's an example:

```php
<?php
	$apples = getApplesByColor($tree, $color);
?>
```
As displayed above, there should be one space on either side of an equals sign used to assign the return value of a function to a variable.

If the function has many arguments and it violates 120 chars rule, you can do something like this and move the arguments to the next line.

```php
<?php

$this->someObject->callThisFunctionWithManyArgs($parameterOne,
	$parameterTwo, $aVeryLongParameterThree);
?>
```

Several parameters per line are allowed. Parameters need to be indented 4 spaces compared to the level of the function call. The opening and closing parentheses are to be put at the end of the function call line.



##Split long assigments onto several lines
Assigments may be split onto several lines when the character/line limit would be exceeded. The equal sign has to be positioned onto the following line, and indented by 4 spaces.

```php
<?php
$GLOBALS['TSFE']->additionalHeaderData[$this->strApplicationName]
    = $this->xajax->getJavascript(t3lib_extMgm::siteRelPath('nr_xajax'));
?>
```



##Class Definitions
Class declarations have their opening brace on a new line:

```php
<?php
class FooBar {

    //... code goes here

}
?>
```
