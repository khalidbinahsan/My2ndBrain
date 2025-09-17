Add to the `functions.php`
```php
function project_navigation_shortcode() {
    ob_start();
    $prev_post = get_adjacent_post(false, '', true);
    $next_post = get_adjacent_post(false, '', false);
    ?>
    <div class="project-navigation">
        <?php if ($prev_post) : ?>
            <div class="prev-project">
                <a href="<?php echo get_permalink($prev_post->ID); ?>">
                    <span class="arrow-box prev-arrow">‹</span>
                    <div class="nav-content">
                        <span class="nav-label">Previous Project</span>
                        <h3 class="nav-title"><?php echo get_the_title($prev_post->ID); ?></h3>
                    </div>
                </a>
            </div>
        <?php endif; ?>

        <?php if ($next_post) : ?>
            <div class="next-project">
                <a href="<?php echo get_permalink($next_post->ID); ?>">
                    <div class="nav-content">
                        <span class="nav-label">Next Project</span>
                        <h3 class="nav-title"><?php echo get_the_title($next_post->ID); ?></h3>
                    </div>
                    <span class="arrow-box next-arrow">›</span>
                </a>
            </div>
        <?php endif; ?>
    </div>
    <?php
    return ob_get_clean();
}
add_shortcode('project_navigation', 'project_navigation_shortcode');

```
Here is some css code
```css
/* ============= Previous & Next Post ========== */
.project-navigation {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 50px 0;
    border-top: 1px solid #eee;
    padding-top: 20px;
}

.project-navigation a {
    display: flex;
    align-items: center;
    text-decoration: none;
    color: #0A1C54; /* dark blue */
}

.prev-project .nav-content,
.next-project .nav-content {
    display: flex;
    flex-direction: column;
    margin: 0 10px;
}

.nav-label {
    font-size: 14px;
    color: #777;
}

.nav-title {
    font-size: 18px !important;
    font-weight: bold;
    color: #0A1C54;
}

.arrow-box {
    background: #f0f2f9;
    color: #0A1C54;
    font-size: 22px;
    padding: 12px 16px;
    border-radius: 8px;
    font-weight: bold;
}
.arrow-box:hover{
	background: #3454ff;
  color: #fff;
}
.next-arrow {
    margin-left: 10px;
}
@media (max-width: 767px){
	.project-navigation{
		flex-direction: column;
		gap: 20px;
	}
	.prev-project{
		align-self: start;
	}
	.next-project{
		align-self: end;
	}
}
```