# Deploy Laravel Projects to Cpanel which you don't have ssh access
first you should make a **.htaccess** file in your public_html or root folder
then you should put this codes :
```
<IfModule mod_rewrite.c>
    RewriteEngine On
    RewriteRule ^(.*)$ public/$1 [L]
</IfModule>
```
and if you want redirect any http to https protocol write this instead in .htaccess

```
<IfModule mod_rewrite.c>
    RewriteEngine On
    RewriteCond %{SERVER_PORT} 80
    RewriteRule ^(.*)$ https://[PUT_YOUR_DOMAIN_NAME_HERE].com/$1 [R,L]
    RewriteCond %{HTTP_HOST} ^www\.[PUT_YOUR_DOMAIN_NAME_HERE]\.com$
    RewriteRule ^/?$ "http\:\/[PUT_YOUR_DOMAIN_NAME_HERE]\.com\/" [R=301,L]
    RewriteRule ^(.*)$ public/$1 [L]
</IfModule>
```

and to create a symlink `php artisan storage:link` if you don't have ssh access
you should put this in your routes
and open in directly expample: domain.com/link

```
use Illuminate\Support\Facades\Artisan;
Route::get('/link', function () {
    Artisan::call('storage:link');
});
```

your storage folder has linked to the root storage folder (storage/app/public)
