# Dingo Serializer Switch

This is a middleware for dingo/api to switch serializer

If a resource's relationship is null, we can return `$this->null()` in a transformer. But default serializer return [], I think null is better.
Also when pagination has no links, default is [], I wish to return null. So I write two serializer to fix this.

If you want to use default serializer just use `default_array` or `default_data_array`.

## Installation

### Laravel

- `composer require umvae67/dingo-serializer-switch`


### Lumen

*bootstrap/app.php*
```php
$app->routeMiddleware([
    // ...
    'serializer' => Umvae67\Dingo\SerializerSwitch::class,
]);
```

## Usage

```
$api->version('v1',
    ['middleware' => 'serializer:array'],
    function ($api) {
});

$api->version('v2',
    ['middleware' => 'serializer'],
    function ($api) {
});

$api->version('v3',
    ['middleware' => 'serializer:data_array'],
    function ($api) {
});
```

default key is data_array, so v2 v3 is same.

```
'default_array' => 'League\Fractal\Serializer\ArraySerializer',
'default_data_array' => 'League\Fractal\Serializer\DataArraySerializer',
'json_api' => 'League\Fractal\Serializer\JsonApiSerializer',

'array' => 'Umvae67\Dingo\Serializers\ArraySerializer',
'data_array' => 'Umvae67\Dingo\Serializers\DataArraySerializer',
```

## License
[MIT LICENSE](https://github.com/umvae67/dingo-api-serializer-switch/blob/master/LICENSE)
