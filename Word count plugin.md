```php
<?php

/*
Plugin Name: Custom Bishal
Description: A test plugin for demo purpose
Version: 1.0.0
Author: Bishal
Author URI: https://google.com
*/

class WordCountPlugin
{
    function __construct()
    {
        add_action('admin_menu', array($this, 'settingsLink'));
        add_action('admin_init', array($this, 'settings'));
    }


    //configuration of the plugin settings
    function settings()
    {
        add_settings_section('wcp_location_section', null, null, 'word-count-settings');

        // location setings

        add_settings_field('wcp_location', "Display Location", array($this, 'locationHtml'), 'word-count-settings', 'wcp_location_section');
        register_setting('wordCountPlugin', 'wcp_location', array('sanitize_callback' => 'sanitize_text_field', "default" => '0'));


        //.custom title
        add_settings_field('wcp_custom_text', "Custom header", array($this, 'customHeaderHtml'), 'word-count-settings', 'wcp_location_section');
        register_setting('wordCountPlugin', 'wcp_custom_text', array('sanitize_callback' => 'sanitize_text_field', "default" => ''));


        //show word count
        add_settings_field('wcp_show_word_count', "Show word count", array($this, 'showWordCountCheckbox'), 'word-count-settings', 'wcp_location_section');
        register_setting('wordCountPlugin', 'wcp_show_word_count', array('sanitize_callback' => 'sanitize_text_field', "default" => '1'));
    }


    //location html code;
    function locationHtml()
    {
?>
        <select name="wcp_location">
            <option value="0" <?php selected(get_option('wcp_location', '0')); ?>>Display on top</option>
            <option value="1" <?php selected(get_option('wcp_location', '1')); ?>>Display at the bottom</option>
        </select>
    <?php
    }

    //Custom heading title html
    function customHeaderHtml()
    {
    ?>
        <input placeholder="Your custom title" name="wcp_custom_text" value="<?php echo (get_option('wcp_custom_text', '')); ?>" />
    <?php
    }

    //Custom heading title html
    function showWordCountCheckbox()
    {
    ?>
        <input type="checkbox" name="wcp_show_word_count" <?php get_option(('wcp_show_word_count') === '1'); ?> />
    <?php
    }

    //registers settings item to admin dashboard
    function settingsLink()
    {
        add_options_page('Word count settings', 'Word Count', 'manage_options', 'word-count-settings', array($this, 'pluginHtml'));
    }

    function pluginHtml()
    {
    ?>
        <div class="wrap">
            <h1>Word Count settings</h1>
            <form action="options.php" method="POST">
                <?php
                settings_fields('wordCountPlugin');
                do_settings_sections('word-count-settings');
                submit_button();
                ?>
            </form>
        </div>
<?php
    }
}

$wordCount = new WordCountPlugin();
```
