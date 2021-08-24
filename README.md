# Laravel TLDR tutorial

#### Routing 
1. Controller route
```PHP
// web.php
use App\Http\Controllers\YourController;

Route::get('/path', [YourController::class, 'someFunction']);
```
\
2. Lambda function route

```PHP
// web.php
use Illuminate\Http\Request;

Route::get('/path', function (Request $request) {
    // ...
});
```
\
3. Return view\
index -> blade filename in resources/views e.g. index.blade.php, name for name.blade.php etc.\
idx -> variable name to bind in name view e.g. 'username'\
value -> value of the variable e.g. 'admin'\
```PHP
// Some controller e.g. IndexController.php
  public function doSomeThings() {
    return view('name', ['idx' => 'value']);
  }
```
\
4. Usage of variable in view
```PHP
// some blade.php file
<h1> Hello {{ $idx }} </h1>
// will return <h1> Hello value </h1>
````
\
5. Routes with parameters for lambda function
```PHP
// web.php
Route::get('/path/{someValue}', function ($someValue) {
    return 'You entered '.$someValue;
});
```
\
6. Routes with parameters for controller function
```PHP
// web.php
use App\Http\Controllers\YourController;

Route::get('/path/{someValue}', [YourController::class, 'someFunction']);

// YourController.php
...
public function someFunction($someValue) {
  // Do something
}
```
\
7. Name your route
```PHP
// web.php
Route::get('/some/path', function () {
    //
})->name('some.path');

// Some your controller e.g. IndexController.php
public function doSomething() { 
    // Generating URLs...
  $url = route('some.path');

  // Generating Redirects...
  return redirect()->route('some.path');
}
```
\
8. Group routes
```PHP
// web.php

Route::group(['prefix' => 'user'], function() {
    // /user
    Route::get('/',     [UserController::class, 'show'])->name('user.index');
    // /user/show
    Route::get('/show', [UserController::class, 'showAll'])->name('user.show');
    // /user/add
    Route::post('/add', [UserController::class, 'add'])->name('user.add');
    // ->name(...) is not required
});
```
\
9. Middleware\
What's that? Function which is called between route and controller e.g. we want to check if user is logged. Middleware validate and handle this. In below example I used auth middleware
```PHP
// web.php
Route::get('/some/path', function () {
    // do something
})->middleware('auth');
```
or
```PHP
// web.php
Route::get('/some/path', 
  [SomeController::class, 'someFunctionInController'
])->middleware('auth')
```
