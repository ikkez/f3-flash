# Flash

This is a little plugin to add simple Flash Messages and Flash Keys for PHP Fat-Free-Framework, version 3.x

### Installation


- Method 1: use composer `composer require ikkez/f3-flash`

- Method 2: copy the `flash.php` file into your F3 `lib/` directory or another directory that is known to the [AUTOLOADER](https://fatfreeframework.com/quick-reference#AUTOLOAD)


### Usage


To add a message (or multiple) that should only be displayed once in your template on the next request, just do:

```php
\Flash::instance()->addMessage('You did that wrong.', 'danger');
// or 
\Flash::instance()->addMessage('It worked!', 'success');
```

And to display that in your templates do:

```html
<!-- bootstrap 4 style-->
<repeat group="{{ \Flash::instance()->getMessages() }}" value="{{ @msg }}">
<div class="alert alert-{{ @msg.status }} alert-dismissable">
  <button type="button" class="close" data-dismiss="alert" aria-hidden="true">&times;</button>
  {{ @msg.text | raw }}
</div>
</repeat>

<!-- bootstrap 5 style-->
<repeat group="{{ \Flash::instance()->getMessages() }}" value="{{ @msg }}">
<div class="alert alert-{{ @msg.status }} alert-dismissable fade show">
  {{ @msg.text | raw }}
  <button type="button" class="btn-close float-end" data-bs-dismiss="alert" aria-label="Close"></button>
</div>
</repeat>
```

That's it.

If you need, you could also add simple keys:


```php
$flash = \Flash::instance()
$f3->set('FLASH', $flash);
$flash->setKey('highlight','bg-success'); // with value
$flash->setKey('show-hint'); // without returns just TRUE
$flash->setKey('error','Catastrophic error occured! ');
```

for use cases like:

```html
<div class="box {{ @FLASH->getKey('highlight') }}">
  <check if="{{ @FLASH->getKey('show-hint') }}">
  <p>It's new !!!</p>
  </check>
  ...
</div>
```

```html
<check if="{{ @@FLASH && @FLASH->hasKey('error') }}">
    <p>{{ @FLASH->getKey('error') }}</p>
</check>
```



## License

You are allowed to use this plugin under the terms of the GNU General Public License version 3 or later.

Copyright (C) 2021 Christian Knuth [ikkez]

