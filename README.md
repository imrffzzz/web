# Setup Google Apps Script untuk Review Website

## Konfigurasi:
- **Google Apps Script URL**: `https://script.google.com/macros/s/AKfycbzjzuVC3HSNAvEO9OC0_iILJU6pRVNA62zkRCukhXYzDYcJ1w7jyR-dPjkAwo1riFWMhw/exec`

## PENTING - Gunakan Script Ini di Apps Script:
```javascript
function doPost(e) {
  try {
    var ss = SpreadsheetApp.getActiveSpreadsheet();
    var sheet = ss.getSheetByName('Sheet1'); 

    var Nama       = e.parameter.Nama;
    var Rating     = e.parameter.Rating
    var Ulasan    = e.parameter.Ulasan;
    var Tanggal       = e.parameter.Tanggal;
    var WaktuInput    = e.parameter.WaktuInput;

    sheet.appendRow([new Date(), Nama, Rating, Ulasan, Tanggal, WaktuInput]);

    return ContentService.createTextOutput("Data Berhasil Disimpan!")
                         .setMimeType(ContentService.MimeType.TEXT);
    
  } catch (error) {
    return ContentService.createTextOutput("Terjadi Eror: " + error.toString())
                         .setMimeType(ContentService.MimeType.TEXT);
  }
}
```

## Cara Setup (PENTING - Ikuti dengan Teliti):

### Cara 1: Dari Google Spreadsheet (REKOMENDASI)
1. **Buka Google Spreadsheet Anda** yang ingin digunakan untuk menyimpan data
2. Klik menu **Extensions** (Ekstensi)
3. Pilih **Apps Script**
4. Hapus semua kode yang ada di editor
5. **Copy semua kode** dari file `GoogleAppsScript.gs` dan paste ke editor
6. Klik ikon **Save** (disket) atau tekan Ctrl+S
7. Klik tombol **Deploy** (kanan atas) > **New deployment**
8. Klik ikon gear > pilih **Web app**
9. Isi deskripsi: "Review API"
10. **Execute as**: "Me"
11. **Who has access**: "Anyone"
12. Klik **Deploy**
13. Jika diminta otorisasi, klik **Authorize access** > pilih akun > klik **Advanced** > **Go to (unsafe)** > **Allow**
14. **Copy URL baru** yang muncul (atau gunakan URL di atas)

### Cara 2: Dari Google Apps Script (Alternatif)
1. Buka https://script.google.com/
2. Buat project baru
3. Copy kode dari file `GoogleAppsScript.gs`
4. Hubungkan dengan spreadsheet: klik "None" di sidebar > pilih spreadsheet
5. Deploy sebagai Web App

## Buat Sheet "Sheet1":
1. Di spreadsheet Anda, klik **"+"** untuk membuat sheet baru
2. Rename sheet menjadi: **Sheet1** (huruf S dan 1 besar!)
3. Di baris pertama (opsional - tidak wajib), bisa tambah header:
   - A1: `Tanggal`
   - B1: `Nama`
   - C1: `Rating`
   - D1: `Ulasan`
   - E1: `Tanggal`
   - F1: `WaktuInput`

## Update index.html:
URL di index.html sudah diupdate otomatis:
```
https://script.google.com/macros/s/AKfycbxfZqXKQMcmtPbPYr6PCXfkL1hj3Oc7bL6lDMtVtoFTldX61U0aQMlvfgI-rfRL8MrpWA/exec
```

## Test:
1. Buka website Anda
2. Klik "Write a Review"
3. Isi nama, rating, dan ulasan
4. Klik submit
5. Cek Google Spreadsheet - data harusnya muncul!

## Troubleshooting:
- **Data tidak muncul?** Pastikan sheet name adalah "Reviews" (huruf besar R)
- **Error di console?** Buka Apps Script > View > Executions untuk melihat error logs
- **Sheet tidak ditemukan?** Pastikan sheet "Reviews" sudah dibuat secara manual

