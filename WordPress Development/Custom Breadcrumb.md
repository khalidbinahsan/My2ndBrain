Here is the code example to create a custom Breadcrumb shortcode
```php
function custom_breadcrumbs() {
    // Get the current post/page ID
    $post_id = get_the_ID();

    // Initialize the breadcrumbs variable
    $breadcrumbs = '<div class="breadcrumbs">';

    // Add a Home link
    $breadcrumbs .= '<a href="' . home_url() . '">Home</a>';

    // Check if the current page is a single post
    if (is_singular('post')) {
        // Get the category of the post
        $category = get_the_category();
        if ($category) {
            $category_link = get_category_link($category[0]->term_id);
            $breadcrumbs .= ' / <a href="' . esc_url($category_link) . '">' . $category[0]->name . '</a>';
        }
        $breadcrumbs .= ' / ' . get_the_title();
    } elseif (is_singular('page')) {
        // Get the parent pages
        $ancestors = get_post_ancestors($post_id);
        if ($ancestors) {
            $ancestors = array_reverse($ancestors);
            foreach ($ancestors as $ancestor) {
                $breadcrumbs .= ' / <a href="' . get_permalink($ancestor) . '">' . get_the_title($ancestor) . '</a>';
            }
        }
        $breadcrumbs .= ' / ' . get_the_title();
    } elseif (is_category()) {
        // Get the current category
        $category = get_queried_object();
        $breadcrumbs .= ' / ' . $category->name;
    } elseif (is_tag()) {
        // Get the current tag
        $tag = get_queried_object();
        $breadcrumbs .= ' / ' . $tag->name;
    } elseif (is_author()) {
        // Get the current author
        $author = get_queried_object();
        $breadcrumbs .= ' / Author: ' . $author->display_name;
    } elseif (is_search()) {
        // Display search query
        $breadcrumbs .= ' / Search results for: ' . get_search_query();
    } elseif (is_404()) {
        // Display 404 error message
        $breadcrumbs .= ' / Error 404';
    } elseif (is_archive()) {
        // Display archive title
        $breadcrumbs .= ' / ' . get_the_archive_title();
    }

    // Close the breadcrumbs div
    $breadcrumbs .= '</div>';

    // Return the breadcrumbs
    return $breadcrumbs;
}
add_shortcode('breadcrumbs', 'custom_breadcrumbs');

```