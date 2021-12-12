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

Cara mengeksekusi Bash Script di remote komputer menggunakan Plink:

https://superuser.com/questions/413783/how-to-run-bash-script-on-a-linux-host-from-windows-using-plink


kata kunci pencarian:

plink + create bash file remotely


Sedang mempelajari tentang [Invoke-Expression](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/invoke-expression?view=powershell-7.1) di Powershell, Invoke-Expression ini akan dipadukan dengan SSH untuk menjalankan perintah/script di remote komputer.

Contoh source code Invoke-Expression yang sudah di coba:

```powershell
$TampilkanProsesBerjalan = "Get-Process"

Invoke-Expression $TampilkanProsesBerjalan
```


Source code yg memanfaatkan Invoke-Expression dan SSH yang berhasil dijalankan:

```powershell
<# mengeksekusi script bash yg ada di remote komputer, kali ini menggunakan bantuan Invoke-Expression #>
<# script dalam bahasa bash akan meminta input, input di minta di Terminal Windows #>

$perintah = 'bash /home/steven/proyekBash/Latihan1/file2.sh'

$alamatServer = '192.168.1.4'

$namaPengguna = 'steven'

$kataKunci = '12345'

$plinkPath = 'C:\STEVEN\ProyekPowershell\Latihan1\plink.exe'



<# Perintah SSH yg di bundel ke dalam variabel #>

$perintahRemote = "& $plinkPath -pw $kataKunci -t $namaPengguna@$alamatServer -batch $perintah"

Invoke-Expression -Command $perintahRemote
```

file2.sh nya berisi source code ini:

```bash
#!/bin/sh
printf "\n"
echo "Tuliskan nama anda : "
read Nama
echo "Selamat Datang Di Fedora 34, $Nama"
```


## Cara Membuat Menu di Powershell

Contoh sederhana:

```powershell

<# Membuat menu di Powershell #>

$makananEnak = Read-Host -Prompt 'Apa Makanan Favorit di Jakarta ?'

if ($makananEnak -eq 'Nasi Padang') {

	Write-Output "Nasi Padang adalah makanan favorit yg rasanya pedas."

} else {

	Write-Output "$makananEnak adalah makanan yang jarang di temui." 

}


```

Melanjutkan source code untuk membuat menu di Powershell:

```powershell

$merah = New-Object System.Management.Automation.Host.ChoiceDescription '&Merah', 'Warna Pilihan : Merah'
$kuning = New-Object System.Management.Automation.Host.ChoiceDescription '&Kuning', 'Warna Pilihan : Kuning'
$hijau = New-Object System.Management.Automation.Host.ChoiceDescription '&Hijau', 'Warna Pilihan : Hijau'

$pilihan = [System.Management.Automation.Host.ChoiceDescription[]]($merah, $kuning, $hijau)

$judul = 'Warna Kesukaan'
$isiPesan = 'Apa warna kesukaan mu ?'
$hasilPilihan = $host.ui.PromptForChoice($judul, $isiPesan, $pilihan, 0)

switch ($hasilPilihan){

	0 { 'Warna kesukaan anda adalah Merah' }

	1 { 'Warna kesukaan anda adalah Kuning' }

	2 { 'Warna kesukaan anda adalah Hijau' }


	}


```


