# Public-Notes for problem fixing - related to WordPress and Tools
Public Notes for everyone and me to remember how Problems are solved

## webvizio.com and WordPress Problem fixing
1. On your hosting service provider or service Panel (GridPane.com) disable the clickjacking protection
2. Install the plugin https://github.com/PHPWatch/WordPress-SameSite
(Click on the green code button, download as Zip, upload as Plugin)
3. add these lines to the functions.php
```
remove_action( 'login_init', 'send_frame_options_header' );
remove_action( 'admin_init', 'send_frame_options_header' );
``` 
4. add this to wp-config.php
```
define('WP_SAMESITE_COOKIE', 'None' );
```

This above 
- Allows you to display the site with the login page and the administrative panel in a frame
- Give opportunity to use all cookies including session cookies in iframes.
If third parties do not know your admin area passwords, the only security problem is displaying your pages in a iframe, but they are protected by login + Wordpress by default allows you to display the site pages in iframe

## Brizy Pro + WooCommerce throwing 404 Error on 2nd Categorie Page
Just go to Settings > Permalinks and hit save. You might need to purge the cache as well.

## LiteSpeed 
### LiteSpeed WordPress Optimizations
Make Litespeed UCSS work, complete process and tools to use
https://www.youtube.com/watch?v=kSC2sKb-K2k

### Cookie Problems - 
#### Do Not Cache PayPal Cookies
It will make you Cache be missed
```
sc_f
c
```

#### Do not cache the Cart Hash Cookie, vary the cookie of the current language of WPML and the current currency
```
woocommerce_cart_hash
```
Try to add these lines to your .htaccess file

```
<IfModule LiteSpeed>
RewriteEngine On 
RewriteRule .* - [E=Cache-Vary:woocommerce_current_currency]
RewriteRule .* - [E=Cache-Vary:wp-wpml_current_language]
</IfModule>
```

#### Cookies Others
https://github.com/WpSpeedDoctor/litespeed-cookie-based-caching
https://www.youtube.com/watch?v=cJeZv3tG-FU

### WP-Cron Problems
Sometimes WP-Con Jobs won't trigger on (Open)LiteSpeed Servers. Here's how to fix this:
"Do Not Cache Query Strings" from /wp-admin/admin.php?page=litespeed-cache#excludes this 
`doing_wp_cron`
and disable "Cache WP-Admin" /wp-admin/admin.php?page=litespeed-cache#object

## WordPress Maintenance, Monitoring and Checkup
- https://de.wordpress.org/plugins/system-dashboard/
- https://wordpress.org/plugins/wp-healthcheck/
- https://de.wordpress.org/plugins/wp-server-stats/ - Warning - Adds a lot of Autoload

## WordPress Pagespeed Optimization
- https://wordpress.org/plugins/pre-party-browser-hints/ - Pre-Load/Connect Assets. Attention: May Break your headers in LiteSpeed, check on testsite first!
- https://wordpress.org/plugins/docket-cache/ - An Object Cache Accelerator
- https://wordpress.org/plugins/freesoul-deactivate-plugins/ - Deactivates Plugins based on sites instead of unloading CSS/JS |  Free/Paid
- https://wordpress.org/plugins/plugin-organizer/ - Deactivates Plugins based on sites instead of unloading CSS/JS Free
- https://wordpress.org/plugins/index-wp-mysql-for-speed/ && https://github.com/OllieJones/index-wp-mysql-for-speed - Adds Indexes to your DB to improve speed
- https://wordpress.org/plugins/index-wp-users-for-speed/ - Companion Plugin for Index WP MySQL for Speed
- https://wordpress.org/plugins/wc-speed-drain-repair/ - Unloads WooCommerce Components where they are not needed

## WP-Cron helpers
- https://github.com/nawawi/docket-cronwp
- https://wordpress.org/plugins/migrate-wp-cron-to-action-scheduler/

## GridPane.com helpers
- https://github.com/managingwp/gp-tools
- https://github.com/managingwp/cache-purge-helper

