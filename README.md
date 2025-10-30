# Klasifikasi Gambar Kucing dan Anjing menggunakan model Convolutional Neural Network (CNN)
Pada proyek ini dilakukan pelatihan model CNN untuk klasifikasi gambar kucing dan anjing. Adapun daaset yang digunakan adalah dataset yang dapat anda download dari website Kaggle

Link dataset: https://www.kaggle.com/datasets/tongpython/cat-and-dog

## Tujuan
Adapun tujuan pembuatan proyek ini adalah sebagai bahan edukasi tentang pengaplikasian model deep learning CNN untuk klasifikasi data gambar. 

## Panduan

Untuk clone repository ini anda dapat menggunakan command berikut
```bash
git clone https://github.com/ramadhaykp12/cat-dog-image-classification.git
cat-dog-image-classification
```

Untuk mengunduh dataset gambar dari Kaggle, anda memerlukan kredensial Kaggle API. Anda bisa mendapatkannya dengan cara membuat akun Kaggle, lalu klik logo profil. Setelah itu anda masuk ke settings, cari bagian API, dan klik create new token. Jika sudah maka akan anda akan mendownload sebuah file json. 
Jika sudah ada fie kaggle.json, anda bisa upload file json menggunakan code berikut
```python
from google.colab import files

files.upload()
```

Setelah itu untuk mendownload dataset dari Kaggle anda dapat menjalankan beberapa command berikut
```bash
# Menyiapkan file kredensial Kaggle API
! mkdir -p ~/.kaggle
! cp kaggle.json ~/.kaggle/
! chmod 600 ~/.kaggle/kaggle.json
# Download dataset dari Kaggle
! kaggle datasets download -d tongpython/cat-and-dog
```

Jika sudah, selanjutnya anda harus ekstrak file zip yang terdownload
```bash
! unzip /content/cat-and-dog.zip
```

Data siap digunakan, anda sudah bisa menjalankan code yang ada untuk melatih model. Jika anda ingin menggunakan model yang sudah dilatih anda dapat menjalankan memuat model yang sudah saya latih seperti berikut
```python
model = tf.keras.models.load_model('/content/trained_model.h5')
```
Sebelum menjalakan code diatas, pastikan anda sudah upload model ke Google Colab atau pastikan model sudah dalam satu directory dengan notebook.  
Untuk menguji model dengan data baru, anda dapat upload satu atau beberapa gambar sesuai dengan class atau label yang ada yaitu anjing dan kucing, lalu jalankan code berikut untuk memulai prediksi.
```python
img = 'file_gambar_anda.jpg'
img = image.load_img(img, target_size=(64, 64))

# ubah gambar menjadi array
img_array = image.img_to_array(img)
img_array = np.expand_dims(img_array, axis=0)
img_array /= 255.0

# prediksi
prediction = model.predict(img_array)
if prediction[0][0] > 0.5:
    print('Anjing')
else:
    print('Kucing')

# tampilkan gambar
plt.imshow(img)
plt.show()
```
