ToInlineStyleEmailBundle
========================

[![Latest Stable Version](https://img.shields.io/packagist/v/vysokeskoly/to-inline-style-email-bundle.svg)](https://packagist.org/packages/vysokeskoly/to-inline-style-email-bundle)
[![License](https://img.shields.io/packagist/l/vysokeskoly/to-inline-style-email-bundle.svg)](https://packagist.org/packages/vysokeskoly/to-inline-style-email-bundle)
[![PHP - Checks](https://github.com/vysokeskoly/ToInlineStyleEmailBundle/actions/workflows/php-checks.yaml/badge.svg)](https://github.com/vysokeskoly/ToInlineStyleEmailBundle/actions/workflows/php-checks.yaml)

**ToInlineStyleEmailBundle** is a _Symfony2_ bundle to use the **CssToInlineStyles** translator by _Tijs Verkoyen_ (see
https://github.com/tijsverkoyen/CssToInlineStyles for the repository)

Requirements
============
**ToInlineStyleEmailBundle** is only supported on **PHP 8.1** and up.

Installation
============
Please, use the _Composer_ to install this bundle in your Symfony2 app.

The following lines should be added in your ```composer.json```

``` json
"require": {
    "vysokeskoly/to-inline-style-email-bundle": "^3.0"
},
```

Then, register the bundle in your AppKernel by adding the following line:

``` php
    VysokeSkoly\ToInlineStyleEmailBundle\ToInlineStyleEmailBundle::class => ['all' => true],
```

Documentation and Examples
==========================
The bundle provides a service named **css_to_inline_email_converter**. Use it in a controller to have a nice shortcut to the
converter developed by _Tijs Verkoyen_. E.g.:

``` php
public function indexAction() {
    $converter = $this->get('css_to_inline_email_converter');
    ...
}
```

Get the HTML and the CSS as a string and set this required values to the converter object, e.g.

``` php
$converter = $this->get('css_to_inline_email_converter');

$html = ...; // get the HTML here
$css = ....; // get the CSS here

return $converter->inlineCSS($html, $css);
```

The retrieval of the HTML and CSS files from its folder it is only up-to you. E.g. in your controller retrieve the content of your CSS as:

``` php
file_get_contents($this->container->getParameter('kernel.root_dir').'/../src/Acme/TestBundle/Resources/css/mystyle.css');
```

Of course, it is supposed that a Symfony user will use a template instead of a static HTML page. Hence,
for convenience, the service provides a function capable to render a template. E.g.:

``` php
$converter->setHTMLByView(
    'AcmeTestBundle:MyController:my_template.html.twig',
    [
        'param_1' => $val_of_param_1,
        // ...,
        'param_n' => $val_of_param_n
    ]
);
```

The preceding function must be used _in vece_ of function ```setHTML()```.

To use the ```generateStyledHTML``` method just use it like:

``` php
$converter->setHtml($html);
$converter->setCss($css);
return $converter->generateStyledHTML();
```

You can use inline css directly in Twig template:

``` html
{% inlinecss '/css/email.css' %}
<div class="foo">
...
</div>
{% endinlinecss %}
```

Paths relative to bundle are supported as well:

``` html
{% inlinecss '@AppBundle/Resources/css/email.css' %}
<div class="foo">
...
</div>
{% endinlinecss %}
```
Dynamic variable is supported (Use absolute path with variable with asset or directly with full path to file)

``` html
{% set path = asset('css/email.css', null, true) %}
{% inlinecss path %}
<div class="foo">
...
</div>
{% endinlinecss %}
```
Dynamic variable is supported (Use absolute path with variable with asset or directly with full path to file)

``` html
{% set path = asset('css/email.css', null, true) %}
{% inlinecss path %}
<div class="foo">
...
</div>
{% endinlinecss %}
```

Read the docs in the files for further details on the usage of the service.

Contributing
============
**ToInlineStyleEmailBundle** is an open source project, under MIT license. Contributions are encouraged.
Feel free to contribute to improve this bundle.

About the author of the bundle
==============================
**ToInlineStyleEmailBundle** has been originally developed by Roberto Trunfio. Currently, the bundle is mantained by Luis Cordova via the gushphp organization.

The initial package on packagist robertotru was moved here to gushphp organization with the author consent for maintenance.
