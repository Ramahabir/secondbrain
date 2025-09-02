Oke siap 🔧 kita ubah ke bahasa Indonesia biar lebih enak dipahami.

![[Pasted image 20250830163815.png]]
---
![[Pasted image 20250830230111.png]]
# 📡 Antena J-Pole VHF (155 MHz)

### 🎯 Target Spesifikasi

- Frekuensi kerja: **155 MHz** (tengah dari 136–174 MHz → pas buat HT SAR)
    
- Bandwidth: bisa cover 136–174 MHz dengan **VSWR < 2** kalau tuning bagus
    
- Gain: sekitar **3 dBi** (jauh lebih baik dari antena bawaan/duck)
    
- Panjang total: kurang lebih **1,5 meter**
    

---

## 🛠️ Material (hemat & ramah mahasiswa)

- **Kawat tembaga** diameter 2–3 mm (butuh sekitar 2 meter). Bisa pakai kabel listrik tunggal.
    
- **Pipa PVC** panjang 1,5 meter (diameter ½ inci cukup). Jadi tiang penyangga antena.
    
- **Kabel coaxial 50Ω** (RG-58, 2–3 meter cukup untuk versi portable).
    
- **Konektor** sesuai HT (SMA, BNC, atau PL-259).
    
- **Isolasi listrik / cable ties** untuk mengikat kawat ke PVC.
    
- **Timah & solder** buat sambungan kabel.
    

💡 Biaya total: murah banget kalau pakai bahan bekas/recycle.

---

## 📏 Dimensi (panjang potongan kawat)

Dihitung dari rumus λ/4 dan λ/2 untuk 155 MHz:

- **¼ λ (stub pendek):** 48,4 cm
    
- **½ λ (radiator panjang):** 96,8 cm
    
- **Jarak antar kaki (stub & radiator):** sekitar **2,5 cm**
    
- **Titik feed (kabel coax):** sambung di **5–10 cm dari bawah** (cari posisi SWR paling rendah).
    

Jadi bentuknya kayak huruf **J**: satu kaki panjang (radiator), satu kaki lebih pendek (stub).

---

## 🔧 Cara Perakitan

1. **Potong kawat tembaga**:
    
    - Satu potong = 97 cm (radiator).
        
    - Satu potong = 48,5 cm (stub).
        
2. **Tempel ke pipa PVC**:
    
    - Ikat kedua kawat sejajar di pipa PVC dengan jarak 2,5 cm.
        
    - Hubungkan bagian bawah kedua kawat dengan jumper kawat tembaga kecil (membuat huruf J).
        
3. **Pasang kabel coax**:
    
    - Kupas ujung coax → inner conductor ke radiator, shield ke stub.
        
    - Solder di titik sekitar 7 cm dari bawah (bisa digeser naik-turun untuk tuning).
        
    - Ikat dengan isolasi biar kuat.
        
4. **Finishing**:
    
    - Tutup sambungan solder dengan lem tembak / isolasi.
        
    - Kalau ada heat-shrink tubing lebih bagus.
        
5. **Uji coba**:
    
    - Pasang antena vertikal (bisa digantung di pohon, tiang, atau tongkat tracking).
        
    - Cek SWR → geser posisi feed point sampai dapat SWR < 2.
        

---

## 📦 Tips Portabilitas

- Kalau mau ringan, pakai **kawat tembaga serabut (flexible)** → bisa digulung masuk tas.
    
- Pipa PVC bisa diganti dengan **tali/paracord** → antena digantung lurus ke bawah.
    
- Untuk dibawa: gulung kawat, ikat pakai velcro → masuk ransel.
    

---

✅ Hasil akhirnya:  
Antena **murah, ringan, portable, dan lebih kuat sinyalnya** daripada antena bawaan HT. Cocok buat operasi SAR di lapangan.

---

Mau saya bikinkan juga versi **UHF (sekitar 435 MHz)** supaya kamu bisa punya sepasang (VHF + UHF), atau cukup fokus dulu ke VHF?

---
# Hasil
## Kode
```
clear; clc;

dj = dipoleJ(RadiatorLength=0.9284, StubLength= 0.4642, Spacing=0.042, FeedOffset=-0.44);

freq = linspace(147e6, 154e6, 201);

figure(1)

show(dj)

title('Dipole-J Geometry')

figure(2)

pattern(dj, 160e6)

title('Radiation Pattern at 160 MHz')

figure(3)

vswr(dj, freq, 50)
```
## Gambar
![[model.png]]

![[radiation.png]]

![[vswr.png]]