```php
function create_ostad_role() {
    // Get administrator capabilities
    $admin_role = get_role('administrator');
    
    // Add new role 'Ostad' with administrator capabilities
    add_role('ostad', 'Ostad', $admin_role->capabilities);
}
add_action('init', 'create_ostad_role');
```