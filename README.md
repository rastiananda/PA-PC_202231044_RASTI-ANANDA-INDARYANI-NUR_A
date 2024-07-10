
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
edges = cv2.Canny(gray_image, 50, 150)
```
#### Penjelasan:
Pada bagian ini `cv2.Canny` digunakan untuk deteksi tepi pada gambar. Parameter pertama adalah gambar input, parameter kedua dan ketiga adalah nilai ambang bawah dan atas untuk deteksi tepi. Nilai-nilai ini dapat disesuaikan sesuai dengan kebutuhan.


#### 5). Deteksi kontur
```
contours, _ = cv2.findContours(edges, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)
contour_image = image.copy()
cv2.drawContours(contour_image, contours, -1, (0, 255, 0), 2)
```
#### Penjelasan:
Pada bagian ini `cv2.findContours` digunakan untuk mendeteksi kontur pada gambar. Parameter pertama adalah gambar tepi yang dihasilkan oleh `cv2.Canny`, parameter kedua adalah mode pengambilan kontur (`cv2.RETR_TREE` digunakan untuk mengambil semua kontur dan membangun hirarki lengkap), dan parameter ketiga adalah metode aproksimasi kontur (`cv2.CHAIN_APPROX_SIMPLE` menyimpan hanya titik-titik penting). kemdian cv2.drawContours digunakan untuk menggambar kontur yang ditemukan pada gambar asli. Parameter pertama adalah gambar tempat kontur akan digambar, parameter kedua adalah kontur yang akan digambar, parameter ketiga adalah indeks kontur yang akan digambar (-1 berarti semua kontur), parameter keempat adalah warna kontur (`0, 255, 0` untuk warna hijau), dan parameter kelima adalah ketebalan garis.


#### 6). Menampilkan Output 1
```
plt.figure(figsize=(10, 5))

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.title('Original Image')

plt.subplot(1, 2, 2)
plt.imshow(edges, cmap='gray')
plt.title('Canny Edge Detection')

plt.show()
```
#### Penjelasan:
Pada bagian output 1, kita membuat sebuah figure dengan ukuran 10x5 inci untuk menampilkan dua subplot yang berisi gambar asli dan hasil deteksi tepi. Fungsi `plt.subplot(1, 2, 1)` digunakan untuk membuat subplot pertama dalam grid 1x2 (satu baris dan dua kolom). Pada subplot ini, kita menampilkan gambar asli yang telah dikonversi dari format BGR ke RGB menggunakan `cv2`.`cvtColor` agar dapat ditampilkan dengan benar oleh matplotlib. Gambar asli ini diberi judul "Original Image". Selanjutnya subplot kedua dibuat dengan `plt.subplot(1, 2, 2)`, di mana kita menampilkan gambar hasil deteksi tepi yang diperoleh dari algoritma Canny. Gambar ini diberi judul "Canny Edge Detection". dan kita menggunakan `plt.show()` untuk menampilkan kedua subplot dalam figure pertama.


#### 7). Menampilkan Output 2
```
plt.figure(figsize=(15, 5))

plt.subplot(1, 3, 1)
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.title('Original Image')

plt.subplot(1, 3, 2)
plt.imshow(edges, cmap='gray')
plt.title('Canny Edge Detection')

plt.subplot(1, 3, 3)
plt.imshow(cv2.cvtColor(contour_image, cv2.COLOR_BGR2RGB))
plt.title('Contours Detection')

plt.show()
```
#### Penjelasan:
Pada bagian output 2 kita membuat figure kedua dengan ukuran 15x5 inci untuk menampilkan tiga subplot yang berisi gambar asli, hasil deteksi tepi, dan hasil deteksi kontur. Fungsi `plt.subplot(1, 3, 1)` digunakan untuk membuat subplot pertama dalam grid 1x3 (satu baris dan tiga kolom), di mana kita menampilkan gambar asli yang dikonversi ke format RGB dengan `cv2.cvtColor`. Gambar asli ini diberi judul "Original Image" dan sumbu-sumbunya dihilangkan. Subplot kedua dibuat dengan `plt.subplot(1, 3, 2)`, di mana kita menampilkan gambar hasil deteksi tepi yang diberi judul "Canny Edge Detection" dan sumbu-sumbunya juga dihilangkan. Subplot ketiga dibuat dengan `plt.subplot(1, 3, 3)`, di mana kita menampilkan gambar hasil deteksi kontur yang ditambahkan ke gambar asli menggunakan `cv2.drawContours`. Gambar ini dikonversi ke format RGB sebelum ditampilkan dan diberi judul "Contours Detection, serta kita menggunakan `plt.show()` untuk menampilkan ketiga subplot dalam figure kedua. 































