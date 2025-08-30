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

```
% --- 1. Definisi Parameter Antena ---
% Frekuensi kerja dalam Hertz
frequency = 155e6; 

% Dimensi dalam meter (diubah dari cm)
radiator_length = 0.968;  % Panjang radiator (1/2 lambda)
stub_length = 0.484;      % Panjang stub (1/4 lambda)
spacing = 0.025;          % Jarak antar elemen vertikal

% Titik feed (kabel coax) dari bawah dalam meter
% INI ADALAH NILAI YANG PERLU DIUBAH UNTUK MENCARI SWR TERBAIK
% Coba ubah nilai ini antara 0.05 (5 cm) hingga 0.10 (10 cm)
feed_height = 0.07; % Memulai dengan 7 cm sebagai titik awal

% Radius kawat yang digunakan (misal, 1 mm)
wire_radius = 0.001; 

% Impedansi karakteristik kabel coax (biasanya 50 Ohm)
Z0 = 50;

% --- 2. Membuat Geometri Antena ---
% Kita akan mendefinisikan antena sebagai 3 segmen kawat:
% 1. Stub vertikal
% 2. Radiator vertikal
% 3. Penghubung horizontal di bagian bawah

% Tentukan koordinat titik-titik untuk setiap segmen kawat
% Format: [x_awal, y_awal, z_awal, x_akhir, y_akhir, z_akhir, radius]

% Letakkan pusat antena di x=0, y=0
half_space = spacing / 2;

Shape = [ ...
    % Segmen 1: Stub (kaki pendek)
    -half_space, 0, 0, -half_space, 0, stub_length, wire_radius; ...
    
    % Segmen 2: Penghubung bawah
    -half_space, 0, 0, half_space, 0, 0, wire_radius; ...
    
    % Segmen 3: Radiator (kaki panjang)
    half_space, 0, 0, half_space, 0, radiator_length, wire_radius ...
];

% --- 3. Menentukan Titik Feed ---
% Feed diberikan secara diferensial pada kedua kaki vertikal
FeedLocation = [ ...
    -half_space, 0, feed_height; ... % Titik feed di stub
     half_space, 0, feed_height  ... % Titik feed di radiator
];

% Tegangan feed, 1V dan -1V untuk feed diferensial
FeedVoltage = [1, -1];

% --- 4. Membuat Objek Antena ---
j_pole = customAntenna( ...
    Shape = Shape, ...
    FeedLocation = FeedLocation, ...
    FeedVoltage = FeedVoltage);

% --- 5. Visualisasi dan Analisis ---

% Tampilkan bentuk geometri antena
figure;
show(j_pole);
title('Geometri Antena J-Pole 155 MHz');
xlabel('X (m)'); ylabel('Y (m)'); zlabel('Z (m)');

% Tentukan rentang frekuensi untuk analisis
freq_range = linspace(150e6, 160e6, 51); % Analisis dari 150 MHz hingga 160 MHz

% Hitung dan plot SWR
figure;
SWR_data = swr(j_pole, freq_range, Z0);
plot(freq_range/1e6, SWR_data, 'LineWidth', 2);
grid on;
title(['SWR (Standing Wave Ratio) - Feed di ', num2str(feed_height*100), ' cm']);
xlabel('Frekuensi (MHz)');
ylabel('SWR');
line([155 155], ylim, 'Color', 'r', 'LineStyle', '--'); % Garis penanda 155 MHz
legend('SWR', 'Frekuensi Target');

% Tampilkan impedansi pada frekuensi kerja
Z = impedance(j_pole, frequency);
disp(['Impedansi pada ', num2str(frequency/1e6), ' MHz: ', num2str(real(Z)), ' + ', num2str(imag(Z)), 'i Ohm']);

% Tampilkan Smith Chart
figure;
smithplot(j_pole, freq_range, Z0);
title('Impedance on Smith Chart');

% Tampilkan pola radiasi 3D
figure;
pattern(j_pole, frequency);
title(['Pola Radiasi 3D pada ', num2str(frequency/1e6), ' MHz']);
```