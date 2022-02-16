# Hector Collection

[![Latest Version](https://img.shields.io/packagist/v/hectororm/collection.svg?style=flat-square)](https://github.com/hectororm/collection/releases)
[![Software license](https://img.shields.io/github/license/hectororm/collection.svg?style=flat-square)](https://github.com/hectororm/collection/blob/main/LICENSE)
[![Build Status](https://img.shields.io/github/workflow/status/hectororm/collection/Tests/main.svg?style=flat-square)](https://github.com/hectororm/collection/actions/workflows/tests.yml?query=branch%3Amain)
[![Quality Grade](https://img.shields.io/codacy/grade/4e2956935f2c4fc08166fe431e7211a3/main.svg?style=flat-square)](https://app.codacy.com/gh/hectororm/collection)
[![Total Downloads](https://img.shields.io/packagist/dt/hectororm/collection.svg?style=flat-square)](https://packagist.org/packages/hectororm/collection)

**Hector Collection** is the module of Hector ORM. Can be used independently of ORM.

## Installation

### Composer

You can install **Hector Collection** with [Composer](https://getcomposer.org/), it's the recommended installation.

```bash
$ composer require hectororm/collection
```

### Dependencies

* **PHP** ^8.0

## Usage

Collection can be view like an array. But you don't call `array_*()` functions but directly methods of collection.

```php
$collection = new Collection();
$collection = new Collection(['my', 'initial', 'array']);
```

The collections implement `CollectionInterface`, only `Collection` is countable.

### Methods

#### `CollectionInterface::getArrayCopy()`

Use method `Collection::getArrayCopy(): array` to get the array representation of your collection.

```php
$collection = new Collection();
$collection->getArrayCopy(); // Returns `[]`

$collection = new Collection(['my', 'initial', 'array']);
$collection->getArrayCopy(); // Returns `['my', 'initial', 'array']`
```

#### `CollectionInterface::append()`

#### `CollectionInterface::prepend()`

#### `CollectionInterface::sort()`

#### `CollectionInterface::filter()`

#### `CollectionInterface::filterInstanceOf()`

#### `CollectionInterface::map()`

#### `CollectionInterface::search()`

#### `CollectionInterface::first()`

#### `CollectionInterface::last()`

#### `CollectionInterface::contains()`

#### `CollectionInterface::chunk()`

#### `CollectionInterface::keys()`

#### `CollectionInterface::values()`

#### `CollectionInterface::unique()`

#### `CollectionInterface::flip()`

#### `CollectionInterface::column()`

#### `CollectionInterface::rand()`

#### `CollectionInterface::sum()`

#### `CollectionInterface::avg()`

#### `CollectionInterface::median()`

#### `CollectionInterface::reduce()`