## install

```
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === 'e0012edf3e80b6978849f5eff0d4b4e4c79ff1609dd1e613307e16318854d24ae64f26d17af3ef0bf7cfb710ca74755a') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
```

## install options

- `--install-dir`

  ```
  php composer-setup.php --install-dir=bin
  ```
  
- `--filename`

  ```
  php composer-setup.php --filename=composer
  ```
  
- `--version`

  ```
  php composer-setup.php --version=1.0.0-alpha8
  ```
  
## packagist

```
composer config -g repo.packagist composer https://packagist.phpcomposer.com
```

## operators

```
composer require/install/update 
```
