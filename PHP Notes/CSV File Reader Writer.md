## CSV (Comma Separated Value) file read

#### Way 1
We need a package named **league/csv** to read the csv file. Run this command to install league/csv
```shell
 composer require league/csv
```
Now you can  read the file this way
```php
<?php
include "vendor/autoload.php"; // need to write every time when you use any package
use League\Csv\Reader;

$reader = Reader::createFromPath("books.csv", "r");
$books = $reader->getRecords();
foreach($books as $book){
    $output = "Book Name: $book[0], Author: $book[1]".PHP_EOL;
    echo $output;
}

```
 If you have a the Header in your CSV file, you can get it by the header name instead of the index number.
```php
 <?php
include "vendor/autoload.php";
use League\Csv\Reader;
$reader = Reader::createFromPath("books.csv", "r");
$reader->setHeaderOffset(0); // Set the first line as header
$books = $reader->getRecords();

foreach($books as $book){
    $output = "Book Name:". $book['Title'].", Author:". $book['Author'].PHP_EOL;
    echo $output;
}
```
#### Way 2
This the second way to read the csv file if you don't want to use any PHP package
```php
$file = new SplFileObject("books.csv"); // need to create a object first
$file->setFlags(SplFileObject::READ_CSV); // Treat the file as csv format
$file->setCsvControl(",");
foreach($file as $row){
    $output = "Book Name: $row[0], Author: $row[1]".PHP_EOL;
    echo $output;
}
```
#### Way 3
```php
$file = fopen("books4.csv", "r");
while($line = fgetcsv($file)){
    print_r($line);
}
```
## CSV (Comma Separated Value) file write
#### Way 1
```php
<?php
$books = [
    ["Book 1", "Author 1", 34],
	["Book 2", "Author 2", 36],
    ["Book 3", "Author 3", 37],
    ["Book 4", "Author 4", 24]
];
$_books = [];
foreach($books as $book){
    $line = implode(", ", $book);
    $_books[] = $line;
}
$data = implode(PHP_EOL, $_books);
file_put_contents("book3.csv", $data);
```
#### Way 2
```php
<?php
$books = [
    ["Book 1", "Author 1", 34],
	["Book 2", "Author 2", 36],
    ["Book 3", "Author 3", 37],
    ["Book 4", "Author 4", 24]
];
$file = fopen("books4.csv", "w");
foreach($books as $book) {
    fputcsv($file, $book);
}
```
