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

$collection = new LazyCollection();
$collection = new LazyCollection(['my', 'initial', 'array']);
```

The collections implement `CollectionInterface`, only `Collection` is countable.

Available collections:

- `Collection`: default collection
- `LazyCollection`: lazy collection whose uses generators to improve performances, but is *unique usage*!

### `CollectionInterface` methods

#### `CollectionInterface::new(Closure|iterable $iterable): static`

Create new instance of current collection.

```php
$collection = Collection::new(['foo', 'bar']);
```

#### `CollectionInterface::getArrayCopy(): array`

Use method to get the array representation of your collection.

```php
$collection = new Collection();
$collection->getArrayCopy(); // Returns `[]`

$collection = new Collection(['my', 'initial', 'array']);
$collection->getArrayCopy(); // Returns `['my', 'initial', 'array']`
```

#### `CollectionInterface::isEmpty(): bool`

Know if collection is empty.

```php
Collection::new(['foo', 'bar'])->isEmpty(); // Returns FALSE
Collection::new()->isEmpty(); // Returns TRUE
```

#### `CollectionInterface::collect(): self`

Collect al data from current collection into another one.
For lazy connection, collect all remaining items into classic collection.

```php
$collection = Collection::new(['foo', 'bar']);
$newCollection = $collection->collect();
```

#### `CollectionInterface::sort(callable|int|null $callback = null): self`

Sort items of collection.

```php
$collection = Collection::new(['foo', 'bar']);
$collection = $collection->sort();
$collection->getArrayCopy(); // Returns `['bar', 'foo']`
```

Similar to PHP array sort functions.

#### `CollectionInterface::filter(?callable $callback = null): self`

Filter items with callback.

```php
$collection = Collection::new([1, 10, 20, 100]);
$collection = $collection->filter(fn($value) => $value >= 20);
$collection->getArrayCopy(); // Returns `[20, 100]`
```

Similar to `array_filter()` function.

#### `CollectionInterface::filterInstanceOf(string|object ...$class): self`

Filter items with object instance comparison.

```php
$collection = Collection::new([new stdClass(), new SimpleXMLElement()]);
$collection = $collection->filterInstanceOf(stdClass::class);
$collection->getArrayCopy(); // Returns `[object<stdClass>]`
```

Similar to `is_a()` function.

#### `CollectionInterface::map(callable $callback): self`

Apply callback on items.

Similar to `array_map()` function.

#### `CollectionInterface::search(callable $callback): mixed`

Search item with callback.

```php
$collection = Collection::new(['foo', 'bar', 'baz']);
$collection = $collection->filter(fn($value) => str_starts_with('ba', $value));
$collection->getArrayCopy(); // Returns `['bar', 'baz']`
```

Similar to `array_search()` function.

#### `CollectionInterface::get(int $index = 0): mixed`

Get item at index.

Negative index, starts at end of collection.

```php
$collection = Collection::new(['foo', 'bar', 'baz']);
$collection = $collection->get(); // Return `'foo'`
$collection = $collection->get(1); // Return `'bar'`
$collection = $collection->get(-1); // Return `'baz'`
```

#### `CollectionInterface::first(?callable $callback = null): mixed`

Search first item.

If callback given, search first item whose respect callback.

```php
$collection = Collection::new(['foo', 'bar', 'baz']);
$collection = $collection->first(); // Return `'foo'`
$collection = $collection->first(fn($value) => str_starts_with('ba', $value)); // Return `'bar'`
```

#### `CollectionInterface::last()`

Search last item.

If callback given, search first item whose respect callback.

```php
$collection = Collection::new(['foo', 'bar', 'baz']);
$collection = $collection->last(); // Return `'baz'`
$collection = $collection->last(fn($value) => str_starts_with('ba', $value)); // Return `'baz'`
```

#### `CollectionInterface::slice(int $offset, int|null $length = null): self`

Extract a slice of the collection.

```php
$collection = Collection::new(['foo', 'bar', 'baz']);
$collection->slice(0, 2)->getArrayCopy(); // Returns `['foo', 'bar']`
$collection->slice(1)->getArrayCopy(); // Returns `['bar', 'baz']`
$collection->slice(-2, 2)->getArrayCopy(); // Returns `['bar', 'baz']`
$collection->slice(-1)->getArrayCopy(); // Returns `['baz']`
```

Similar to `array_slice()` function.

#### `CollectionInterface::contains(mixed $value, bool $strict = false): bool`

Collection contains value?

```php
$collection = Collection::new(['foo', 'bar', '2', 'baz']);
$collection->contains('foo'); // Returns `true`
$collection->contains('qux'); // Returns `false`
$collection->contains(2); // Returns `true`
$collection->contains(2, true); // Returns `false`
```

Similar to `in_array()` function.

#### `CollectionInterface::chunk(int $length): self`

Chunk collection items into collection of fixed length.

```php
$collection = Collection::new(['foo', 'bar', 'baz']);
$collection = $collection->chunck(2); // Returns 2 collections
$collection->getArrayCopy(); // Returns `[['foo', 'bar'], ['baz']]`
```

Similar to `array_chunk()` function.

#### `CollectionInterface::keys(): self`

Get keys of collection items.

```php
$collection = Collection::new(['k1' => 'foo', 1 => 'bar', 'k2' => 'baz']);
$collection->keys()->getArrayCopy(); // Returns `['k1', 1, 'k2']`
```

Similar to `array_keys()` function.

#### `CollectionInterface::values(): self`

Get values of collection items.

```php
$collection = Collection::new(['k1' => 'foo', 1 => 'bar', 'k2' => 'baz']);
$collection->keys()->getArrayCopy(); // Returns `['foo', 'bar', 'baz']`
```

Similar to `array_values()` function.

#### `CollectionInterface::unique(): self`

Get unique items of collection items.

```php
$collection = Collection::new(['k1' => 'foo', 1 => 'foo', 'bar', 'k2' => 'baz']);
$collection->unique()->getArrayCopy(); // Returns `['k1' => 'foo', 'bar', 'k2' => 'baz']`
```

Similar to `array_unique()` function.

#### `CollectionInterface::flip(): self`

Flip keys and values.

```php
$collection = Collection::new(['k1' => 'foo', 1 => 'foo', 'bar', 'k2' => 'baz']);
$collection->flip()->getArrayCopy(); // Returns `['foo' => 'k1', 'bar' => 0, 'baz' => 'k2']`
```

Similar to `array_flip()` function.

#### `CollectionInterface::column(string|int|Closure|null $column_key, string|int|Closure|null $index_key = null): self`

Get column value or reindex collection.

```php
$collection = Collection::new([
    ['k1' => 'foo', 'value' => 'foo value'],
    ['k1' => 'bar', 'value' => 'bar value'],
    ['k1' => 'baz', 'value' => 'baz value'],
]);
$collection = $collection->column('k1')->getArrayCopy(); // Returns `['foo', 'bar', 'baz']`
$collection = $collection->column('value', 'k1')->getArrayCopy(); // Returns `['foo' => 'foo value', 'bar' => 'bar value', 'baz' => 'baz value']`
```

Similar to `array_column()` function.

#### `CollectionInterface::rand(int $length = 1): self`

Get random values of collection.

```php
$collection = Collection::new(['foo', 'bar', 'baz']);
$collection = $collection->rand(2)->getArrayCopy(); // Returns 2 values random
```

Similar to `array_rand()` function.

#### `CollectionInterface::sum(): float|int`

Get sum of values.

```php
$collection = Collection::new([1, 2, 3, 4]);
$collection->sum(); // Returns `10`
```

Similar to `array_sum()` function.

#### `CollectionInterface::avg(): float|int`

Get average of values.

```php
$collection = Collection::new([1, 2, 3, 4]);
$collection->avg(); // Returns `2.5`
```

#### `CollectionInterface::median(): float|int`

Get median of values.

```php
$collection = Collection::new([1, 3, 5, 7]);
$collection->median(); // Returns `4`
```

#### `CollectionInterface::variance(): float|int`

Get population variance of values.

```php
$collection = Collection::new([1, 1, 2, 2, 3, 5]);
$collection->variance(); // Returns `1.888888888889`
```

#### `CollectionInterface::deviation(): float|int`

Get population deviation of values.

```php
$collection = Collection::new([1, 3, 5, 7]);
$collection->deviation(); // Returns `2.2360679775`
```

#### `CollectionInterface::reduce(callable $callback, mixed $initial = null): mixed`

Reduce collection with callback and optional initial value.

```php
$collection = Collection::new([1, 2, 3, 4]);
$collection->reduce(fn($carry, $item) => $carry + $item, 10); // Returns `20`
$collection->reduce(fn($carry, $item) => $carry + $item); // Returns `10`
```

Similar to `array_reduce()` function.

### `Collection` methods

`Collection` class implement `ArrayAccess` interface to allow to manipulate collection like an array.

#### `Collection::append(mixed ...$value): static`

Append value(s) to collection.

```php
$collection = Collection::new(['foo', 'bar']);
$collection->append('baz', 'qux')->getArrayCopy(); // Returns `['foo', 'bar', 'baz', 'qux']`
```

Similar to `array_push()` function.

#### `Collection::prepend()`

Prepend value(s) to collection.

```php
$collection = Collection::new(['foo', 'bar']);
$collection->prepend('baz', 'qux')->getArrayCopy(); // Returns `['baz', 'qux', 'foo', 'bar']`
```

Similar to `array_unshift()` function.

#### `Collection::count(): int`

Count number of items in collection.

```php
$collection = Collection::new(['foo', 'bar', 'baz']);
$collection->count(); // Returns `3`
count($collection); // Returns `3`
```

Similar to `count()` function.

#### `Collection::lazy(): CollectionInterface`

New lazy collection from current collection.

### `LazyCollection` methods

Lazy collection use generators to improve performances.
Usage of a collection is unique, but can be chained.

#### `Collection::count(int &$length = 0): CollectionInterface`

Count number of items and return new collection.

```php
$collection = LazyCollection::new(['foo', 'bar', 'baz']);
$length = 0;
$collection = $collection->count($length);
print $length; // Print `3`
```