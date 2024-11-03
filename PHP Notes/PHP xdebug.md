Download xdebug from here  [Download](https://xdebug.org/download/historical) Now go to the folder of **php -> ext** and copy the **xdebug.dll** file there.
Now get back and open **php.ini** file and go to the end of the file add the following code there
```
xdebug.mode=debug
xdebug.start_with_request=yes
xdebug.client_port=9003
xdebug.client_host = localhost
zend_extension="C:\xampp\php\ext\xdebug.dll"
```