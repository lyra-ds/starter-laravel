# Lyra DS Laravel template

A minimal [Laravel](https://laravel.com) template for
[Lyra Design System](https://lyra-ds.dev). It ships the public Lyra Blade
components and styles, local fonts, theme selection (light / dark / system),
live white-label branding, ready-to-go Fortify-compatible auth views, and a
Pint + Pest + npm CI setup.

[See the live demo →](https://github.com/lyra-ds/starter-laravel-demo)

## Create your project

Click **Use this template** on GitHub, or clone directly:

```sh
git clone https://github.com/lyra-ds/starter-laravel.git my-app
cd my-app
```

Then:

```sh
composer install
npm install
cp .env.example .env
php artisan key:generate
npm run build
php artisan serve
```

## After cloning

- [ ] Rename `name` in `composer.json`.
- [ ] Set `APP_NAME` in `.env`.
- [ ] Replace the example brands in `resources/css/app.css` with your own.
- [ ] When you start building, delete the `welcome.blade.php` demo content
      and replace it with your app's first page.

## White-label branding

Lyra rebrands with only four CSS variables — everything else derives from
them:

```css
[data-brand='acme'] {
  --brand: #176b87;
  --brand-contrast: #ffffff;
  --brand-radius: 0.75rem;
  --brand-font: 'Plus Jakarta Sans', sans-serif;
}
```

See `resources/css/app.css` for the example brands (`citrus`, `ocean`,
`grape`) the welcome page switches between. The "Lyra" option is the
baseline look: it removes `data-brand` entirely — never set the attribute
without defining `--brand`, or the derived accent group resolves to
nothing.

## Authentication (optional)

This template does **not install Fortify** — it only ships the seven
authentication views in `resources/views/auth/`, already styled with the
Lyra components, ready to wire up when you need real authentication.

To enable it:

```sh
composer require laravel/fortify
php artisan vendor:publish --provider="Laravel\Fortify\FortifyServiceProvider"
```

Then point Fortify at the ready-made views, in
`app/Providers/FortifyServiceProvider.php` (`boot` method):

```php
Fortify::loginView(fn () => view('auth.login'));
Fortify::registerView(fn () => view('auth.register'));
Fortify::requestPasswordResetLinkView(fn () => view('auth.forgot-password'));
Fortify::resetPasswordView(fn (Request $request) => view('auth.reset-password', ['request' => $request]));
Fortify::verifyEmailView(fn () => view('auth.verify-email'));
Fortify::confirmPasswordView(fn () => view('auth.confirm-password'));
Fortify::twoFactorChallengeView(fn () => view('auth.two-factor-challenge'));
```

## Why there is no Tailwind

Lyra is CSS-first: the components ship already styled by `@lyra-ds/styles`,
with no dependency on a utility framework. The same CSS serves React, plain
HTML, and Blade — which is exactly what this template demonstrates. Adding
Tailwind here would contradict that point. If you want Tailwind in your
app, you can install it; it is not forbidden, just absent from the starting
point.

## Scripts

| Command                | What it does                    |
| ----------------------- | -------------------------------- |
| `php artisan serve`    | Start the dev server             |
| `npm run dev`          | Vite dev server (assets)         |
| `npm run build`        | Production asset build           |
| `vendor/bin/pest`      | Run tests                        |
| `vendor/bin/pint`      | Fix code style                   |
| `vendor/bin/pint --test` | Check code style (used in CI) |

CI runs Pint, Pest, and the asset build on every push and PR, on PHP 8.3
and 8.4.

## AI agents

The template ships an [`AGENTS.md`](./AGENTS.md) that points AI coding
agents at the Lyra DS docs, the machine-readable component contracts
([llms.txt](https://lyra-ds.dev/llms.txt)), and this project's commands and
conventions. Keep it updated as your project evolves.

## Links

- [Lyra DS](https://lyra-ds.dev)
- [Lyra repository](https://github.com/lyra-ds/lyra)
- [lyra-ds/blade on Packagist](https://packagist.org/packages/lyra-ds/blade)
- [@lyra-ds/styles on npm](https://www.npmjs.com/package/@lyra-ds/styles)
- [@lyra-ds/alpine on npm](https://www.npmjs.com/package/@lyra-ds/alpine)
