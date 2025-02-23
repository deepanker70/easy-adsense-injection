<?php
/*
Plugin Name: Easy Adsense Injection
Version: 3.0
Plugin URI: https://thewpguides.com/
Author: Deepanker
Author URI: https://deepankerverma.com
Description: A simple Wordpress plugin to inject Google Adsense Ads into posts, pages, sidebars or any other part of theme. 
License: GPLv3
*/

if (!defined('ABSPATH')) {
    exit; // Prevent direct access
}

$easy_ad_injection_version = 30;

// Function to inject ads manually
function adscript($num) {
    $ad_value = get_option("easy_ad_code_{$num}");
    
    if ($ad_value) {
        echo "<div class='put_wp_ad_{$num}'>" . $ad_value . "</div>";
    }
}

// Function to generate ad shortcodes for manual placement
function put_wp_ad($num) {
    return get_option("easy_ad_code_{$num}", '');
}

for ($i = 1; $i <= 5; $i++) {
    add_shortcode("easy_ad_inject_{$i}", function() use ($i) { return put_wp_ad($i); });
}

// Function to insert ads automatically
function auto_insert_ads($content) {
    if (is_single()) {
        $ad_below_title = get_option("easy_ad_below_title");
        $ad_below_content = get_option("easy_ad_below_content");
        $ad_inbetween = get_option("easy_ad_inbetween");
        $paragraph_position = get_option("easy_ad_paragraph_position", 3);

        if ($ad_below_title) {
            $content = $ad_below_title . $content;
        }
        if ($ad_inbetween) {
            $paragraphs = explode('</p>', $content);
            if (count($paragraphs) > $paragraph_position) {
                array_splice($paragraphs, $paragraph_position, 0, $ad_inbetween);
                $content = implode('</p>', $paragraphs);
            }
        }
        if ($ad_below_content) {
            $content .= $ad_below_content;
        }

    }
    return $content;
}
add_filter('the_content', 'auto_insert_ads');

// Function to inject ads above header and below footer
function insert_ad_above_header() {
    $ad_above_header = get_option("easy_ad_above_header");
    if ($ad_above_header) {
        echo $ad_above_header;
    }
}
add_action('wp_head', 'insert_ad_above_header');

function insert_ad_below_footer() {
    $ad_below_footer = get_option("easy_ad_below_footer");
    if ($ad_below_footer) {
        echo $ad_below_footer;
    }
}
add_action('wp_footer', 'insert_ad_below_footer');

// Admin options page
function ad_camp_add_option_page() {
    if (function_exists('add_options_page')) {
        add_options_page('Easy Ad Injection', 'Easy Ad Injection', 'manage_options', 'easy_ad_injection', 'ad_insertion_options_page');
    }
}
add_action('admin_menu', 'ad_camp_add_option_page');

function ad_insertion_options_page() {
    if (isset($_POST['info_update']) && check_admin_referer('easy_ads_update_options')) {
        echo '<div id="message" class="updated fade"><p><strong>Options Updated!</strong></p></div>';
        for ($i = 1; $i <= 5; $i++) {
            $ad_code = isset($_POST["easy_ad_code_{$i}"]) ? wp_unslash($_POST["easy_ad_code_{$i}"]) : '';
            update_option("easy_ad_code_{$i}", $ad_code);  
        }
        update_option("easy_ad_below_title", wp_unslash($_POST["ad_below_title"] ?? ''));
        update_option("easy_ad_below_content", wp_unslash($_POST["ad_below_content"] ?? ''));
        update_option("easy_ad_above_header", wp_unslash($_POST["ad_above_header"] ?? ''));
        update_option("easy_ad_below_footer", wp_unslash($_POST["ad_below_footer"] ?? ''));
        update_option("easy_ad_inbetween", wp_unslash($_POST["ad_inbetween"] ?? ''));
        update_option("easy_ad_paragraph_position", intval($_POST["ad_paragraph_position"] ?? 3));
    }
    ?>
    <div class="wrap">
        <h2>Easy Ad Injection Options</h2>
        <p>Use this plugin to inject ads manually or automatically.</p>
        <style>
            .nav-tab-wrapper { margin-bottom: 20px; }
            .tab-content { display: none; padding: 20px; background: #fff; border: 1px solid #ddd; }
            .tab-content.active { display: block; }
            .form-table th { width: 200px; }
            textarea { width: 100%; height: 100px; }
            .button-primary { margin-top: 10px; }
        </style>
        <script>
            document.addEventListener('DOMContentLoaded', function() {
                var tabs = document.querySelectorAll('.nav-tab');
                var contents = document.querySelectorAll('.tab-content');
                tabs.forEach(tab => {
                    tab.addEventListener('click', function(e) {
                        e.preventDefault();
                        tabs.forEach(t => t.classList.remove('nav-tab-active'));
                        contents.forEach(c => c.classList.remove('active'));
                        this.classList.add('nav-tab-active');
                        document.querySelector(this.getAttribute('href')).classList.add('active');
                    });
                });
                document.querySelector('.nav-tab-active').click();
            });
        </script>
        <h2 class="nav-tab-wrapper">
            <a href="#manual_ads" class="nav-tab nav-tab-active">Manual Ad Placement</a>
            <a href="#auto_ads" class="nav-tab">Automatic Ad Placement</a>
        </h2>
        <form method="post" action="">
            <?php wp_nonce_field('easy_ads_update_options'); ?>
            <div id="manual_ads" class="tab-content active">
                <table class="form-table">
                    <?php for ($i = 1; $i <= 5; $i++) : ?>
                        <tr>
                            <th>Ad Code <?php echo $i; ?>:</th>
                            <td><textarea name="easy_ad_code_<?php echo $i; ?>" rows="6" cols="50"><?php echo esc_textarea(get_option("easy_ad_code_{$i}")); ?></textarea>
                                <br>Use shortcode: <code>[easy_ad_inject_<?php echo $i; ?>]</code>
                                <br>Or use function: <code>put_wp_ad(<?php echo $i; ?>);</code>
                            </td>
                        </tr>
                    <?php endfor; ?>
                </table>
            </div>
            <div id="auto_ads" class="tab-content">
                    <table class="form-table">
                    <tr><th>Ad Above Website Header:</th><td><textarea name="ad_above_header" rows="6" cols="50"><?php echo esc_textarea(get_option("easy_ad_above_header")); ?></textarea></td></tr>
                    <tr><th>Ad Below Article Title:</th><td><textarea name="ad_below_title" rows="6" cols="50"><?php echo esc_textarea(get_option("easy_ad_below_title")); ?></textarea></td></tr>
                    <tr><th>Ad Inbetween Article Content:</th><td><textarea name="ad_inbetween" rows="6" cols="50"><?php echo esc_textarea(get_option("easy_ad_inbetween")); ?></textarea><br>Insert after <input type="number" name="ad_paragraph_position" value="<?php echo esc_attr(get_option("easy_ad_paragraph_position", 3)); ?>" min="1"></td></tr>
                    <tr><th>Ad Below Article Content:</th><td><textarea name="ad_below_content" rows="6" cols="50"><?php echo esc_textarea(get_option("easy_ad_below_content")); ?></textarea></td></tr>
                    <tr><th>Ad Below Website Footer:</th><td><textarea name="ad_below_footer" rows="6" cols="50"><?php echo esc_textarea(get_option("easy_ad_below_footer")); ?></textarea></td></tr>
                </table>
            </div>
            <p><input type="submit" name="info_update" value="Save Changes" class="button-primary"></p>
        </form>
    </div>
    <?php
}

// Allow shortcodes in widgets and excerpts
add_filter('widget_text', 'do_shortcode');
add_filter('the_excerpt', 'do_shortcode');
