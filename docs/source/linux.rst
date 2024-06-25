Setting dan Konfigurasi Linux
=============================
1. Konfigurasi Nama Device Menjadi Static dengan Udev
---------------------
Pengaturan nama device menjadi static dapat digunakan untuk mengatasi nama device berganti-ganti ketiga dihubungkan ke PC.
Misal, ketika USB kamera dihubungkan ke port USB yang berbeda biasanya device tersebut terindex pada ``/dev/video*``.
Jika nama device berubah maka program perlu penyesuaian dengan nama ini.
Untuk memudahkan, dapat dilakukan pengaturan pada Udev dengan melakukan symbolic link ke nama tertentu berdasarkan Product ID dan Device ID.

**Langkah Konfigurasi**:

1. Buka terminal kemudian ketikkan perintah berikut ``udevadm info /dev/video0 | grep ID``. Catat ``ID_VENDOR_ID`` dan ``ID_PRODUCT_ID``.
2. Buat file ``camera.rules`` di direktori ``/etc/udev/rules.d/`` dengan perintah ``sudo touch /etc/udev/rules.d/camera.rules``
3. Edit file ``camera.rules`` menggunakan text editor dengan perintah ``sudo nano /etc/udev/rules.d/camera.rules``.
  Edit file menjadi berikut ini.

  .. code-block:: shell

    SUBSYSTEM=="video4linux", ATTRS{idVendor}=="1234", ATTRS{idProduct}=="5678", SYMLINK+="head_cam"
  Pastikan ``1234`` dan ``5678`` pada file tersebut disesuaikan dengan ``ID_VENDOR_ID`` dan ``ID_PRODUCT_ID`` dari device yang dihubungkan.
4. Reload rules yang telah dibuat dengan perintah berikut ``sudo udevadm control --reload-rules``
5. Trigger rules dengan perintah berikut ini ``sudo udevadm trigger``

**Verifikasi Konfigurasi**

Untuk melakukan verifikasi ketikkan perintah berikut pada terminal ``ls /dev/ | grep head_cam``. Pastikan pada terminal muncul device dengan nama ``/dev/head_cam``.


2. Setting CPU Isolation
------------------------
3. Setting Latency Timer
------------------------
