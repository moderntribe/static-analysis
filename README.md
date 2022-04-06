# Modern Tribe Static Analysis Using PHPStan

## Install

Composer v2:

```sh
composer require --dev moderntribe/static-analysis
```

Composer v1:

Add to the `repositories` object:

```json
    {
      "type": "vcs",
      "url": "git@github.com:moderntribe/static-analysis.git"
    }
```

And `require-dev`:

```json
  "moderntribe/static-analysis": "^0.0"
```

## Usage

To run static analysis on your project, create `phpstan.neon.dist` file in your project root with the following content:

```neon
parameters:
	level: 2
	paths:
		- wp-content/themes/core/
		- wp-content/plugins/core/
		- wp-content/mu-plugins/
	excludePaths:
		- vendor
	bootstrapFiles:
		- vendor/php-stubs/wordpress-stubs/wordpress-stubs.php
		- vendor/php-stubs/acf-pro-stubs/acf-pro-stubs.php
	tmpDir: .phpstan-cache/
	ignoreErrors:
		- '#^Function yoast_get_primary_term_id not found.$#'

	checkAlwaysTrueStrictComparison: true

	# Unfortunately, DocBlocks can't be relied upon in WordPress.
	treatPhpDocTypesAsCertain: false
```

To run phpstan on your project, run `phpstan analyse --configuration=phpstan.neon.dist` from your project root.
