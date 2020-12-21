# PHP

#### Create a new array
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

#### Loops
```php
// an array
$this->categoryList = [];

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
```

#### Mock Error
```php
// pretend some endpoint fails
throw new \Exception('my error!');
```
