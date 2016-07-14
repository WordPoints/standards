# PHP Coding Standards

This document outlines the PHP coding standards used by the WordPoints projects.

It is recommended that you understand the [WordPress PHP coding
standards](http://make.wordpress.org/core/handbook/coding-standards/php/), as
WordPoints follows these except as noted below.

## End Of File Comments

Every PHP file MUST end in a comment like this:

```php
// EOF
```

The comment MUST have an empty newline above and below it. It MUST be exactly of the
form above, with no ending period.

There is one exception to this rule: if the file ends in HTML mode (i.e., the last
PHP tag was closed and was followed by HTML/text), it SHOULD NOT enter PHP mode so 
that the EOF comment can be supplied.

## Backticks in SQL

Backticks MUST be used around all [identifiers](https://dev.mysql.com/doc/refman/5.1/en/identifiers.html) 
in SQL statements.

```mysql
SELECT `ID` FROM `wp_posts`
```

This makes the meaning unambigous to the parser and to humans too. And while you 
SHOULD NOT use [reserved words](https://dev.mysql.com/doc/mysqld-version-reference/en/mysqld-version-reference-reservedwords-5-5.html) 
as identifiers, by using backticks you are safe if your column names ever become 
reserved words in the future.

## Global Variables

Your code MUST NOT declare new `global` variables. If you are thinking of introducing
a new global, refactor your code instead.

### Using Global Variables

Of course, WordPress uses some global variables, like `$wpdb`, and it's fine for you
to _use_ globals provided by WordPress/other plugins/etc. when necessary. Just don't 
create any new ones.

When using a global variable, you MUST declare it `global` in the current
scope, even if you think that you are currently in the global scope. For example,
if you use `$wpdb` in a file's main scope, you MUST add this at the top of the file
(or anywhere before using the variable):

```php
global $wpdb;
```

## Property Access via Magic Methods

Your code SHOULD NOT use the following magic methods to grant "public" access to protected or private class properties: `__get()`, `__set()`, `__isset()`, `__unset()`.

These methods [increase memory consumption](https://gist.github.com/nikic/5015323) for your object, and add the overhead of a method call without making this obvious to the developer. Think of these as "deceptive", rather than "magic", methods. They can easily trick the developer into thinking that it is OK to do this:

```php
$obj->magic->method();
$obj->magic->another_method();
```

In reality, the above code is calling `__get()` twice, to retreive the magic property each time. If this property wasn't magic, the overhead of accessing it twice woudl be negligable. Because accessing it is actually a method call under the hood, what is really happening is this:

```php
$obj->magic()->method();
$obj->magic()->another_method();
```

Which obviously needs to be refactored to this:

```php
$magic = $obj->magic();
$magic->method();
$magic->another_method();
```

But this isn't obvious to the developer when this behaviour is being hidden behind the magic of the `__get()` method.

These methods can also have other limitations that can lead to unexpected issues in certain cituations. For example, it is not possible to call them recursively.

The only places in your code where you should use these methods is where it is absolutely necessary for compatibility (either with older code or a library that is outside of your control).

## Slashing

Functions and methods MUST NOT expect data passed to them to be slashed ("magic quoted"). This tends to bubble up to higher-level functions, where the behavior is likely to be undocumented and unexpected, since it is hidden behind the function used by the function used by the function. *Nightmares*. You get the idea.
