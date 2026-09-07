# Enable/Disable Two-Factor Auth for Magento 2 (SISL fork)

Adds an admin configuration switch to turn Magento 2's mandatory Two-Factor Authentication
on or off. Magento forces 2FA on every admin login, which is correct for production but a
constant friction on **staging, dev and CI environments** where a shared admin has no phone
to enrol. This module lets you disable it there — from config, without hacking core or
juggling `bin/magento security:tfa:*` commands.

Maintained fork of `wolfsellers/module-enabledisabletfa`, verified on **Magento 2.4.9 / PHP 8.4**.

## What changed vs upstream

- Added `require` to composer.json (`php` 8.1–8.5, `magento/framework >=103.0.4 <104`); the
  original declared neither, so Composer would install it on any incompatible version silently.
- Relaxed the `magento/module-two-factor-auth` constraint from `1.*` (which blocked newer
  Magento) to work with the version shipped in 2.4.9. Removed `minimum-stability: dev`.

> Use it on non-production environments. Leave 2FA enabled in production.

## Install

```bash
composer config repositories.tfa vcs https://github.com/SISL-source/module-enabledisabletfa
composer require wolfsellers/module-enabledisabletfa:dev-main
bin/magento module:enable WolfSellers_EnableDisableTfa
bin/magento setup:upgrade
```

Then toggle it under *Stores → Configuration → Security → 2FA* (admin scope).

## License

MIT (upstream). Maintained by [SISL](https://sisl.pl).
