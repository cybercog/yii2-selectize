Selectize Widget for Yii 2
=========
- Widget based on selectize.js extension http://brianreavis.github.io/selectize.js/

Installation 
------------

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```
php composer.phar require --prefer-dist yii2mod/selectize "*"
```

or add

```json
"yii2mod/selectize": "*"
```

to the require section of your composer.json.

Usage
------------
Once the extension is installed, simply add widget to your page as follows:

1) Tagging input:
```php
echo $form->field($model, "attribute")->widget(Selectize::className(), [
        'pluginOptions' => [
            'persist' => false,
            'createOnBlur' => true,
            'create' => true
        ]
]); 
```
2) Select input:
```php
echo $form->field($model, "attribute")->widget(Selectize::className(), [
        'items' => [
            'Yes',
            'No'
        ],
        'pluginOptions' => [
            'persist' => false,
            'createOnBlur' => true,
            'create' => true
        ]
]); 
```

3) Tagging input with remote source and default values(If you want render select input, just setup items property):

- Setup view file:
 
```php
// setup the following to get the existing data from database
$model->attribute = 'first, last';
 
// or if the data is an array you can preselect the tags like this
$model->attribute = implode(', ', ["first", "last"]);

echo $form->field($model, "attribute")->widget(Selectize::className(), [
         'url' => '/site/search',
         'pluginOptions' => [
            'valueField' => 'name',
            'labelField' => 'name',
            'searchField' => ['name'],
            'persist' => false,
            'createOnBlur' => true,
            'create' => true
        ]
]);
 ```

- Your action must return data in json format, example:

```php
  public function actionSearch($query = null)
     {
         Yii::$app->response->format = Response::FORMAT_JSON;
         return [
             ['name' => 'Search Item 1'],
             ['name' => 'Search Item 2'],
         ];
     }
```

Select Options 
----------------
You can find them on the [options page](https://github.com/brianreavis/selectize.js/blob/master/docs/api.md)