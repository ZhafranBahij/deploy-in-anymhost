# deploy-in-anymhost

Tulisan ini hanyalah review berdasarkan pengalaman untuk menggunakan [Anymhost](https://anymhost.id/) selama 1 hari. Terakhir kali aku mendeploy ke suatu server mungkin sekitar 2 tahun yang lalu. 

## Kenapa Hosting Pakai Anymhost

![alt](img/Screenshot_(1140).jpg)

Karena murah, aku menggunakan Anymhost. Secara teknis, murah di sini lebih merujuk kepada batas minimal harga yang ditawarkan. Yup, cukup 50rb/tahun bisa meraih mendapatkan suatu server.

![alt](img/Screenshot_(1141).jpg)

Jika ingin mendapatkan akses SSH dan keamanan SSL, harga 180rb/tahun bisa didapat. Sejauh ini, Anymhost memang melayani paket murah.

Selain itu, vibes anime yang ditawarkan juga menarik perhatian. Sebagai penikmat anime, tidak ada salahnya menikmati hostingan yang ada tema animenya, kan?

## Tujuan Utama

Tujuan utama beli server karena ingin belajar mengolah server jika memakai framework Laravel.

Di samping itu, ada keinginan untuk mempelajari cara deploy hal-hal lain seperti React JS dan sebagainya.

## Catatan

Untuk skala profesional, disarankan memakai hostingan lain. Soalnya, sebagian hostingan lain menawarkan spek gahar dgn harga yg mungkin terjangkau.

## Panduan

Ini hanya merupakan panduan jika diriku kehilangan arah tentang cara penggunaan Cpanel di Anymhost. 

Ada kemungkinan, ini juga bisa berlaku di beberapa hostingan lainnya dan kemungkinannya lebih besar jika hostingan tersebut menggunakan Cpanel juga.

### Cloning Repo dari Github

1. Ketik ini di terminal. Usahakan tidak menggunakan passphrase. Passphrase tuh mirip dgn password.

```bash
ssh-keygen -t rsa -f ~/.ssh/repo_name -b 4096 -C "cpanel_username@your_website_name"
```

![alt](img/Screenshot_(1135)_edited.jpg)
<!-- ![alt](Screenshot_(1135)_edited.jpg) -->

2. Buka CPanel File Manager, lalu buka folder .ssh. Atur config agar jadi 0600 dan isi config di bawah ini. 
Btw, isi confignya yg aku ketahui hanya bisa 1 IdentityFile saja.

```
Host *
    IdentityFile ~/.ssh/repo_name
```
![alt](img/Screenshot_(1142).jpg)
![alt](img/Screenshot_(1136).jpg)

3. Buka repo github > settings > deploy keys > add new

![alt](img/Screenshot_(1137).jpg)

4. Isi key dgn public key. Public key bisa diakses di folder .ssh, lalu cari yg "nama_repo.pub".

![alt](img/screenshot_(1143)_edited.jpg)

5. Setelah itu, coba cek menggunakan command di bawah.

```bash
ssh -T -p 443 git@ssh.github.com
```

![alt](img/screenshot_(1139).jpg)

6. Git clone di terminal dgn

```bash
git clone ssh://git@ssh.github.com:443/nama_user_github/nama_repo.git
```

atau 

```bash
git clone https://github.com/nama_user_github/nama_repo.git
```

### Sub Domain 
1. Masuk ke Cpanel, lalu search menu Domain.

![alt](img/screenshot_(1155).jpg)

2. Nantinya akan ada daftar domain serta subdomain yg kita punya. Silahkan klik "Create a New Domain".

![alt](img/screenshot_(1156).jpg)

3. Buat domain seperti ini. Lalu, penempatan document root seperti ini. Kalau sudah tekan submit.

```bash
nama_sub_domain.nama_domain.nama_extension
```

```bash
/public_html/nama_sub_domain.nama_domain.nama_extension
```

![alt](img/screenshot_(1157).jpg)

4. Ketika prosesnya kelar, akan muncul pesan seperti ini.

![alt](img/screenshot_(1158).jpg)

5. Kalau sudah, tinggal pindahkan isi web yg diinginkan ke dalam folder sub domain.

![alt](img/screenshot_(1159).jpg)

6. Hasilnya seperti ini.

![alt](img/screenshot_(1160).jpg)

### Deploy Laravel
1. Lakukan git clone kepada folder yg dituju. Kalau saya cloning di folder laravel_app.

![alt](img/screenshot_(1183).jpg)

2. Buat DB-nya terlebih dahulu. Masuk ke menu Database > MySQL Databases.

![alt](img/screenshot_(1184).jpg)

3. Buat database dgn cara masukkan nama Database lalu tekan tombol **Create Database**

![alt](img/screenshot_(1185).jpg)

4. Buat user.

![alt](img/screenshot_(1186).jpg)

5. Lakukan **Add User To Database**. Agar database bisa diakses nantinya.

![alt](img/screenshot_(1187).jpg)

6. Atur **.env** di folder project laravelnya

![alt](img/screenshot_(1177)_edited.jpg)

7. Lakukan **composer update** di tempat projekan berada melalui terminal.

![alt](img/screenshot_(1170)_edited.jpg)

8. Lakukan **php artisan migrate** di terminal. Jika ada error sepert ini, tambahkan ini di file **AppServiceProvider.php**.

```php
use Illuminate\Support\Facades\Schema;

/**
 * Bootstrap any application services.
 *
 * @return void
 */
public function boot()
{
    Schema::defaultStringLength(191);
}
```

![alt](img/screenshot_(1175).jpg)

9. Lakukan lagi **php artisan migrate**.

![alt](img/screenshot_(1176).jpg)

10. Buat subdomainnya. Lalu pindahkan isi dari folder public ke subdomain.

11. Ubah lokasi directory kedua item tersebut di **index.php** menuju ke directory sebenarnya. Untuk contohnya, gambar di bawah adalah hasil pengubahan. Lokasi **folder projek laravel** terletak di **folder laravel_app** . **Folder laravel_app** terletak di home. Lalu, **file index.php**  terletak di **folder subdomain**. Lalu, lokasi **folder subdomain** ada di dalam **public_html**. **public_html** terletak di **home**

![alt](img/screenshot_(1169).jpg)

12. Seperti ini penempatan **index.php**

![alt](img/screenshot_(1188).jpg)

13. Kalau berhasil, bisa menampilkan page yg sesuai keinginan.

![alt](img/screenshot_(1181).jpg)

## Sumber Tutorial

- [Clone Repo Github](https://docs.cpanel.net/knowledge-base/web-services/guide-to-git-set-up-access-to-private-repositories/)
- [Fixing issue clone repo github](https://askubuntu.com/questions/610940/ssh-connect-to-host-github-com-port-22-connection-refused)
- [Deploy Laravel](https://www.iankumu.com/blog/deploy-laravel-on-shared-hosting/)
- [Subdomain](https://docs.cpanel.net/cpanel/domains/domains/)