# laravel8bug
> laravel新版本8出现了新的问题。

## 访问首页不存在
````
<IfModule mod_rewrite.c>
RewriteEngine on
RewriteCond %{REQUEST_FILENAME} !-d
RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule ^(.*)$ index.php/?$1 [QSA,PT,L]
</IfModule>
````

## 传统路由写法不行
app\Providers\RouteServiceProvider.php，搜寻nameprace取消注释即可。

