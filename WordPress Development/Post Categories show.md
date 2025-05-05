Put this code into your **functions.php**
```php
function display_all_post_categories() {
    $categories = get_categories();
    
    if ($categories) {
        $output = '<ul class="post-categories">';
        
        foreach ($categories as $category) {
            $output .= '<li><a href="' . get_category_link($category->term_id) . '">' . $category->name . '</a></li>';
        }
        
        $output .= '</ul>';
        
        return $output;
    } else {
        return 'No categories found';
    }
}
add_shortcode('all_post_categories', 'display_all_post_categories');
```
Here is some **CSS**
```css
ul{
padding: 0;
}
li{
list-style: none;
}
.post-categories{
	font-family: Teko;
	font-size: 1.3rem;
}
.post-categories li{
	border-bottom: 1px solid #dbdbdb;
	padding: 5px 0;
}
.post-categories li a {
	color: black !important;
	letter-spacing: 0.5px;
}
.post-categories li a:hover{
	color: #AF2724 !important;
}
```