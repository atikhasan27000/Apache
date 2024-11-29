# `.htaccess` Configuration Guide

This `.htaccess` file is configured to handle several key functionalities, including HTTPS redirection, removing `.php` extensions from URLs, restricting access to `.php` files directly, and specifying the PHP version to be used.

## Features

1. **Redirect HTTP to HTTPS**  
   Ensures all HTTP traffic is redirected to HTTPS for secure browsing.

2. **Remove `.php` Extension from URLs**  
   Allows pages to be accessed without specifying the `.php` extension, improving SEO and user-friendliness.

3. **Restrict Direct Access to `.php` Files**  
   Prevents direct access to `.php` files in URLs, returning a 404 error if attempted.

4. **Specify PHP Version**  
   Configures the server to use a specific version of PHP (`PHP 7.4` in this case).

---

## File Breakdown

### 1. Redirect HTTP to HTTPS
````apache
RewriteEngine on
RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
````
* Redirects all HTTP requests to their HTTPS equivalent.

### 2. Remove `.php` Extensions
````apache
RewriteCond %{REQUEST_FILENAME} !-d
RewriteCond %{REQUEST_FILENAME}\.php -f
RewriteRule ^([^\.]+)$ $1.php [NC,L]
````
* Maps requests without an extension to `.php` files while hiding the `.php` extension.

### 3. Restrict .php Access
````apache
RewriteCond %{THE_REQUEST} "\.php"
RewriteRule ^ - [L,R=404]
````
* Denies access to URLs explicitly containing `.php` in the request.

### 4. Specify PHP Version
````apache
<IfModule mime_module>
    AddHandler application/x-httpd-ea-php74 .php .php7 .phtml
</IfModule>
````
* Configures the server to use PHP 7.4. Adjust this as needed for your environment.

## Usage
1. Place the `.htaccess` file in the root directory of your web application.
2. Ensure your server has `mod_rewrite` enabled.
3. Adjust the PHP handler if necessary, depending on your hosting environment.
4. Test the configuration to ensure proper functionality.

## Compatibility
* Server Requirements: Apache with `mod_rewrite` and `mime_module` enabled.
* Tested PHP Versions: PHP 7.4 (adjustable in the file).
