# Public-Notes for problem fixing - related to WordPress and Tools
Public Notes for everyone and me to remember how Problems are solved

## webvizio.com and WordPress Problem fixing
1. On your hosting service provider or service Panel (GridPane.com) disable the clickjacking protection
2. Install the plugin https://github.com/PHPWatch/WordPress-SameSite
(Click on the green code button, download as Zip, upload as Plugin)
3. add these lines to the functions.php
  - remove_action( 'login_init', 'send_frame_options_header' );
  - remove_action( 'admin_init', 'send_frame_options_header' );
4. add this to wp-config.php
define('WP_SAMESITE_COOKIE', 'None' );

This above 
- Allows you to display the site with the login page and the administrative panel in a frame
- Give opportunity to use all cookies including session cookies in iframes.
If third parties do not know your admin area passwords, the only security problem is displaying your pages in a iframe, but they are protected by login + Wordpress by default allows you to display the site pages in iframe

## Brizy Pro + WooCommerce throwing 404 Error on 2nd Categorie Page
Just go to Settings > Permalinks and hit save. You might need to purge the cache as well.

## LiteSpeed 
### Cookie Problems - 
#### Do Not Cache PayPal Cookies
It will make you Cache be missed
- sc_f
- c

#### Do not cache the Cart Hash and the current language of WPML
- woocommerce_cart_hash
- wp-wpml_current_language

## WordPress Maintenance, Monitoring and Checkup
- https://de.wordpress.org/plugins/system-dashboard/
- https://wordpress.org/plugins/wp-healthcheck/

## WordPress Pagespeed Optimization
- https://wordpress.org/plugins/pre-party-browser-hints/ - Pre-Load/Connect Assets
- https://wordpress.org/plugins/docket-cache/ - An Object Cache Accelerator

## GridPane.com helpers
- https://github.com/managingwp/gp-tools

