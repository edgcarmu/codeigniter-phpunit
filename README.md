<div align="center">
    <a href="https://codeigniter.com/" target="_blank">
        <img src="https://codeigniter.com/assets/icons/ci-logo.png" height="100px">
    </a>
    <h1 align="center">CodeIgniter PHPUnit Test</h1>
    <br>
</div>

CodeIgniter 3 PHPUnit Test extension library

[![Latest Stable Version](https://poser.pugx.org/edgcarmu/codeigniter-phpunit/v/stable?format=flat-square)](https://packagist.org/packages/edgcarmu/codeigniter-phpunit)
[![License](https://poser.pugx.org/edgcarmu/codeigniter-phpunit/license?format=flat-square)](https://packagist.org/packages/edgcarmu/codeigniter-phpunit)

Official adaptation of the [yidas/codeigniter-phpunit](https://github.com/yidas/codeigniter-phpunit) repository for compatibility with **CodeIgniter 3.1.13** and **PHP 7.1+**.

FEATURES
--------

- ***PHPUnit Test** in **Codeigniter 3** Framework*

- *Easy to install into your Codeigniter project by Composer*

---

OUTLINE
-------

- [Requirements](#requirements)
- [Installation](#installation)
- [Directory Structure](#directory-structure)
- [Configuration](#configuration)
- [Usage](#usage)
- [Test Case](#test-case)


REQUIREMENTS
------------

This library requires the following:

- PHP 7.1.0+
- CodeIgniter 3.1.13+

---

INSTALLATION
------------

Run Composer from the project root:

    composer require edgcarmu/codeigniter-phpunit

---

DIRECTORY STRUCTURE
-------------------

```
codeigniter/
├── application/
├── system/
├── tests/
│   ├── bootstrap.php        ← Initializes the test environment; create only if needed to customize, then delegate to vendor/edgcarmu/codeigniter-phpunit/bootstrap.php
│   └── MyTest.php           ← Your test cases go here
├── vendor/
└── phpunit.xml              ← PHPUnit configuration; can point directly to the library's bootstrap if no customization is needed
```

---

CONFIGURATION
-------------

According to [Directory Structure](#directory-structure), create and configure `phpunit.xml` in the project root:

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<phpunit bootstrap="vendor/edgcarmu/codeigniter-phpunit/bootstrap.php">
  <testsuites>
    <testsuite name="TestSuite">
      <directory>tests</directory>
    </testsuite>
  </testsuites>
</phpunit>
```

For this phpunit.xml template, the test cases directory is tests/, located at the project root.
Make sure to place all your test cases inside this directory.

---

USAGE
-----

From the project root, run PHPUnit using the Composer-installed binary:

```
./vendor/bin/phpunit
```

Or using absolute path commands like:

```
$ /var/www/html/codeigniter3/vendor/bin/phpunit -c /var/www/html/codeigniter3/phpunit.xml
$ phpunit -c /var/www/html/codeigniter3/phpunit.xml
```

Then the result would like:

```ps
PHPUnit 5.7.27 by Sebastian Bergmann and contributors.



Time: 40 ms, Memory: 2.75MB

No tests executed!
```

---

TEST CASE
---------

With this extension library, you can write test cases while loading the CodeIgniter framework.

For example, create a test case at tests/CodeigniterTest.php to test a CodeIgniter component like the config loader:
```php
<?php

use PHPUnit\Framework\TestCase;

final class CodeigniterTest extends TestCase
{
    function __construct() 
    {
        parent::__construct();
        // Load CI application
        $this->CI = & get_instance();
    }
    
    public function testConfigItem()
    {
        $indexPage = $this->CI->config->item('index_page');
        
        $this->assertSame('index.php', $indexPage);
    }
}
```

Then you would get the result `OK (1 test, 1 assertion)` by running PHPUnit test.
