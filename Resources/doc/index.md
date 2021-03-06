Documentation
=============

## Installation

Run from terminal:

```bash
$ composer require pugx/shortid-doctrine-bundle
```

Enable bundle in the kernel:

```php
<?php
// app/AppKernel.php
public function registerBundles()
{
    $bundles = array(
        // ...
        new PUGX\ShortidDoctrineBundle\PUGXShortidDoctrineBundle(),
    );
}
```

## Usage

You can use the ``shortid`` type in your entity.
Example:

```php
<?php

namespace AppBundle\Entity;

use Doctrine\ORM\Mapping as ORM;

/**
 * @ORM\Entity()
 * @ORM\Table()
 */
class Book
{
    /**
     * @var string
     *
     * @ORM\Column(type="shortid")
     * @ORM\Id
     * @ORM\GeneratedValue(strategy="CUSTOM")
     * @ORM\CustomIdGenerator(class="PUGX\ShortidDoctrineBundle\Generator\ShortidGenerator")
     */
    protected $id;
}
```

## Optional configuration

If you want to globally configure Shortid, you can set a configuration like in this example:

```yaml
pugx_shortid_doctrine:
    global_config:
        length: 6
        alphabet: "é123456789àbcdefghìjklmnòpqrstùvwxyzABCDEFGHIJKLMNOPQRSTUVWX.!@|"
```

The ``length`` option must be between 2 and 20 (default is 7), while ``alphabet`` must be 64 characters long.

Be aware: if you change ``length`` in this way, you **must** specify ``length`` option in every column definition.
