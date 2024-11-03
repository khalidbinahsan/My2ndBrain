We need to follow some naming convention to create the Laravel migration file.
## Create a new table
```bash
php artisan make:migration create_tableName_table
```
## Rename table
```bash
php artisan make:migration rename_tableName_table
```
## Add a new column
```bash
php artisan make:migration add_columnName_to_tableName
```
## Update a column like rename column
```bash
php artisan make:migration update_columnName_to_tableName
```
## Remove a column
```bash
php artisan make:miration remove_columnName_from_tableName
```
## Drop a table
```bash
php artisan make:miration drop_tableName
```
## Example Code
#### Create a new table
 
```php
public function up(): void
    {
        Schema::create('profiles', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->string('phone');
            $table->string('city');
            $table->timestamp('created_at')->useCurrent();
            $table->timestamp('updated_at')->useCurrent()->useCurrentOnUpdate();
        });
    }

    /**
     * Reverse the migrations.
     */
public function down(): void
    {
        Schema::dropIfExists('profiles');
    }
```
#### Rename the table
```bash
public function up(): void
    {
        Schema::rename('profiles', 'new_profiles')
    }

```
#### Delete the table
```php
public function up(): void
    {
        Schema::dropIfExists('profiles');
    }
```
#### Add a new column to the table
```php
public function up(): void
    {
        Schema::table('profiles', function (Blueprint $table) {
            $table->after('name', function(Blueprint $table) {
                $table->string('gender');
                $table->string('address');
            });
        });
    }
```
#### Rename the column name
In the lower version of mysql database less than 8.0.3 we need to use a package for it is [doctrine](https://packagist.org/packages/doctrine/dbal) 
Use this command to install
```bash
composer require doctrine/dbal
```
Now write the function like
```php
public function up(): void
    {
        Schema::table('profiles', function (Blueprint $table) {
            $table->renameColumn('full_name', 'name');
        });
    }
```
#### Drop column from table
```php
public function up(): void
    {
        Schema::table('profiles', function (Blueprint $table) {
            $table->dropColumn('city');
        });
    }
```
## Table Relationship
```php
public function up(): void
    {
        Schema::create('profiles', function (Blueprint $table) {
            $table->id();
            $table->string('firstName', 50);
            $table->string('lastName', 50);
            $table->string('mobile', 50);
            $table->string('city', 50);
            $table->string('shippingAddress', 1000);
            $table->string('email', 50)->unique();
            
            // Relationship
            $table->foreign('email')->references('email')->on('users')
            ->restrictOnDelete()
            ->cascadeOnUpdate();
            
            $table->timestamp('created_at')->useCurrent();
            $table->timestamp('updated_at')->useCurrent()->useCurrentOnUpdate();
        });
    }
```
You can follow another approach to make the relationship
```php
$table->foreignId('user_id')->constrained()->cascadeOnDelete()->cascadeOnUpdate();
```
To create the many to many relationship you need to create another middle table called **pivot** table. In Laravel, a **pivot table** is an intermediary table used to manage the many-to-many relationships between two other tables. Since databases don’t allow direct many-to-many relationships, a pivot table helps **"link" two related tables** by storing their primary keys.
## ERD Diagram
To graph the database diagram here is the two most accurate tools
### 1. [Oracle SQL Developer](https://www.oracle.com/database/sqldeveloper/)
### 2. [dbForge](https://www.devart.com/dbforge/)
