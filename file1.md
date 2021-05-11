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




## Rename Komponen-komponen Firewall

