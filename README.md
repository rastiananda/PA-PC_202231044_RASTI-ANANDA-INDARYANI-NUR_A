
# DETEKSI TEPI POLA OBJEK

### 1. Teori yang mendukung mengenai Project ini

Teori yang mendukung di dalam project ini adalah teori pengolahan citra digital, yang mencakup teknik untuk memanipulasi gambar digital melalui operasi seperti peningkatan gambar, restorasi gambar, segmentasi, dan pengenalan pola. Pada proyek ini, kita menerapkan teknik pengolahan citra untuk mengubah gambar asli menjadi bentuk yang lebih mudah dianalisis. Deteksi tepi pola objek adalah proses identifikasi batas-batas objek dalam gambar yang menandai perubahan signifikan dalam intensitas warna. Konversi dari gambar berwarna ke gambar skala abu-abu adalah langkah penting dalam banyak aplikasi pengolahan citra karena gambar berwarna terdiri dari tiga komponen warna (RGB), sementara gambar skala abu-abu hanya terdiri dari satu komponen intensitas. Konversi ini menyederhanakan proses analisis karena banyak algoritma pengolahan citra bekerja lebih baik pada gambar dengan satu komponen. Deteksi tepi adalah proses menemukan batas atau tepi dalam gambar, yang biasanya menandai perubahan signifikan dalam intensitas warna. Algoritma deteksi tepi, seperti deteksi tepi Canny yang digunakan dalam proyek ini, didasarkan pada konsep gradien intensitas. Gradien intensitas mengukur perubahan dalam intensitas warna pada piksel tetangga, sehingga memungkinkan identifikasi tepi yang tajam. Algoritma Canny menggunakan filter Gaussian untuk menghaluskan gambar, menghitung gradien dengan operator Sobel, dan kemudian menerapkan dua ambang batas (threshold) untuk mendeteksi tepi yang kuat dan lemah. Kontur adalah garis atau kurva yang menghubungkan titik-titik dengan intensitas yang sama atau perubahan intensitas yang signifikan dalam gambar. Deteksi kontur adalah teknik segmentasi yang sering digunakan dalam pengolahan citra untuk mengekstraksi bentuk objek dalam gambar. Pustaka OpenCV menyediakan fungsi yang dapat menemukan dan menggambar kontur berdasarkan hasil deteksi tepi. OpenCV (Open Source Computer Vision Library) adalah pustaka yang menyediakan berbagai fungsi untuk pengolahan citra dan visi komputer. Teori yang mendukung penggunaan OpenCV mencakup berbagai algoritma dan teknik yang telah diimplementasikan dalam pustaka ini untuk memfasilitasi tugas-tugas seperti pemrosesan gambar, analisis video, dan pengenalan objek. Pada proyek ini, OpenCV digunakan untuk membaca gambar, mengkonversi gambar ke skala abu-abu, melakukan deteksi tepi, dan mendeteksi serta menggambar kontur. Visualisasi data adalah teknik untuk menampilkan data dalam bentuk grafis untuk memudahkan pemahaman dan analisis. Pustaka Matplotlib digunakan dalam proyek ini untuk menampilkan gambar asli, hasil deteksi tepi, dan gambar dengan kontur yang terdeteksi. Visualisasi ini membantu dalam memahami bagaimana setiap langkah dalam proses pengolahan citra mempengaruhi hasil akhir dan memastikan bahwa deteksi tepi dan kontur berjalan dengan baik. Dengan memahami teori-teori di atas, kita dapat melihat bagaimana berbagai konsep dalam pengolahan citra digital diterapkan dalam proyek deteksi tepi dan kontur untuk menghasilkan analisis gambar yang akurat dan efektif.

### 2. Tahapan cara menyelesaikan Project ini

- Tahap pertama adalah membaca gambar yang ingin dianalisis. Gambar tersebut diimpor ke dalam program menggunakan pustaka OpenCV, sebuah pustaka terkenal dalam pengolahan citra dan visi komputer. Setelah gambar berhasil diimpor, langkah selanjutnya adalah mengkonversi gambar berwarna tersebut ke dalam format skala abu-abu. Konversi ini penting karena banyak algoritma deteksi tepi bekerja lebih efektif pada gambar yang tidak mengandung informasi warna, melainkan hanya intensitas cahaya.

- Tahap kedua  yakni setelah gambar dikonversi ke skala abu-abu, algoritma deteksi tepi Canny diterapkan. Deteksi tepi Canny adalah salah satu metode paling populer dan efektif untuk mendeteksi tepi dalam gambar. Algoritma ini bekerja dengan menerapkan filter Gaussian untuk menghaluskan gambar dan mengurangi noise, kemudian menghitung gradien intensitas gambar untuk menemukan tepi yang kuat. Dua ambang batas (threshold) digunakan untuk menentukan tepi yang kuat dan tepi yang lemah, sehingga hasil deteksi tepi lebih akurat dan minim noise.

- Tahap ketiga adalah mendeteksi kontur berdasarkan hasil deteksi tepi. Kontur adalah kurva yang menghubungkan titik-titik dengan intensitas yang sama atau perubahan intensitas yang signifikan. Pustaka OpenCV menyediakan fungsi untuk menemukan dan menggambar kontur pada gambar. Pada proyek ini, kontur yang ditemukan kemudian digambar di atas salinan gambar asli untuk memvisualisasikan hasil deteksi.

- Terakhir, hasil dari setiap tahapan proses kemudian divisualisasikan menggunakan pustaka Matplotlib. Visualisasi ini penting untuk memahami bagaimana setiap langkah mempengaruhi gambar dan untuk memastikan bahwa deteksi tepi dan kontur berjalan dengan baik. Gambar asli, hasil deteksi tepi dengan Canny, dan gambar dengan kontur yang terdeteksi ditampilkan berdampingan untuk perbandingan yang mudah.


### 3. Penjelasan program

#### 1). Mengimport Library:
```
import cv2
import numpy as np
from matplotlib import pyplot as plt
```
#### Penjelasan:
Pada bagian cv2 adalah modul OpenCV yang digunakan untuk pemrosesan gambar dan video, kemudian numpy (np) adalah pustaka digunakan untuk operasi array serta pyplot dari matplotlib adalah pustaka digunakan untuk menampilkan gambar.

#### 2). Membaca Gambar:
```
image_path = ('rasti4.jpg')
image = cv2.imread(image_path)
```
#### Penjelasan:
Pada bagian ini `cv2.imread` membaca gambar dari path yang diberikan.

#### 3). Mengkonversi gambar ke grayscale:
```
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
```
#### Penjelasan:
Pada bagian ini `cv2.cvtColor` mengonversi gambar dari format BGR (Blue-Green-Red) ke grayscale. Konversi ini diperlukan untuk deteksi tepi dan kontur karena algoritma tersebut bekerja lebih baik pada gambar grayscale.


#### 4). Deteksi tepi menggunakan Canny Edge Detection
```
edges = cv2.Canny(gray_image, 40, 80)
```
#### Penjelasan:
Pada bagian ini `cv2.Canny` digunakan untuk deteksi tepi pada gambar. Parameter pertama adalah gambar input, parameter kedua dan ketiga adalah nilai ambang bawah dan atas untuk deteksi tepi. Nilai-nilai ini dapat disesuaikan sesuai dengan kebutuhan.


#### 5). Deteksi kontur
```
contours, _ = cv2.findContours(edges, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)
contour_image = cv2.cvtColor(gray_image, cv2.COLOR_GRAY2BGR)
cv2.drawContours(contour_image, contours, -1, (0, 255, 0), 2)
```
#### Penjelasan:
Pada bagian ini proses deteksi kontur dilakukan dengan menggunakan `cv2.findContours` pada gambar tepi yang dihasilkan dari deteksi Canny. Fungsi ini mengembalikan daftar kontur yang ditemukan dalam gambar. Kontur ini kemudian digambar pada gambar yang telah dikonversi dari grayscale ke format BGR menggunakan `cv2.cvtColor`, sehingga memungkinkan pewarnaan kontur. Untuk menggambar kontur, digunakan `cv2.drawContours` dengan parameter gambar `(contour_image)`, daftar kontur `(contours)`, `-1` untuk menggambar semua kontur, warna hijau `(BGR: 0, 255, 0)`, dan ketebalan garis 2 piksel. Hasilnya adalah gambar grayscale dengan kontur berwarna hijau yang menunjukkan batas-batas objek yang terdeteksi.


#### 6). Menampilkan Output 1
```
fig, axs = plt.subplots(1, 2, figsize=(10, 5))

axs[0].imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
axs[0].set_title('Original Image')

axs[1].imshow(edges, cmap='gray')
axs[1].set_title('Canny Edge Detection')

plt.show()
```
#### Penjelasan:
Pada bagian output 1 kita membuat visualisasi menggunakan Matplotlib untuk menampilkan dua hasil berbeda dari pemrosesan gambar. Dengan menggunakan `plt.subplots(1, 2, figsize=(10, 5))`, kita membuat sebuah figure dengan dua subplot yang disusun dalam satu baris dan dua kolom, serta ukuran keseluruhan gambar yang diatur menjadi 10x5 inci. Subplot pertama `(axs[0])` menampilkan gambar asli yang diambil dari file dan dikonversi dari format BGR (yang digunakan oleh OpenCV) ke format RGB (yang digunakan oleh Matplotlib) dengan `cv2.cvtColor(image, cv2.COLOR_BGR2RGB)`. Judul "Original Image" ditambahkan ke subplot ini menggunakan `set_title`. Subplot kedua (`axs[1]`) menampilkan hasil dari deteksi tepi menggunakan algoritma Canny yang dikonversi ke skala abu-abu dengan cmap='gray'. Judul "Canny Edge Detection" juga ditambahkan menggunakan `set_title`. Setelah kedua subplot diatur `plt.show()` digunakan untuk menampilkan figure ini.


#### 7). Menampilkan Output 2
```
fig, axs = plt.subplots(1, 3, figsize=(15, 5))

axs[0].imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
axs[0].set_title('Original Image')

axs[1].imshow(edges, cmap='gray')
axs[1].set_title('Canny Edge Detection')

axs[2].imshow(cv2.cvtColor(contour_image, cv2.COLOR_BGR2RGB))
axs[2].set_title('Contours Detection')

plt.show()
```
#### Penjelasan:
Pada bagian output 2 kita melakukan proses serupa untuk membuat visualisasi dengan tiga hasil pemrosesan gambar. Dengan `plt.subplots(1, 3, figsize=(15, 5))` kita membuat sebuah figure dengan tiga subplot yang disusun dalam satu baris dan tiga kolom, dengan ukuran keseluruhan gambar 15x5 inci. Subplot pertama `(axs[0])` kembali menampilkan gambar asli dalam format RGB dengan judul "Original Image". Subplot kedua `(axs[1])` menampilkan hasil deteksi tepi dalam skala abu-abu dengan judul "Canny Edge Detection". Subplot ketiga `(axs[2])` menampilkan gambar dengan kontur yang terdeteksi. Gambar ini dihasilkan dengan menggambar kontur pada gambar grayscale yang telah dikonversi kembali ke format BGR, sehingga garis kontur dapat diberi warna hijau. Judul "Contours Detection" ditambahkan ke subplot ini untuk memberikan konteks visual. Setelah semua subplot diatur, `plt.show()` digunakan untuk menampilkan figure dengan ketiga subplot ini.































