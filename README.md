# W4M PHP Standards

This is the W4M PHP Standards customized PHP standards based on the PSR-2 PHP Standard.

It is for W4M Internal use only!

## TO COVER

- Multiple blank lines - one line at most

## Usage

Check with PHP_CodeSniffer against this standard

Add the W4M PHP Standards to your PHP project using composer

**1.** Install this standard

w4msolutions/php-standard will install [PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer) as a dependency (squizlabs/php_codesniffer)

```bash
composer require --dev w4msolutions/php-standard
```

After install, `composer.json` should look like:

```json
{
    "name": "w4msolutions/MyProject",
    "version": "1.0",
    "description": "MyProject Description",
    "keywords": ["MyProject", "framework", "xxxxx", "xxxxxxxx"],
    "homepage": "https://w4msolutions.com/",
    "type": "project",
    "license": "proprietary",
    "minimum-stability": "stable",
    "require": {
    },
    "require-dev": {
        "w4msolutions/php-standard": "*"
    }
}
```

**2.** Add `phpcs.xml` file to the root of the project

`phpcs.xml` will be used to specify which standard to use with PHP_CodeSniffer, adjust some sniffs and adapt to current project.

You can find `vendor/w4msolutions/php-standard/phpcs-dist-project.xml` inside the `w4msolutions/php-standards` package that can be used as a base when creating `phpcs.xml` for your project.

**3.** Check code

From the root of your project execute PHP_CodeSniffer (phpcs)

php_codesniffer should be installed for your project (not global) so you have to use full path to executable

```bash
# Check a file
./vendor/squizlabs/php_codesniffer/bin/phpcs --standard=./phpcs.xml myFile.php

# Check a folder
./vendor/squizlabs/php_codesniffer/bin/phpcs --standard=./phpcs.xml path/to/folder/

# Check whole project
./vendor/squizlabs/php_codesniffer/bin/phpcs --standard=./phpcs.xml .
```

Example output:

```bash
./vendor/squizlabs/php_codesniffer/bin/phpcs --standard=phpcs.xml /app/api/index.php

E 1 / 1 (100%)

FILE: api/index.php
--------------------------------------------------------------------------------------------------
FOUND 2 ERRORS AND 1 WARNING AFFECTING 3 LINES
--------------------------------------------------------------------------------------------------
  1 | WARNING | [ ] A file should declare new symbols (classes, functions, constants, etc.) and
    |         |     cause no other side effects, or it should execute logic with side effects,
    |         |     but should not do both. The first symbol is defined on line 9 and the first
    |         |     side effect is on line 4. (PSR1.Files.SideEffects.FoundWithSymbols)
  9 | ERROR   | [x] No space found after comma in function call
    |         |     (Generic.Functions.FunctionCallArgumentSpacing.NoSpaceAfterComma)
 11 | ERROR   | [x] No space found after comma in function call
    |         |     (Generic.Functions.FunctionCallArgumentSpacing.NoSpaceAfterComma)
--------------------------------------------------------------------------------------------------
PHPCBF CAN FIX THE 2 MARKED SNIFF VIOLATIONS AUTOMATICALLY
--------------------------------------------------------------------------------------------------

Time: 480ms; Memory: 5.25Mb
```

> Correcting marked errors should be safe but **ALWAYS CHECK THE FILES** after automatic fixing.

Correct the files manually or automatically and execute again.    
There should be **NO ERRORS** and the LEAST AMOUNT OF WARNINGS as possible.

**4.** (EXPERIMENTAL AND OPTIONAL) Automatically correct the code

From the root of your project execute PHP Code Beautifier and Fixer (`phpcbf`)

PHP Code Beautifier and Fixer (`phpcbf`) will fix ~some errors~ - It will not fix warnings

```bash
# Check a file
./vendor/squizlabs/php_codesniffer/bin/phpcbf --standard=./phpcs.xml myFile.php

# Check a folder
./vendor/squizlabs/php_codesniffer/bin/phpcbf --standard=./phpcs.xml path/to/folder/

# Check whole project
./vendor/squizlabs/php_codesniffer/bin/phpcbf --standard=./phpcs.xml .
```

Example output:

```bash
./vendor/squizlabs/php_codesniffer/bin/phpcbf --standard=phpcs.xml /app/api/index.php

F 1 / 1 (100%)

PHPCBF RESULT SUMMARY
----------------------------------------------------------------------
FILE                                                  FIXED  REMAINING
----------------------------------------------------------------------
api/index.php                                         2      1
----------------------------------------------------------------------
A TOTAL OF 2 ERRORS WERE FIXED IN 1 FILE
----------------------------------------------------------------------

Time: 538ms; Memory: 5.5Mb
```

Running php_codesniffer again will show any existing errors and warnings.

**Repeat process until there are no errors or warnings.**

Example output:

```bash
./vendor/squizlabs/php_codesniffer/bin/phpcs --standard=phpcs.xml /app/api/index.php

W 1 / 1 (100%)

FILE: api/index.php
-------------------------------------------------------------------------------------
FOUND 0 ERRORS AND 1 WARNING AFFECTING 1 LINE
-------------------------------------------------------------------------------------
 1 | WARNING | A file should declare new symbols (classes, functions, constants,
   |         | etc.) and cause no other side effects, or it should execute logic
   |         | with side effects, but should not do both. The first symbol is
   |         | defined on line 9 and the first side effect is on line 4.
   |         | (PSR1.Files.SideEffects.FoundWithSymbols)
-------------------------------------------------------------------------------------

Time: 518ms; Memory: 5.25Mb
```
