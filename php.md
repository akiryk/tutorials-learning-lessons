# PHP

### Create a new array
```php
// empty
$this->listOfStuff = [];

// with content
  $this->header = [
      'title' => $this->translate->trans('transId.someId'),
      'actionText' => $this->translate->trans('transId.otherId'),
      'actionUrl' => My_Helpers::SOME_URL
    ];
```

### Loops
```php
// an array
$this->categoryList = [];

// count and sizeof are the same thing
for($i = 0; $i < count($categoryIds); $i++) {
    $category = $storefront->get_category($categoryIds[$i]);
    $this->categoryList[] = [
      'name' => $category->get_name(),
      'imageId' => $category->get_image_id(),
      'link' => $category->get_category_url(),
      'itemsPurchased' => count($category->get_completed_child_categories()),
      'itemsRequired' => count($category->get_child_categories()),
      ];
    }
    
// foreach is a specially-designed loop for arrays
for ($myArray as $itemInArray) {
   echo $itemInArray;
}

// with a key value array
foreach($keyvals as $key => $val){
  echo "<li>$key is $val</li>";
}
```

### Useful operators
#### Spaceship operator
Return `-1` if the first value is less than the second;
return `0` if they are equal
return `1` if the first is greater
```php 
// $val = 1
$val = 5 <=>3;
```

#### Null Coalescing Operator
Return the first value if it exists and is not null. Otherwise return the second value.
```php
$val = $someUnknownValue ?? 'default';
```

### Built in functions
You can sort arrays
```php
  usort($names, function($a, $b) {
    return [$a->get_first(), $a->get_last()] <=> [$b->get_first(), $b->get_last()];
  });
```

#### Mock Error
```php
// pretend some endpoint fails
throw new \Exception('my error!');
```
