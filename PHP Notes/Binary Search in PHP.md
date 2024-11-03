Binary search in very useful in a large number of array item like 1000 item or more. In the first round it will make the array half and search the value. Then the second round it will make the array again half and so on until the value is not found. That's actually make the search functionality more faster than loop through the 1000 or more than items.
Look at the example below
```php
<?php
function binarySearch($array, $element) {
    $start = 0;
    $end = count($array) - 1;

    while ($start <= $end) {
        $mid = floor(($start + $end) / 2);

        if ($element == $array[$mid]) {
            return $mid; // Found the element!
        } elseif ($element > $array[$mid]) {
            $start = $mid + 1; // Search in the right half
        } else {
            $end = $mid - 1; // Search in the left half
        }
    }

    return -1; // Element not found
}
```