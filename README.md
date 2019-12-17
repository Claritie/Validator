# Validator

This library is originally part of the Claritie framework for validating known as *Validator*.

## Requirements

- PHP >=5.3.6+

## Code Examples

```php
$rules = array
(
  'name' => 'alpha|required',
  'year' => 'num|required',
);

$Validation = new Validator();
$Validation->validate($_POST, $rules);

if (!empty($Validation->getErrors()))
{
  print_r($Validation->getErrors());
}

// or more viewable direction:
if (!$Validation->passed())
{
  $Validation->goBackWithErrors();
}
```

* Show validation errors (within HTML)
```html
 <label>Name :
      <input type="text" name="name">
 </label>
 <?= Validator::error('name') ? Validator::error('name') : ""; ?>
```

You can wrap error messages with custom HTML markup

```php
  Validator::error('confirm_password', '<span class="error">:message</span>');
```


## Rules
 * required
 * num
 * alpha
 * alpha-num
 * email
 * min:[number]
 * max:[number]
 * same:[field_name]


## Custom Expressions & Messages
* Custom Expressions

You can register your custom RegExp before running the validator

```php
$v->registerExpression( 'cnic', '#^([0-9]{13})$#', 'Invalid CNIC number' );
```

registerExpression method takes 3 arguments
* expressionID - unique name for the expression
* pattern - the RegExp string
* message [optional] - the error message to be retured if the validation fails

```Validator::registerExpression($expressionID , $pattern, $message)```


* Custom Messages

You can also pass a custom error message with each rule

```php
 $rules['full_name'] = "required--Please Enter your name|alpha-- Please don't use special charators and numbers";
```

## Conditional Rules
You can define specific conditional rules for a field
```php
 $rules['age'] = 'if:gender[Male](required|min:2|num)';
```

## Comparison Rules

You can also compare a field with another
```php
  $rules['password'] = 'required|min:8';
  $rules['confirm_password'] = 'same:password';
```

## Installation / Integration:
When using Claritie Beta (Skyfire), you can install **Validator** by calling 'Validator' within the load::service() function.
```php
load::service('Validator');
```
Also, externally you can use Validator independently by requiring 'index.php' from the main directory including the rest of the directory folders.
```php
require_once __DIR__.'index.php';
```


## License

Validator is licensed under the [MIT License](http://opensource.org/licenses/MIT).

Copyright 2015-2019 [Travis van der Font](http://travisfont.com)
