# Catatan Powershell

File ini berisi berbagai perintah dan script Powershell. Lebih aman share tutorial dalam bentuk text, ketimbang langsung upload projectnya. Karena mana tau ada credential-credential yang terikut tanpa sengaja. Mengikuti kebiasan para hacker zaman dahulu, yang membagikan tutorial dalam bentuk file plain text. Pertama yang ingin di bahas adalah cara membuat perintah/script powershell yang berkerjasama dengan software [Aria2c](https://aria2.github.io/) .

**Source Code Untuk Download File dari Internet:**
```powershell
<# Fedora Server 34 #>

Write-Output "Sedang Mendownload Fedora Server 34 ..."

<# https://download.fedoraproject.org/pub/fedora/linux/releases/34/Server/x86_64/iso/Fedora-Server-dvd-x86_64-34-1.2.iso #>

Start-Process -FilePath C:\STEVEN\Aria2\aria2c.exe -ArgumentList "https://download.fedoraproject.org/pub/fedora/linux/releases/34/Server/x86_64/iso/Fedora-Server-dvd-x86_64-34-1.2.iso --max-download-limit=2000K --log=CatatDownload.txt --dir=C:\STEVEN\Torrent --summary-interval=0 --max-connection-per-server=5" -Wait

Write-Output "Fedora Server 34 Berhasil Di Download"

```
Jadi untuk menulis tulisan ke shell menggunakan perintah:

```powershell

Write-Output

```
Untuk bisa menjalankan perintah satu per satu, jadi setiap perintah baru dijalankan setelah satu perintah sebelumnya selesai dijalankan, maka kita menggunakan perintah:

```powershell

-Wait

```

Untuk membuat comment di source code powershell bisa menggunakan tanda:

```powershell

<# isi komentar #>

```

# Powershell dan SSH

Cara menjalankan Plink bersama dengan powershell:

https://cmatskas.com/run-ssh-with-powershell/

kalau plink sudah bisa berkerjasama dengan powershell, maka gampang untuk menjalankan perintah di remote server, maka cukup melalui Terminalnya powershell. tanpa perlu membuka aplikasi putty. akan mencoba juga script powershell, untuk copy paste file ke remote server menggunakan protokol SSH.

selanjutnya untuk telekomunikasi secara jarak jauh melalui internet, akan di fasilitasi dengan ssh melalui jalur telekomunikasi yang disediakan oleh aplikasi [Ngrok](https://ngrok.com/)

**Tutorial bagus lainnya terkait kerjasama antara powershell dengan plink**:

https://www.ttestscripting.com/2017/05/04/running-ssh-commands-in-powershell-putty-method/

**Kata kunci pencarian (Google/Duckduckgo):**

plink + run powershell command


Untuk menjalankan koneksi SSH ke mesin Linux (untuk percobaan di pergunakan Ubuntu dan Fedora), bisa menggunakan **plink.exe** . Plink akan dijalankan melalui script Powershell. Tujuannya agar bisa melakukan otomatisasi dan pekerjaan yg berulang tanpa banyak melibatkan campur tangan manusia. Dan juga bisa meremote banyak komputer di jaringan LAN maupun internet.

Contoh perintah-perintah sederhana yang berhasil dijalankan di Terminal Powershell:

Perintah yang ini ketika dijalankan masih mengharuskan pengguna menekan tombol Enter terlebih dahulu:

```text
.\plink.exe -ssh -t steven@192.168.1.4 -pw 12345 ls
```

Penambahan -batch berfungsi agar plink tidak menampilkan prompt lagi, dan langsung mengeksekusi perintah yang diberikan:

```text
.\plink.exe -ssh -t steven@192.168.1.4 -pw 12345 -batch ls
```

Multiple command yg dieksekusi setelah berhasil login ke masin Linux, bisa dijalankan melalui kode ini:

```text
.\plink.exe -ssh -t steven@192.168.1.4 -pw 12345 -batch 'cd PythonProject;ls'
```






## Rename Komponen-komponen Firewall

