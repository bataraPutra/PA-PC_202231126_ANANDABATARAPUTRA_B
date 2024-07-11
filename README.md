# PROJECT AKHIR UAS PENGOLAHAN CITRA DIGITAL 

## FILTERING CITRA

### GAMBAR ASLI
![https://github.com/bataraPutra/PA-PC_202231126_ANANDABATARAPUTRA_B/blob/main/myself.jpg](https://github.com/bataraPutra/PA-PC_202231126_ANANDABATARAPUTRA_B/blob/main/myself.jpg)


### Lokasi 
![https://github.com/bataraPutra/pcduasdokumentasi/blob/main/loc.jpg
](https://github.com/bataraPutra/pcduasdokumentasi/blob/main/loc.jpg)


### Source Code
1. Import Library
``` bash
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
2. Import Image
``` bash
image = cv2.imread('myself.jpg')
```
Penjelasan :
- cv2.imread('myself.jpg'): cv2 adalah singkatan dari OpenCV, sebuah pustaka komputer vision yang populer.
imread adalah fungsi dalam OpenCV yang digunakan untuk membaca gambar dari file.
- 'myself.jpg' adalah nama file gambar yang ingin dibaca. Ini bisa berupa path relatif atau absolut ke file gambar.
3. Image Shape
``` bash
image.shape
```
Penjelasan :
- image.shape adalah atribut dari array NumPy yang berisi informasi tentang dimensi array tersebut.
  
Output :

![https://github.com/bataraPutra/pcduasdokumentasi/blob/main/shape.png](https://github.com/bataraPutra/pcduasdokumentasi/blob/main/shape.png)

4. Baris Kolom
``` bash
(baris,kolom) = image.shape[:2]
```
Penjelasan :
- image.shape mengembalikan tuple dengan tiga elemen: (height, width, channels).
- image.shape[:2] mengambil dua elemen pertama dari tuple tersebut, yaitu height (tinggi) dan width (lebar).
- baris, kolom adalah variabel yang digunakan untuk menyimpan nilai tinggi dan lebar gambar.
5. Gray Image
``` bash
 gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
```
Penjelasan :
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2RGB) digunakan untuk mengonversi gambar dari format BGR ke RGB. Ini penting karena OpenCV membaca gambar dalam format BGR secara default, sementara matplotlib dan beberapa pustaka lain menggunakan format RGB

6. Citra Asli
``` bash
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.axis('on')
plt.show()
```
Penjelasan :
- plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB)): Menampilkan gambar yang telah dikonversi ke format RGB menggunakan matplotlib.
- plt.axis('on'): Mengaktifkan tampilan axis (sumbu x dan y) pada plot. Dalam hal ini, kamu bisa mengubahnya menjadi 'off' jika tidak ingin menampilkan sumbu.
- plt.show(): Menampilkan plot dengan gambar yang telah dipersiapkan.

Output :

![https://github.com/bataraPutra/pcduasdokumentasi/blob/main/citra%20asli.png](https://github.com/bataraPutra/pcduasdokumentasi/blob/main/citra%20asli.png)

7. Median Filtering
``` bash
image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
m, n, _ = image_rgb.shape
median_filtered = np.zeros_like(image_rgb)
for i in range(3):
    median_filtered[:, :, i] = cv2.medianBlur(image_rgb[:, :, i], 3)
fig, axis = plt.subplots(1, 2, figsize=(12, 6))
ax = axis.ravel()

ax[0].imshow(image_rgb)
ax[0].set_title('Original Image')
ax[0].axis('on')

ax[1].imshow(median_filtered)
ax[1].set_title('After Median Filtered Image')
ax[1].axis('on')

plt.show()
```
Output :

![https://github.com/bataraPutra/pcduasdokumentasi/blob/main/Screenshot%202024-07-10%20204630.png](https://github.com/bataraPutra/pcduasdokumentasi/blob/main/Screenshot%202024-07-10%20204630.png)

8. Mean Filtering
``` bash
citra = cv2.imread("myself.jpg")
citra = cv2.cvtColor(citra, cv2.COLOR_BGR2GRAY)
copyCitra1 = citra.copy().astype(float)

m1, n1 = copyCitra1.shape
output1 = np.empty([m1, n1])

print("Shape copy Citra 1 : ", copyCitra1.shape)
print("Shape copy Citra 1 : ", output1.shape)

print('m1 : ', m1)
print('n1 : ', n1)
print()
```
Penjelasan :
Kode ini memulai dengan memuat sebuah gambar bernama "myself.jpg" menggunakan OpenCV dan kemudian mengonversinya menjadi gambar grayscale. Setelah itu, gambar grayscale disalin ke dalam variabel copyCitra1 dan diubah tipe datanya menjadi float untuk memungkinkan operasi numerik yang lebih presisi. Dimensi gambar (jumlah baris m1 dan kolom n1) diperoleh dari shape copyCitra1, dan sebuah array kosong output1 dengan ukuran yang sama juga dibuat. Kode ini kemudian mencetak shape dari copyCitra1 dan output1 untuk memverifikasi ukuran kedua array tersebut, serta mencetak nilai m1 dan n1 yang merepresentasikan jumlah baris dan kolom gambar. Pada akhirnya, sebuah baris kosong dicetak untuk memberikan pemisah visual dalam output konsol.

Output :

![https://github.com/bataraPutra/pcduasdokumentasi/blob/main/Screenshot%202024-07-11%20204605.png](https://github.com/bataraPutra/pcduasdokumentasi/blob/main/Screenshot%202024-07-11%20204605.png)

``` bash
image_gray = cv2.cvtColor(image, cv2.COLOR_RGB2GRAY)
for baris in range(0, m1-1):
    for kolom in range (0,n1-1):
        a1 = baris
        b1 = kolom
        jumlah = copyCitra1[a1-1,b1-1] + copyCitra1[a1-1,b1] + copyCitra1[a1-1,b1+1] +\
        copyCitra1[a1+1,b1-1] + copyCitra1[a1,b1] + copyCitra1[a1,b1+1] +\
        copyCitra1[a1+1,b1-1] + copyCitra1[a1+1,b1] + copyCitra1[a1+1,b1+1]
        output1[a1, b1] = 1/9*jumlah
fig, axis = plt.subplots(1,2, figsize=(10,10))
ax = axis.ravel()

ax[0].imshow(image_gray, cmap='gray')
ax[0].set_title('Citra Asli')

ax[1].imshow(citra, cmap='gray')
ax[1].set_title('Mean Filtered')
plt.show()
```
Penjelasan :
Kode ini dimulai dengan mengonversi gambar berwarna menjadi gambar grayscale menggunakan fungsi cvtColor dari OpenCV. Kemudian, dilakukan perulangan ganda (nested loop) yang iterasi melalui setiap piksel dalam gambar (dari baris ke-0 hingga baris m1-2 dan dari kolom ke-0 hingga kolom n1-2). Pada setiap iterasi, dilakukan penghitungan rata-rata dari nilai intensitas piksel di sekitar piksel saat ini (termasuk piksel itu sendiri), mencakup piksel di posisi (a1-1, b1-1), (a1-1, b1), (a1-1, b1+1), (a1, b1-1), (a1, b1), (a1, b1+1), (a1+1, b1-1), (a1+1, b1), dan (a1+1, b1+1). Hasil penghitungan ini kemudian disimpan dalam array output1 di posisi yang sesuai. Setelah semua piksel diproses, hasilnya adalah gambar yang telah diterapkan filter rata-rata (mean filter). Gambar asli dan gambar yang telah difilter kemudian ditampilkan secara berdampingan menggunakan Matplotlib.

Output :

![https://github.com/bataraPutra/pcduasdokumentasi/blob/main/Screenshot%202024-07-11%20204804.png](https://github.com/bataraPutra/pcduasdokumentasi/blob/main/Screenshot%202024-07-11%20204804.png)

9. Show All Images
``` bash
fig, axs = plt.subplots(2, 2, figsize=(10, 10))

axs[0, 0].imshow(image_rgb)
axs[0, 0].set_title("Citra Asli")
axs[0, 0].axis('on')

axs[0, 1].imshow(median_filtered)
axs[0, 1].set_title("After Median Filter")
axs[0, 1].axis('on')

axs[1, 0].imshow(image_gray, cmap='gray')
axs[1, 0].set_title("Original Image")
axs[1, 0].axis('on')

axs[1, 1].imshow(citra, cmap='gray')
axs[1, 1].set_title("Mean Filtered Image")
axs[1, 1].axis('on')

plt.show()
```
Penjelasan :
Kode ini digunakan untuk menampilkan empat gambar secara berdampingan dalam satu jendela plot dengan menggunakan Matplotlib. Pertama, dua gambar dari langkah sebelumnya (image_rgb dan median_filtered) ditampilkan di baris pertama. Gambar pertama adalah gambar asli yang telah dikonversi ke RGB, sedangkan gambar kedua adalah hasil dari filter median yang diterapkan pada gambar tersebut.

Di baris kedua, dua gambar lainnya (image_gray dan citra) ditampilkan. Gambar pertama adalah gambar asli dalam skala abu-abu (grayscale), sementara gambar kedua adalah hasil dari filter rata-rata yang diterapkan pada gambar grayscale tersebut.

Output :

![https://github.com/bataraPutra/pcduasdokumentasi/blob/main/Screenshot%202024-07-11%20204948.png](https://github.com/bataraPutra/pcduasdokumentasi/blob/main/Screenshot%202024-07-11%20204948.png)
