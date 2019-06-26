# Belongs To Many Field Nova

Belongs To Many field to represent many to many relationship in field. This Field allow attaching relationships easily, you can pass query to the Multiple Select.

![image](https://user-images.githubusercontent.com/11976865/54318738-46290000-45b5-11e9-8ea0-941adb4b79ba.png)


### Installation
```bash
composer require benjacho/belongs-to-many-field
```

### Usage

To use in nova 1.0 use 0.3 in nova 2.0 use 0.4 and above.

First of all use the trait in the model that you want to attach example User, user want to attach roles

```php
    use Benjacho\BelongsToManyField\HasBelongsToMany;

    class User extends Model {
        use HasBelongsToMany;
    }
```
Then in the resource you need to pass:
- Method make (label, many to many relationship, Nova Resource Relationship) 
- Method options (Here you pass option that you need to render in Multiple Select, you can pass Querys, use get() method for that purpose)
- Method relationModel (Here is a trick to pass the relation that you want to bind) Example User
- You dont need to pass onlyOnForms(), it is by default.

```php
use Benjacho\BelongsToManyField\BelongsToManyField;

public function fields(Request $request){
    BelongsToManyField::make('Role Label', 'roles', 'App\Nova\Role')->options(\App\Role::all())->relationModel(\App\User::class),
}
```

Optional

- Method optionsLabel('columnName'), this method is when you don't have column 'name' in your table and you want to label by another column name. By default it tracks by label 'name'


```php
use Benjacho\BelongsToManyField\BelongsToManyField;

public function fields(Request $request){
    BelongsToManyField::make('Role Label', 'roles', 'App\Nova\Role')->options(\App\Role::all())->relationModel(\App\User::class)->optionsLabel('title'),
}
```

### Validations
This package implement all Laravel Validations, you need to pass the rules in rules method, rules are listed on laravel validations rules for arrays*.
```php
use Benjacho\BelongsToManyField\BelongsToManyField;

public function fields(Request $request){
    BelongsToManyField::make('Role Label', 'roles', 'App\Nova\Role')->options(\App\Role::all())->relationModel(\App\User::class)->rules('required', 'min:1', 'max:5', 'size:3' new CustomRule),
}
```

![image](https://raw.githubusercontent.com/Benjacho/belongs-to-many-field-nova/master/validation.png)

For translations of this validations, use normal laravel validations translations.

### Todo
Implement validations, implement custom rules

### Contributing
-Pull Requests
-Issues
-Or Contact me: christianbfc97@gmail.com