## $table->cascadeOnUpdate()
cascadeOnUpdate means if we update any data on the database, all other data in the related table should be update at the same time.
## $table->restrictOnUpdate()
restrictOnUpdate means you should update the child table data first, then you can update the parent table data
## $table->cascadeOnDelete()
cascadeOnDelete means if we delete any data on the database, all other data in the related table should be delete at the same time.
## $table->restrictOnDelete()
restrictOnDelete means you should delete the child table data first, then you can delete the parent data.
## $table->nullOnDelete()
nullOnDelete means when the data will be delete, the child table data will be null instead of delete the table row

Look at the example bellow how to use that in a foreign key
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
            $table->timestamps();
        });
    }
```