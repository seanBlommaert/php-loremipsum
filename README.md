php-loremipsum
==============

Lorem ipsum generator without dependencies.

Origins
-------

Once upon a time, I was attempting to find a lorem ipsum generator over on [Packagist](https://packagist.org/search/?q=lorem%20ipsum). I was presented with many options, and some of those options were good. Unfortunately, the bulk of those options depended on Symphony or the Zend Framework. This wouldn’t have been a big deal but under the circumstances, I wanted something that was not tightly coupled to these frameworks because I wanted to use the generator in my _own_ framework.

I had decided to use [badcow/lorem-ipsum](https://packagist.org/packages/badcow/lorem-ipsum) because it did not have any dependencies nor did it rely on any external APIs. As I started to use the library, I found that I was going to have to fight with it to get it to do what I wanted. After digging through the code, I realized that I was going to end up gutting most of it to bend it to my will. I know when you overhaul someone’s code the liklihood of them accepting a pull request goes down dramatically, hence building this library while taking cues from it’s predecessor.

Installation
------------

The preferred installation method is via `composer`. First add the following to your `composer.json`

```json
"require": {
	"joshtronic/php-loremipsum": "dev-master"
}
```

Then run `composer update`

Usage
-----

### Getting Started

```php
require_once 'GravityBlvd/LoremIpsum.php';
$lipsum = new GravityBlvd\LoremIpsum();
```

### Generating Words

```php
echo '1 word: '  . $lipsum->word();
echo '5 words: ' . $lipsum->words(5);
```

### Generating sentences

```php
echo '1 sentence:  ' . $lipsum->sentence();
echo '5 sentences: ' . $lipsum->sentences(5);
```

### Generating paragraphs

```php
echo '1 paragraph:  ' . $lipsum->paragraph();
echo '5 paragraphs: ' . $lipsum->paragraphs(5);
```

### Wrapping text with HTML tags

If you would like to wrap the generated text with a tag, pass it as the second parameter:

```php
echo $lipsum->paragraphs(3, 'p');

// Generates: <p>Lorem ipsum...</p><p>...</p><p>...</p>
```

Multiple tags can also be specified:

```php
echo $lipsum->sentences(3, ['article', 'p']);

// Generptes: <article><p>...</p></article><article><p>...</p></article><article><p>...</p></article>
```

And you can back reference using `$1`:

```php
echo $lipsum->words(3, '<li><a href="$1">$1</a></li>');

// Generates: <li><a href="...">...</a></li><li><a href="...">...</a></li><li><a href="...">...</a></li>
```

### Return as an array

Perhaps you want an array instead of a string:

```php
print_r($lipsum->wordsArray(5));
print_r($lipsum->sentencesArray(5));
print_r($lipsum->paragraphsArray(5));
```

You can still wrap with markup when returning an array:

```php
print_r($lipsum->wordsArray(5), 'li');
```

Assumptions
-----------

* The first sentence or paragraph will always start with “Lorem ipsum…”
* Subsequent sentences and paragraphs will never start with “Lorem ipsum…”
* Words will never contain “lorem” or “ipsum”