
# Penjelasan code
## import pustaka
```bash
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
cv2: OpenCV, pustaka untuk pemrosesan gambar dan video.  
numpy: Pustaka untuk operasi array multidimensi.  
matplotlib.pyplot: Pustaka untuk plotting grafik.

## Memuat Gambar dan Konversi ke RGB:
```bash
gambar = cv2.imread('jeruk.jpg')
gambar_rgb = cv2.cvtColor(gambar, cv2.COLOR_BGR2RGB)
```
cv2.imread('jeruk.jpg'): Memuat gambar dari file.  
cv2.cvtColor(gambar, cv2.COLOR_BGR2RGB): Mengonversi gambar dari format BGR (defaultOpenCV) ke format RGB yang lebih sering dipakai.

## Mengonversi Gambar ke Ruang Warna HSV:
```bash
hsv = cv2.cvtColor(gambar_rgb, cv2.COLOR_RGB2HSV)
```
Mengonversi gambar dari ruang warna RGB ke ruang warna HSV (Hue, Saturation, Value). Ruang warna HSV memisahkan informasi warna (Hue) dari intensitas (Value), sehingga memudahkan dalam segmentasi berdasarkan warna.

## Mendefinisikan Rentang Warna untuk Jeruk dan Daun:
```bash
oren_bawah = np.array([10, 100, 100])
oren_atas = np.array([25, 255, 255])

hijau_bawah = np.array([36, 25, 25])
hijau_atas = np.array([86, 255, 255])
```
Rentang warna ini didefinisikan dalam format HSV untuk mengidentifikasi warna oren dari jeruk dan hijau dari daun. Nilai-nilai ini adalah batas bawah dan atas dari nilai HSV yang akan digunakan untuk membuat masker.

## Membuat Masker untuk Jeruk dan Daun
```bash
masker_jeruk = cv2.inRange(hsv, oren_bawah, oren_atas)
masker_daun = cv2.inRange(hsv, hijau_bawah, hijau_atas)
```
cv2.inRange(): Fungsi ini membuat masker biner, di mana piksel dalam rentang yang ditentukan diatur ke 255 (putih), dan piksel di luar rentang diatur ke 0 (hitam). Masker ini digunakan untuk menyorot bagian gambar yang memiliki warna tertentu.

## Segmentasi Jeruk dan Daun dari Gambar:
```bash
segmentasi_jeruk = cv2.bitwise_and(gambar_rgb, gambar_rgb, mask=masker_jeruk)
segmentasi_daun = cv2.bitwise_and(gambar_rgb, gambar_rgb, mask=masker_daun)
```
cv2.bitwise_and(): Fungsi ini menggabungkan gambar asli dengan masker biner, sehingga hanya bagian gambar yang sesuai dengan masker yang tetap ada. Ini dilakukan untuk kedua masker: jeruk dan daun.

## Menampilkan Hasil:
```bash
plt.figure(figsize=(10, 10))

plt.subplot(2, 2, 1)
plt.title('Gambar Asli')
plt.imshow(gambar_rgb)
plt.axis()

plt.subplot(2, 2, 2)
plt.title('Masker Jeruk')
plt.imshow(masker_jeruk, cmap='gray')
plt.axis()

plt.subplot(2, 2, 3)
plt.title('Segmentasi Jeruk')
plt.imshow(segmentasi_jeruk)
plt.axis()

plt.subplot(2, 2, 4)
plt.title('Segmentasi Daun')
plt.imshow(segmentasi_daun)
plt.axis()

plt.tight_layout()
plt.show()
```
plt.figure(): Membuat figure baru dengan ukuran tertentu.  
plt.subplot(): Menambahkan subplot ke figure.  
plt.title(): Menambahkan judul ke subplot.  
plt.imshow(): Menampilkan gambar di subplot.  
plt.axis('off'): Menonaktifkan sumbu pada subplot.  
plt.tight_layout(): Menyusun subplot agar tidak tumpang tindih.  
plt.show(): Menampilkan figure yang berisi semua subplot.  






# Penjelasan code
## import pustaka
```bash
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
cv2: OpenCV, pustaka untuk pemrosesan gambar dan video.  
numpy: Pustaka untuk operasi array multidimensi.  
matplotlib.pyplot: Pustaka untuk plotting grafik.

## Memuat Gambar dan Konversi ke RGB:
```bash
gambar = cv2.imread('jeruk.jpg')
gambar_rgb = cv2.cvtColor(gambar, cv2.COLOR_BGR2RGB)
```
cv2.imread('jeruk.jpg'): Memuat gambar dari file.  
cv2.cvtColor(gambar, cv2.COLOR_BGR2RGB): Mengonversi gambar dari format BGR (defaultOpenCV) ke format RGB yang lebih sering dipakai.

## Mengonversi Gambar ke Ruang Warna HSV:
```bash
hsv = cv2.cvtColor(gambar_rgb, cv2.COLOR_RGB2HSV)
```
Mengonversi gambar dari ruang warna RGB ke ruang warna HSV (Hue, Saturation, Value). Ruang warna HSV memisahkan informasi warna (Hue) dari intensitas (Value), sehingga memudahkan dalam segmentasi berdasarkan warna.

## Mendefinisikan Rentang Warna untuk Jeruk dan Daun:
```bash
oren_bawah = np.array([10, 100, 100])
oren_atas = np.array([25, 255, 255])

hijau_bawah = np.array([36, 25, 25])
hijau_atas = np.array([86, 255, 255])
```
Rentang warna ini didefinisikan dalam format HSV untuk mengidentifikasi warna oren dari jeruk dan hijau dari daun. Nilai-nilai ini adalah batas bawah dan atas dari nilai HSV yang akan digunakan untuk membuat masker.

## Membuat Masker untuk Jeruk dan Daun
```bash
masker_jeruk = cv2.inRange(hsv, oren_bawah, oren_atas)
masker_daun = cv2.inRange(hsv, hijau_bawah, hijau_atas)
```
cv2.inRange(): Fungsi ini membuat masker biner, di mana piksel dalam rentang yang ditentukan diatur ke 255 (putih), dan piksel di luar rentang diatur ke 0 (hitam). Masker ini digunakan untuk menyorot bagian gambar yang memiliki warna tertentu.

## Segmentasi Jeruk dan Daun dari Gambar:
```bash
segmentasi_jeruk = cv2.bitwise_and(gambar_rgb, gambar_rgb, mask=masker_jeruk)
segmentasi_daun = cv2.bitwise_and(gambar_rgb, gambar_rgb, mask=masker_daun)
```
cv2.bitwise_and(): Fungsi ini menggabungkan gambar asli dengan masker biner, sehingga hanya bagian gambar yang sesuai dengan masker yang tetap ada. Ini dilakukan untuk kedua masker: jeruk dan daun.

## Menampilkan Hasil:
```bash
plt.figure(figsize=(10, 10))

plt.subplot(2, 2, 1)
plt.title('Gambar Asli')
plt.imshow(gambar_rgb)
plt.axis()

plt.subplot(2, 2, 2)
plt.title('Masker Jeruk')
plt.imshow(masker_jeruk, cmap='gray')
plt.axis()

plt.subplot(2, 2, 3)
plt.title('Segmentasi Jeruk')
plt.imshow(segmentasi_jeruk)
plt.axis()

plt.subplot(2, 2, 4)
plt.title('Segmentasi Daun')
plt.imshow(segmentasi_daun)
plt.axis()

plt.tight_layout()
plt.show()
```
plt.figure(): Membuat figure baru dengan ukuran tertentu.  
plt.subplot(): Menambahkan subplot ke figure.  
plt.title(): Menambahkan judul ke subplot.  
plt.imshow(): Menampilkan gambar di subplot.  
plt.axis('off'): Menonaktifkan sumbu pada subplot.  
plt.tight_layout(): Menyusun subplot agar tidak tumpang tindih.  
plt.show(): Menampilkan figure yang berisi semua subplot.  






## Teori yang di gunakan
`+`Ruang Warna (Color Space):

    `+`RGB (Red, Green, Blue) adalah model warna yang umum digunakan untuk tampilan dan pencitraan digital.  
    `+`HSV (Hue, Saturation, Value) adalah model warna yang memisahkan informasi warna (Hue) dari intensitas (Value), sehingga memudahkan segmentasi berdasarkan warna.  
`+`Segmentasi Warna:

    `+`Segmentasi warna adalah teknik untuk memisahkan objek dalam gambar berdasarkan warna mereka. Ini berguna dalam berbagai aplikasi seperti deteksi objek, pengenalan pola, dan analisis citra.
`+`Masking:

    `+`Masking adalah teknik untuk memisahkan bagian tertentu dari gambar berdasarkan kriteria tertentu (dalam hal ini, warna). Masker biner digunakan untuk menunjukkan bagian gambar yang memenuhi kriteria tersebut.