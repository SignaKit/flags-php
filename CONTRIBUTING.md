# Contributing to SignaKit Flags — PHP SDK

## Requirements

- PHP 8.1+
- Composer 2+

## Getting Started

```bash
git clone https://github.com/SignaKit/flags-php.git
cd flags-php
composer install
```

## Running Tests

```bash
vendor/bin/phpunit
```

## Project Structure

```
src/
  SignaKitClient.php           # Main client — flag resolution public API
  SignaKitUserContext.php      # User context builder
  Evaluator.php                # Flag evaluation algorithm
  AudienceMatcher.php          # Audience rule matching
  Hasher.php                   # MurmurHash3 for deterministic user bucketing
  ConfigManager.php            # Config fetching, ETag caching, polling
  Contracts/
    HttpClientInterface.php    # HTTP client abstraction
  Http/
    CurlHttpClient.php         # Default cURL HTTP client
    GuzzleHttpClient.php       # Optional Guzzle HTTP client
  Types/
    Decision.php               # Decision result type
    ProjectConfig.php          # Deserialized config type

tests/
  AudienceMatcherTest.php
  ConfigManagerTest.php
  EvaluatorTest.php
  HasherTest.php
  SignaKitUserContextTest.php
```

## Making Changes

1. Fork the repo and create a branch from `main`.
2. Make your changes. Add or update tests to cover them.
3. Run `vendor/bin/phpunit` — all tests must pass.
4. Open a pull request against `main`.

## Releasing

Releases are triggered automatically when `composer.json` is updated on `main`. To cut a release:

1. Bump `version` in `composer.json` (e.g. `1.2.2`).
2. Open a PR with the version bump.
3. Merge — the publish workflow creates and pushes the `vX.Y.Z` git tag, which Packagist picks up automatically.

Packagist must be configured to watch this repository (Settings → Webhooks on Packagist, or via the GitHub service integration).

## Coding Conventions

- Target PHP 8.1+. Use typed properties, enums, fibers, and union types where appropriate.
- All public API methods must have PHPDoc blocks.
- The cURL client is the zero-dependency default — Guzzle is optional. Keep the core SDK free of required runtime dependencies.
- Follow PSR-4 autoloading and PSR-12 code style.

## Reporting Issues

Open an issue on GitHub with a description of the bug or feature request. For security vulnerabilities, email security@signakit.com instead of opening a public issue.
