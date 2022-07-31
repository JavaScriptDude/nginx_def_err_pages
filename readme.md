NGINX has built-in error pages that contain the block `<hr><center>nginx/_version_</center>` in the output. This may not be desirable. This template is to set up new default error pages for all error codes that are not caught and handled by the 'servers'.

1) Create directory for static error pages: `/var/www/error`
    * Ensure that nginx has read access
  
2) Upload <err_num>.html files to /var/www/error
    * See var/www/error in this repo for templates -or- use http_codes.ods to create your own

3) Create /etc/nginx/common (if not existing)

4) Create `error.conf` in `/etc/nginx/common` with contents:=
```
error_page 400 /400.html;
error_page 401 /401.html;
error_page 402 /402.html;
error_page 403 /403.html;
error_page 404 /404.html;
error_page 405 /405.html;
error_page 406 /406.html;
error_page 407 /407.html;
error_page 408 /408.html;
error_page 409 /409.html;
error_page 410 /410.html;
error_page 411 /411.html;
error_page 412 /412.html;
error_page 413 /413.html;
error_page 414 /414.html;
error_page 415 /415.html;
error_page 416 /416.html;
error_page 417 /417.html;
error_page 418 /418.html;
error_page 421 /421.html;
error_page 422 /422.html;
error_page 423 /423.html;
error_page 424 /424.html;
error_page 425 /425.html;
error_page 426 /426.html;
error_page 428 /428.html;
error_page 429 /429.html;
error_page 431 /431.html;
error_page 451 /451.html;
error_page 500 /500.html;
error_page 501 /501.html;
error_page 502 /502.html;
error_page 503 /503.html;
error_page 504 /504.html;
error_page 505 /505.html;
error_page 506 /506.html;
error_page 507 /507.html;
error_page 508 /508.html;
error_page 510 /510.html;
error_page 511 /511.html;

location ~ /*.html {
        try_files $1.html @error;
        internal;
}

location @error {
    root /var/www/error;
}
```

5) Add directive to in top of each of your `server` block `include common/error.conf;`

6) test by using location like (change code to see different error pages:
```
    location / {
        return 502;
    }
```

You can create your own tempaltes using the provided spreadsheet `http_codes.ods`.
  
