# Change Log

All notable changes to this project will be documented in this file. This project adheres
to [Semantic Versioning] (http://semver.org/). For change log format,
use [Keep a Changelog] (http://keepachangelog.com/).

## [1.0.0-beta5] - In progress

### Added

- New method `CollectionInterface::each(): self`
- New method `CollectionInterface::all(): array`

### Changed

- `CollectionInterface` implements now `\Countable`, so signature of method `LazyCollection::count()` changed

### Fixed

- Fix `CollectionInterface::collect(): self` with sub collections

## [1.0.0-beta4] - 2022-09-01

### Added

- New method `CollectionInterface::multiSort(): self`

## [1.0.0-beta3] - 2022-04-29

### Added

- New method `CollectionInterface::isEmpty(): bool`
- New method `CollectionInterface::median(): float|int` to calculate median of collection values
- New method `CollectionInterface::variance(): float` to calculate population variance of collection values
- New method `CollectionInterface::deviation(): float` to calculate population deviation of collection values

### Changed

- Return type of `Collection::getIterator()` method

### Removed

- `callback` argument of method `CollectionInterface::chunk()`

## [1.0.0-beta2] - 2022-04-28

### Added

- `LazyCollection` collection
- Common tests for all `CollectionInterface`

## [1.0.0-beta1] - 2022-02-19

Initial development.
