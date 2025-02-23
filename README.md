# Easy Adsense Injection Plugin

![License](https://img.shields.io/badge/license-GPLv3-blue.svg)

## Description

Easy Adsense Injection is a WordPress plugin that allows users to easily insert Google Adsense into posts or any part of the WordPress theme. The plugin supports both manual and automatic ad placement, ensuring seamless ad integration with minimal effort.

## Features

### **Automatic Ad Placement:**
The plugin supports automatic ad placement in the following areas:
- Above the header
- Below the post title
- Between paragraphs (configurable after how many paragraphs)
- Below the post content
- Below the footer

### **Manual Ad Placement:**

#### **Shortcodes for Ad Placement in Posts**
Use these shortcodes within your post content:

```
[easy_ad_inject_1]
[easy_ad_inject_2]
[easy_ad_inject_3]
[easy_ad_inject_4]
[easy_ad_inject_5]
```

#### **PHP Functions for Theme Integration**
Use these functions within your WordPress theme to insert ads programmatically:

```php
<?php echo put_wp_ad_1(); ?>
<?php echo put_wp_ad_2(); ?>
<?php echo put_wp_ad_3(); ?>
<?php echo put_wp_ad_4(); ?>
<?php echo put_wp_ad_5(); ?>
```

## Installation

1. Download and unzip the plugin in the `wp-content/plugins` folder or install it directly from the WordPress dashboard.
2. Activate the plugin from the WordPress admin panel.
3. Navigate to the plugin settings page.
4. Enter your Google Adsense code and configure the ad placement options.

## Screenshots

_No screenshots available._

## Changelog

### Version 3.0
- Added automatic ad placement for seamless integration.
- Removed the alternate ads option for users using an ad blocker.

## License

This plugin is licensed under the GPLv3 License. For more details, see [GPL-3.0 License](https://www.gnu.org/licenses/gpl-3.0.html).

## Contributors

- [Deepanker Verma](https://thewpguides.com/)

## Support & Donations

If you find this plugin helpful, consider donating at [The WP Guides](https://thewpguides.com/).