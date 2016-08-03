Buffer PHP Coding Style Guide (in progress)
==================
Our PHP coding guide very much derived from [PSR-2](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md). We follow PSR-2 coding standard.

The goal of this guide is to make our code more consistent and improve code readability.

1. Overview and Important Points
-----------
- Code MUST use 4 spaces for indenting, not tabs.

- Opening braces for classes/methods MUST go on the next line, and closing braces MUST
  go on the next line after the body.

- New controllers and models are also CamelCase. E.g. `InteractionsController.php`.

- Camel case for classes and methods. E.g. `class SampleClassName` and `public function getTeamMembers()`

- Camel case for all instance, global and local variables, properties defined within the class or file.

- Exceptions are json endpoints. Use *underscore* pattern for naming json endpoint methods.
    - This is a way to keep our api urls consistent with industry standards and also a way to differentiate endpoints from regular methods. e.g. `GET profiles/{id}/influencers/engagements.json` routes to `public function influencers_engagements() {}` method.
  

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

## Table of Contents

*TODO*

##Naming Conventions

*TODO*

## Indenting and Line Length
Use an indent of one tabs character. This helps to avoid problems with diffs, patches, git history and annotations.
Try to keep line within 75-85 characters long for better code readability.
Use vertical space instead of horizontal space.

## Control Structures
These include ``if``, ``for``, ``while``, ``switch``, etc.
Here is an example if statement, since it is the most complicated of them:

```php
<?php
if ((condition1) || (condition2))
{
    action1;
}
elseif ((condition3) && (condition4))
{
    action2;
}
else
{
    defaultaction;
}
?>
```
Control statements should have one space between the control keyword and opening parenthesis, to distinguish them from function calls. Curly braces should be used on new lines.
You are strongly encouraged to always use curly braces even in situations where they are technically optional. Having them increases readability and decreases the likelihood of logic errors being introduced when new lines are added.
For switch statements:
```php
<?php
switch (condition)
{
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
The closing parenthesis and opening brace get their own line at the end of the conditions.

Keeping the operators at the beginning of the line has two advantages:
It is trivial to comment out a particular line during development while keeping
syntactically correct code (except of course the first line).
Further is the logic kept at the front where it's not forgotten.
Scanning such conditions is very easy since they are aligned below each other.

```php
<?php

if (($condition1
    || $condition2)
    && $condition3
    && $condition4
)
{
    //code here
}
?>
```

The first condition may be aligned to the others.
```php
<?php

if (   $condition1
    || $condition2
    || $condition3
)
{
    //code here
}
?>
```

The best case is of course when the line does not need to be split.
When the ``if`` clause is really long enough to be split, it might be better to
simplify it. In such cases, you could express conditions as variables and
compare them in the ``if()`` condition. This has the benefit of "naming" and
splitting the condition sets into smaller, better understandable chunks:

```php
<?php

$is_foo = ($condition1 || $condition2);
$is_bar = ($condition3 && $condtion4);
if ($is_foo && $is_bar)
{
    // ....
}
?>

```

In order to maximize the **bias towards clarity** value, it's encouraged to keep those conditional expressions that depend on multiple conditions (being *multiple* more than one) on a boolean method. 

So, something like this:

```php
<?php
    if ($date->before(self::SUMMER_START) || $date->before(self::SUMMER_END))
    {
        $charge = $quantity * $this->winterRate + $this->winterServiceCharge;
    }
    else
    {
        $charge = $quantity * $this->summerRate;
    }
?>
```

Can be converted into:

```php
<?php
    if ($this->notSummer($date))
    {
        $charge = $this->winterRate($quantity);
    }
    else
    {
        $charge = $this->summerRate($quantity);
    }
?>
```
Of course, the multiline formatting proposed before would apply too in the extracted method:

```php
<?php
    private function notSummer($date) {
        return $date->before(self::SUMMER_START)
            || $date->before(self::SUMMER_END)
        ;
    }
?>
```

Another way to make conditionals even clearer are by avoiding the **if not / else** form into a *positive* if conditional. The example code, by applying that, would be:

```php
<?php
    if($this->isSummer($date))
    {
        $charge = $this->summerRate($quantity);
    }
    else
    {
        $charge = $this->winterRate($quantity);
    }
?>
```

##Ternary operators
The same rule as for if clauses also applies for the ternary operator:
 It may be split onto several lines, keeping the question mark and the colon at
 the front.
```php
<?php

$a = $condition1 && $condition2
    ? $foo : $bar;

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
$var = foo($bar, $baz, $quux);
?>
```
As displayed above, there should be one space on either side of an equals sign used to assign the return value of a function to a variable. In the case of a block of related assignments, more space may be inserted to promote readability:

```php
<?php
$short         = foo($bar);
$long_variable = foo($baz);
?>
```
To support readability, parameters in subsequent calls to the same function/method may be aligned by parameter name:

```php
<?php

$this->callSomeFunction('param1',     'second',        true);
$this->callSomeFunction('parameter2', 'third',         false);
$this->callSomeFunction('3',          'verrrrrrylong', true);
?>
```
Split function call on several lines
The CS require lines to have a maximum length of 80 chars. Calling functions or methods with many parameters while adhering to CS is impossible in that cases. It is allowed to split parameters in function calls onto several lines.

```php
<?php

$this->someObject->subObject->callThisFunctionWithALongName(
    $parameterOne, $parameterTwo,
    $aVeryLongParameterThree
);
?>
```

Several parameters per line are allowed. Parameters need to be indented 4 spaces compared to the level of the function call. The opening parenthesis is to be put at the end of the function call line, the closing parenthesis gets its own line at the end of the parameters. This shows a visual end to the parameter indentations and follows the opening/closing brace rules for functions and conditionals.

The same applies not only for parameter variables, but also for nested function calls and for arrays.

```php
<?php

$this->someObject->subObject->callThisFunctionWithALongName(
    $this->someOtherFunc(
        $this->someEvenOtherFunc(
            'Help me!',
            array(
                'foo'  => 'bar',
                'spam' => 'eggs',
            ),
            23
        ),
        $this->someEvenOtherFunc()
    ),
    $this->wowowowowow(12)
);
?>
```

Nesting those function parameters is allowed if it helps to make the code more readable, not only when it is necessary when the characters per line limit is reached.

Using fluent application programming interfaces often leads to many concatenated function calls. Those calls may be split onto several lines. When doing this, all subsequent lines are indented by 4 spaces and begin with the "->" arrow.

```php
<?php

$someObject->someFunction("some", "parameter")
    ->someOtherFunc(23, 42)
    ->andAThirdFunction();
?>
```

## Alignment of assignments
To support readability, the equal signs may be aligned in block-related assignments:

```php
<?php

$short  = foo($bar);
$longer = foo($baz);
?>
```

The rule can be broken when the length of the variable name is at least 8 characters longer/shorter than the previous one:

```php
<?php

$short = foo($bar);
$thisVariableNameIsVeeeeeeeeeeryLong = foo($baz);
?>
```

##Split long assigments onto several lines
Assigments may be split onto several lines when the character/line limit would be exceeded. The equal sign has to be positioned onto the following line, and indented by 4 characters.

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
class Foo_Bar
{

    //... code goes here

}
?>
```
