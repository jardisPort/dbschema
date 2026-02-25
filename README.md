# DbSchema

![Build Status](https://github.com/jardisCore/dbschema/actions/workflows/ci.yml/badge.svg)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![PHP Version](https://img.shields.io/badge/php-%3E%3D8.2-blue.svg)](https://www.php.net/)
[![PHPStan Level](https://img.shields.io/badge/PHPStan-Level%208-success.svg)](phpstan.neon)
[![PSR-4](https://img.shields.io/badge/autoload-PSR--4-blue.svg)](https://www.php-fig.org/psr/psr-4/)
[![PSR-12](https://img.shields.io/badge/code%20style-PSR--12-orange.svg)](phpcs.xml)

PHP library providing database schema interfaces for Domain Driven Design (DDD) approaches.

## Installation

```bash
composer require jardisport/dbschema
```

## Requirements

- PHP >= 8.2

## Interfaces

This package provides two complementary interfaces for database schema operations:

### DbSchemaReaderInterface

Read and introspect database schema information:

```php
use JardisPort\DbSchema\DbSchemaReaderInterface;

class YourSchemaReader implements DbSchemaReaderInterface
{
    public function tables(): ?array
    {
        // Return list of all tables in the database
    }

    public function columns(string $container, ?array $fields = null): ?array
    {
        // Return columns for a table, optionally filtered by specified fields
    }

    public function indexes(string $container): ?array
    {
        // Return indexes for a table
    }

    public function foreignKeys(string $container): ?array
    {
        // Return foreign keys for a table
    }

    public function fieldType(string $fieldType): ?string
    {
        // Map database field types to PHP types (e.g., 'varchar' -> 'string')
    }

    public function getDriverName(): string
    {
        // Return the name of the database driver (e.g., 'mysql', 'pgsql', 'sqlite')
    }
}
```

### DbSchemaExporterInterface

Export database schema in various formats:

```php
use JardisPort\DbSchema\DbSchemaExporterInterface;

class YourSchemaExporter implements DbSchemaExporterInterface
{
    public function toSql(array $tables): string
    {
        // Export schema as SQL DDL script
    }

    public function toJson(array $tables, bool $prettyPrint = false): string
    {
        // Export schema as JSON
    }

    public function toArray(array $tables): array
    {
        // Export schema as PHP array
    }
}
```

## Terminology

- **Container**: Database-agnostic term for "table" (aligned with DDD principles)
- **Fields**: Specific column attributes to retrieve when querying columns

## Development

This project uses Docker for all development operations. See [CLAUDE.md](.claude/CLAUDE.md) for detailed instructions.

### Quick Start

```bash
# Install dependencies
make install

# Run code quality checks
make phpcs
make phpstan

# Access container shell
make shell
```

### Code Quality Standards

- **PHP Version**: 8.2+ (development: 8.3)
- **Coding Standard**: PSR-12
- **Static Analysis**: PHPStan Level 8
- **Strict Types**: Required in all files

## Contributing

1. Follow branch naming: `feature/[ticket]_description` or `fix/[ticket]_description`
2. Pre-commit hooks enforce code standards automatically
3. All PRs must pass PHPCS and PHPStan checks

## License

MIT

## Support

- Issues: https://github.com/JardisPort/dbschema/issues
- Email: jardisCore@headgent.dev
