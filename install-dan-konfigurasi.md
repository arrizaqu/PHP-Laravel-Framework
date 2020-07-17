# Instalasi dan Konfigurasi

Beberapa yang harus diperhatikan dalam konfigurasi laravel adalah sebagai berikut :

## Standart kebutuhan

Kerangka kerja Laravel memiliki beberapa persyaratan sistem. Tentu saja, semua persyaratan ini dipenuhi oleh mesin virtual Laravel, dan kemudian anda harus memastikan server Anda memenuhi persyaratan berikut:

* PHP &gt;= 7.1.3
* OpenSSL PHP Extension
* PDO PHP Extension
* Mbstring PHP Extension
* Tokenizer PHP Extension
* XML PHP Extension
* Ctype PHP Extension
* JSON PHP Extension
* BCMath PHP Extension

## Instalasi dengan PHP Composer

Pertama, unduh Laravel installer menggunakan Composer:

```
composer global require laravel/installer
```

namun sebelum menggunakan composer sebaiknya untuk terlebih dahulu meng-install php composer, PHP Composer adalah salah satu dependency management untuk PHP, seperti halnya maven dan gradle. secara singkat bisa kita lakukan peng-installan composer dengan code berikut ini melalui CLI command line:

```
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === '48e3236262b34d30969dca3c37281b3b4bbe3221bda826ac6a9a62d6444cdb0dcd0615698a5cbe587c3f0fe57a54d8f5') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
```

namun lagi lagi tidak terlupakan adalah perlu di install terlebih dahulu PHP-CLI di composer kita sebelumnya.

Setelah itu, akan dapatkan file di dalam directory tersebut file "composer.phar", pertama kalinya perlu di tambahkan repository laravel/installer ke dalam compser, sehingga composer tahu kemana akan mencari dependency laravel yang akan diperlukan pada saat instalasi.

```
php composer.phar composer global require laravel/installer
```

selanjutnya adalah create project laravel menggunakan composer sebagai beriikut :

```
php composer.phar create-project --prefer-dist laravel/laravel smartweb
```

jika berjalan dengan baik, maka kita sudah memilki project laravel yang siap untuk di jalankan untuk pertama kali.

## Menjalankan Service

Untuk menjalankan deployment atau pertama kali apakah aplikasi sudah bisa di jalan maka dapat dilakukan sebagai berikut :

```
php artisan serve
```

dan jalankan dengan url browser : [http://localhost:8000/](http://localhost:8000/)

# Application Key

Hal berikutnya yang harus Anda lakukan setelah menginstal Laravel adalah mengatur kunci aplikasi Anda ke string acak. Jika Anda menginstal Laravel melalui Composer atau installer Laravel, kunci ini telah ditetapkan untuk Anda

```
php artisan key:generate
```

**If the application key is not set, your user sessions and other encrypted data will not be secure!**

## Install existing application

php -d "disable\_functions=" composer.phar install --ignore-platform-reqs

