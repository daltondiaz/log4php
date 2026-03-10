# Log4php

A versatile logging framework for PHP. This project is a fork of Apache log4php, modernized for PHP 8.0+ compatibility.

## Table of Contents

- [Installation](#installation)
- [Basic Usage](#basic-usage)
- [Documentation](#documentation)
- [Contributing](#contributing)
- [Development Setup](#development-setup)
- [Running Tests](#running-tests)
- [Project Structure](#project-structure)
- [License](#license)

## Installation

Install via Composer:

```bash
composer require daltondiaz/log4php
```

## Basic Usage

```php
<?php
require_once 'vendor/autoload.php';

// Configure logger
\Logger::configure('config.xml');

// Get a logger instance
$logger = \Logger::getLogger(__CLASS__);

// Log messages
$logger->info('This is an info message');
$logger->error('This is an error message');
$logger->debug('Debug information');
```

## Documentation

For detailed documentation, visit the Apache log4php project website:  
[http://logging.apache.org/log4php/](http://logging.apache.org/log4php/)

## Contributing

We welcome contributions! Whether it's bug fixes, new features, improvements, or documentation, please follow the guidelines below.

### Development Setup

#### Prerequisites

- **PHP**: 8.0 or higher
- **Composer**: Latest version
- **Git**: For version control

#### Clone and Setup

```bash
# Clone the repository
git clone https://github.com/daltondiaz/log4php.git
cd log4php

# Install dependencies (including dev dependencies)
composer install --ignore-platform-req=ext-mongodb

# The --ignore-platform-req flag is needed due to MongoDB extension version constraints
```

#### Project Structure

```
log4php/
├── src/
│   ├── main/php/          # Main source code
│   │   ├── appenders/     # Output appenders (File, Database, Email, etc.)
│   │   ├── layouts/       # Message format layouts
│   │   ├── filters/       # Log filtering
│   │   └── *.php          # Core classes (Logger, LoggerLevel, etc.)
│   ├── test/php/          # PHPUnit test files
│   │   ├── appenders/     # Appender tests
│   │   ├── configurators/ # Configuration tests
│   │   ├── layouts/       # Layout tests
│   │   ├── renderers/     # Renderer tests
│   │   └── *.php          # Core class tests
│   ├── resources/         # Test configuration files
│   └── examples/          # Usage examples
├── vendor/                # Composer dependencies
├── phpunit.xml           # PHPUnit configuration
├── composer.json         # Project dependencies
└── README.md            # This file

```

### Running Tests

#### Before You Start

Make sure you've completed the [Development Setup](#development-setup) section.

#### Run All Tests

```bash
# Run the complete test suite
./vendor/bin/phpunit --verbose --testdox

```

#### Run Specific Tests

```bash
# Run a single test file
./vendor/bin/phpunit --testdox src/test/php/LoggerLevelTest.php

# Run tests for a specific component
./vendor/bin/phpunit --testdox src/test/php/appenders/

# Run with verbose output
./vendor/bin/phpunit --testdox
```

#### Generate Coverage Report

```bash
# Generate HTML coverage report
./vendor/bin/phpunit --coverage-html target/test/report
```

Coverage reports will be generated in `target/test/report/index.html`

#### Test Status

- ✅ **261 tests** - All passing
- ✅ **967 assertions** - All passing
- ⚠️ **46 deprecation warnings** - Related to PHPUnit 10 compatibility (backward compatible)
- ⏭️ **13 tests skipped** - Optional extensions not available

### How to Contribute

#### 1. Create an Issue First (Recommended)

Before starting work, create an issue to discuss:
- Bug reports (with reproduction steps)
- Feature requests (with use cases)
- Improvements or refactoring ideas

This helps ensure your work aligns with project goals.

#### 2. Fork and Branch

```bash
# Fork the repository on GitHub

# Clone your fork
git clone https://github.com/YOUR-USERNAME/log4php.git
cd log4php

# Add upstream remote
git remote add upstream https://github.com/daltondiaz/log4php.git

# Create a feature branch
git checkout -b feature/your-feature-name
# or for bug fixes
git checkout -b fix/your-bug-fix-name
```

#### 3. Development Workflow

```bash
# Install dependencies and ignore mongo if you dont use it
composer install --ignore-platform-req=ext-mongodb

# Make your changes in src/main/php/

# If adding functionality, also add tests in src/test/php/
```

#### 4. Write Tests

For any new functionality or bug fixes, add corresponding test cases:

```php
<?php
// Example: src/test/php/YourNewFeatureTest.php
class YourNewFeatureTest extends \PHPUnit\Framework\TestCase
{
    public function testYourNewFeature()
    {
        // Arrange
        $object = new YourClass();
        
        // Act
        $result = $object->yourMethod();
        
        // Assert
        self::assertEquals('expected', $result);
    }
}
```

Run your tests to ensure they pass:

```bash
./vendor/bin/phpunit src/test/php/YourNewFeatureTest.php
```

#### 5. Code Style Guidelines

- Follow PSR-12 coding standards
- Use meaningful variable and method names
- Add PHPDoc comments for public methods
- Keep methods focused and single-responsibility

Example:

```php
<?php
/**
 * Get the logger instance for the specified class
 *
 * @param string $class The class name
 * @return Logger The logger instance
 */
public static function getLogger($class)
{
    // Implementation
}
```

#### 6. Run Full Test Suite

Before submitting, ensure all tests pass:

```bash
# Run entire test suite
./vendor/bin/phpunit

# Should see: WARNINGS! (46 warnings are expected and backward compatible)
# Should NOT see: FAILURES or ERRORS
```

#### 7. Commit Changes

```bash
# Stage your changes
git add .

# Commit with descriptive message for features and changes
git commit -m "feat: description of your changes"

# Commit with descriptive message for bug fix 
git commit -m "fix: description of your fix"

# Commit with descriptive message for refactor
git commit -m "refactor: description of your refactor"

# Commit with descriptive message for any change or new doc
git commit -m "docs: description of your refactor"

# Push to your fork
git push origin feature/your-feature-name
```

**Commit Message Guidelines:**
- Use imperative mood ("Add" not "Added", "Fix" not "Fixed")
- Start with a capital letter
- Keep the subject line under 50 characters
- Add detailed description in the body if needed

Examples:
```
feat: Add support for custom appender configuration
fix: Fix timezone issue in date formatting
docs: Update LoggerLevel documentation
refactor: Refactor LoggerConfigurator for better readability
```

#### 8. Create a Pull Request

1. Go to your fork on GitHub
2. Click "New Pull Request"
3. Select `main` as the base branch
4. Provide a clear title and description
5. Reference any related issues (e.g., "Fixes #123")
6. Wait for review and CI checks to pass

**Pull Request Template:**

```markdown
## Description
Brief description of your changes

## Related Issue
Fixes #123 (if applicable)

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## How to Test
Steps to verify your changes work

## Checklist
- [ ] Tests pass locally
- [ ] Added/updated tests for new functionality
- [ ] Updated documentation if needed
- [ ] Followed code style guidelines
```

#### 9. Respond to Feedback

- Be open to suggestions and constructive criticism
- Update your PR based on review feedback
- Push additional commits to address issues (no need to force push)

### Testing New Appenders or Features

If you're adding a new appender or layout:

```bash
# 1. Create a test file
touch src/test/php/appenders/YourNewAppenderTest.php

# 2. Write comprehensive tests
# 3. Run your tests
./vendor/bin/phpunit --testdox src/test/php/appenders/YourNewAppenderTest.php

# 4. Run full suite to ensure no regressions
./vendor/bin/phpunit --testdox
```

### Common Development Tasks

#### Add a New Appender

1. Create: `src/main/php/appenders/LoggerAppenderYourName.php`
2. Extend: `LoggerAppender`
3. Implement: `append()` method
4. Create tests: `src/test/php/appenders/LoggerAppenderYourNameTest.php`

#### Add a New Layout

1. Create: `src/main/php/layouts/LoggerLayoutYourName.php`
2. Extend: `LoggerLayout`
3. Implement: `format()` method
4. Create tests: `src/test/php/layouts/LoggerLayoutYourNameTest.php`

#### Report a Bug

Create an issue with:
- Clear title describing the bug
- PHP version and environment details
- Minimal code to reproduce
- Expected vs actual behavior
- Error messages or stack traces

## License

Licensed under the Apache License, Version 2.0. See the [LICENSE](LICENSE) file for details.

---

## Getting Help

- **Questions?** Create a GitHub Discussion or Issue
- **Found a bug?** Open an Issue with reproduction steps
- **Have an idea?** Share it in a GitHub Discussion
- **Documentation unclear?** Help us improve by reporting it

Thank you for contributing! 🎉
