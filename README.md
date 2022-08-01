# Public-Notes for Problem fixing
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
