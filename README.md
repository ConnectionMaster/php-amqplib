# php-amqplib #

[![Build Status](https://secure.travis-ci.org/videlalvaro/php-amqplib.png)](http://travis-ci.org/videlalvaro/php-amqplib)

This library is a _pure PHP_ implementation of the AMQP protocol. It's been tested against [RabbitMQ](http://www.rabbitmq.com/).

**Requirements: PHP 5.3** due to the use of `namespaces`.

The library was used for the PHP examples of [RabbitMQ in Action](http://manning.com/videla/) and the [official RabbitMQ tutorials](http://www.rabbitmq.com/tutorials/tutorial-one-php.html).

## BC BREAKING CHANGES ##

Since version 2.0 this library uses `AMQP 0.9.1` by default. You shouldn't need to change your code, but test before upgrading.

## New since version 2.0 ##

Since now the library uses `AMQP 0.9.1` we added support for the following RabbitMQ extensions:

* Exchange to Exchange Bindings
* Basic Nack

Extensions that modify existing methods like `alternate exchanges` are also supported.

## Setup ##

 Add a `composer.json` file to your project:

```javascript
{
  "require": {
      "videlalvaro/php-amqplib": "v2.1.0"
  }
}
```

Then provided you have [composer](http://getcomposer.org) installed, you can run the following command:

```bash
$ composer.phar install
```

That will fetch the library and its dependencies inside your vendor folder. Then you can add the following to your
.php files in order to use the library

```php
require_once __DIR__.'/vendor/autoload.php';
```

Then you need to `use` the relevant classes, for example:

```php
use PhpAmqpLib\Connection\AMQPConnection;
use PhpAmqpLib\Message\AMQPMessage;
```

## Usage ##

With RabbitMQ running open two Terminals and on the first one execute the following commands to start the consumer:

```bash
$ cd php-amqplib/demo
$ php amqp_consumer.php
```

Then on the other Terminal do:

```bash
$ cd php-amqplib/demo
$ php amqp_publisher.php some text to publish
```

You should see the message arriving to the process on the other Terminal

Then to stop the consumer, send to it the `quit` message:

```bash
$ php amqp_publisher.php quit
```

If you need to listen to the sockets used to connect to RabbitMQ then see the example in the non blocking consumer.

```bash
$ php amqp_consumer_non_blocking.php
```

To not repeat ourselves, if you want to learn more about this library, 
please refer to the [official RabbitMQ tutorials](http://www.rabbitmq.com/tutorials/tutorial-one-php.html).

## More Examples ##

- `amqp_ha_consumer.php`: demos the use of mirrored queues
- `amqp_consumer_exclusive.php` and `amqp_publisher_exclusive.php`: demos fanout exchanges using exclusive queues.
- `amqp_consumer_fanout_{1,2}.php` and `amqp_publisher_fanout.php`: demos fanout exchanges with named queues.
- `basic_get.php`: demos obtaining messages from the queues by using the _basic get_ AMQP call.

## Debugging ##

If you want to know what's going on at a protocol level then add the following constant to your code:

```php
<?php
define('AMQP_DEBUG', true);

... more code

?>
```

## Benchmarks ##

To run the publishing/consume benchmark type:

```bash
$ make benchmark
```

## Tests ##

To successfully run the tests you need to first setup the test `user` and test `virtual host`.

You can do that by running the following commands after starting RabbitMQ:

```bash
$ rabbitmqctl add_vhost phpamqplib_testbed
$ rabbitmqctl add_user phpamqplib phpamqplib_password
$ rabbitmqctl set_permissions -p phpamqplib_testbed phpamqplib ".*" ".*" ".*"
```

Once your environment is set up you can run your tests like this:

```bash
$ make test
```

## Using AMQP 0.8 ##

If you still want to use the old version of the protcol then you can do it by settings the following constant in your configuration code:

```php
define('AMQP_PROTOCOL', '0.8');
```

The default value is `'0.9.1'`.

## Original README: ##

Below is the original README file content. Credits goes to the original authors.

PHP library implementing Advanced Message Queuing Protocol (AMQP).

The library is port of python code of py-amqplib
http://barryp.org/software/py-amqplib/

It have been tested with RabbitMQ server.

Project home page: http://code.google.com/p/php-amqplib/

For discussion, please join the group:

http://groups.google.com/group/php-amqplib-devel

For bug reports, please use bug tracking system at the project page.

Patches are very welcome!

Author: Vadim Zaliva <lord@crocodile.org>
