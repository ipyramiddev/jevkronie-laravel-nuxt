# Laravel-Nuxt

<a href="https://travis-ci.org/cretueusebiu/laravel-nuxt"><img src="https://travis-ci.org/cretueusebiu/laravel-nuxt.svg?branch=master" alt="Build Status"></a>
<a href="https://packagist.org/packages/cretueusebiu/laravel-nuxt"><img src="https://poser.pugx.org/cretueusebiu/laravel-nuxt/d/total.svg" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/cretueusebiu/laravel-nuxt"><img src="https://poser.pugx.org/cretueusebiu/laravel-nuxt/v/stable.svg" alt="Latest Stable Version"></a>

> A Laravel-Nuxt starter project template.

<p align="center">
<img src="https://i.imgur.com/NHFTsGt.png">
</p>

## Features

- Laravel 5.6
- Nuxt 2.7
- VueI18n
- SPA or SSR 
- Authentication with JWT
- Socialite integration
- Bootstrap 4 + Font Awesome 5
- Login, register, password reset and profile pages

## Installation

- `composer create-project --prefer-dist cretueusebiu/laravel-nuxt`
- Edit `.env` to set your database connection details and `APP_URL` (the url to your Laravel application)
- (When installed via git clone or download, run `php artisan key:generate` and `php artisan jwt:secret`)
- `php artisan migrate`
- `npm install`

## Usage

### Development

```bash
npm run dev
```

### Production with SSR

If you want to enable server side rendering follow the next steps:

- Remove `mode: 'spa'` and `'~plugins/nuxt-client-init'` from `client/nuxt.config.js` 
- Add `API_URL=http://api.example.com/api` and `CLIENT_URL=http://example.com` in your `.env`
- Run `npm run build` and `npm run start`

Make sure to read the [Nuxt docs](https://nuxtjs.org/).

#### Nginx Proxy

For Nginx you can add a proxy using the follwing location block:

```
server {
    location / {
        proxy_pass http://http://127.0.0.1:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

#### Process Manager

In production you need a process manager to keep the Node server alive forever:

```bash
# install pm2 process manager
npm install -g pm2

# startup script
pm2 startup

# start process
pm2 start npm --name "laravel-nuxt" -- run start

# save process list
pm2 save

# list all processes
pm2 l
```

After each deploy you'll need to restart the process:

```bash
pm2 restart laravel-nuxt 
```

## Notes

- This project uses [router-module](https://github.com/nuxt-community/router-module), so you have to add the routes manually in `client/router.js`.
- If you want to separate this in two projects (client and server api), move `package.json` into `client/` and remove config path option from the scripts section. Also make sure to add the env variables in `client/.env`.

## Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.
