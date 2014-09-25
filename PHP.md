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
