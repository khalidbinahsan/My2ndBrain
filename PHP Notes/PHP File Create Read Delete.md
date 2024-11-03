## File Create
First of all you need to create a file format with the function **fopen()**  than you can create the file with **fwrite** function. Look at the example below
```php
<?php
// Way 1
$file = fopen("data2.txt", "a");
$data = "Hello from Khalid".PHP_EOL;
fwrite($file, $data);
fclose($file);

// Way 2
$books = [
    "Book 1",
    "Book 2",
    "Book 3",
    "Book 4"
];
$createFile = fopen("book3.txt", "w");
foreach($books as $book){
    fwrite($createFile, $book.PHP_EOL);
}

// Way 3

// heredoc syntax
$books = <<<EOD
Book 1
Book 2
Book 3
EOD;
file_put_contents("books4.txt", $books);
echo "Done";

// To Append new data you can follow this
$books = <<<EOD
Book 4
Book 5
Book 6
EOD;
file_put_contents("books4.txt", $books, FILE_APPEND);
echo "Data Appened";
```

## File Read
You need to open the file first with the function **fopen()** than you can read it with the different way. The file format should be **r** here

```php
$file = fopen("book.txt", "r");

// way 1
while(!feof($file)){ //feof is for go to the last of the file
    echo fgets($file);
};

// way 2
$file2 = file("book.txt");
foreach($file2 as $file){
    echo $file.PHP_EOL;
};

// way 3 popular way
$content = file_get_contents("books.txt");
echo $content;

```
## File Delete
```php
<?php
$exists = file_exists("unwanted.txt");
if($exists){
    unlink("unwanted.txt");
}
```
## File find
You can find the file form current directory with it's extension.
```php
<?php
$csvFile = glob("*.php");
print_r($csvFile);
```