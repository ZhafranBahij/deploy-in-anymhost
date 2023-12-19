# deploy-in-anymhost

Tulisan ini hanyalah review berdasarkan pengalaman untuk menggunakan Anymhost selama 1 hari. Terakhir kali aku mendeploy ke suatu server mungkin sekitar 2 tahun yang lalu. 

## Kenapa Hosting Pakai Anymhost

Karena murah, aku menggunakan Anymhost. Secara teknis, murah di sini lebih merujuk kepada batas minimal harga yang ditawarkan. Yup, cukup 50rb/tahun bisa meraih mendapatkan suatu server.

Jika ingin mendapatkan akses SSH dan keamanan SSL, harga 180rb/tahun bisa didapat. Sejauh ini, Anymhost memang melayani paket murah.

Selain itu, vibes anime yang ditawarkan juga menarik perhatian. Sebagai penikmat anime, tidak ada salahnya menikmati hostingan yang ada tema animenya, kan?

## Catatan

Untuk skala profesional, tampaknya ada beberapa hostingan lainnya yang menyediakan fasilitas menarik dgn harga yg gak jauh beda. 

## Panduan

Ini hanya merupakan panduan jika diriku kehilangan arah tentang cara penggunaan.

### Cloning Repo dari Github

1. Ketik ini di terminal 

```bash
ssh-keygen -t rsa -f ~/.ssh/repo_name -b 4096 -C "cpanel_username@your_website_name"
```

![alt]('./Screenshot%20(1135).png')

1. Buka CPanel, lalu buka folder .ssh. Atur config agar jadi 0600 dan isi config di bawah ini

```
Host *
    IdentityFile ~/.ssh/repo_name
```

3. Buka repo github > settings > deploy keys > add new

4. Isi dgn public key. Public key bisa diakses di folder .ssh, lalu cari yg "nama_repo.pub"

5. Cek dulu menggunakan 

```bash
ssh -T -p 443 git@ssh.github.com
```

6. Git clone di terminal dgn

```bash
git clone ssh://git@ssh.github.com:443/Amekiri9023/example-app.git
```
