---

# Sistem Pemantauan Iklim Mikro

## Gambaran Umum

Sistem Pemantauan Iklim Mikro adalah proyek yang dirancang untuk mengumpulkan dan memproses data lingkungan menggunakan berbagai sensor, seperti sensor curah hujan, sensor suhu dan kelembaban (DHT22, SHT31), sensor tekanan barometrik (BMP3XX), dan lainnya. Sistem ini memanfaatkan skrip **Python** dan pustaka **Arduino** untuk berinteraksi dengan sensor melalui protokol **I2C, UART, dan RS485**. Data dicatat dan diproses untuk analisis, terutama untuk aplikasi pemantauan iklim mikro.

Repositori ini berisi skrip untuk komunikasi sensor, pencatatan data, dan kontrol sistem, sebagian besar ditulis dalam **Python** dan **C++ (untuk Arduino)**. Proyek ini terstruktur untuk mendukung berbagai jenis sensor dan protokol komunikasi, dengan kode modular untuk skalabilitas.

---

## Struktur Direktori

Di bawah ini adalah struktur proyek, dengan fokus pada direktori dan file penting yang tidak diabaikan oleh `.gitignore`:

* **controller/**: Berisi skrip utilitas untuk kontrol sistem.
    * `restart_ssh.py`: Skrip untuk mengelola restart layanan SSH.

* **i2c/**: Skrip untuk komunikasi sensor berbasis I2C.
    * **final/**:
        * `atas.py`: Skrip untuk menangani data sensor tingkat atas.
        * `bmp00.py`: Skrip untuk berinteraksi dengan sensor tekanan barometrik BMP3XX.
        * `DFRobot_BMP3XX.py`: Pustaka untuk komunikasi sensor BMP3XX.
        * `sht31.py`: Skrip untuk berinteraksi dengan sensor suhu dan kelembaban SHT31.

* **rs485/**: Skrip untuk komunikasi sensor berbasis RS485.
    * **final/**:
        * `delete_log.py`: Utilitas untuk membersihkan log.
        * `mainA.py`: Skrip utama untuk sensor RS485 A (misalnya, anemometer, piranometer).
        * `mainB.py`: Skrip utama untuk sensor RS485 B.
        * `pyrano.py`: Skrip untuk data sensor piranometer.
        * `RainGauge_replacement.py`: Skrip untuk menangani data sensor curah hujan.
        * `rg.py`: Skrip pengukur curah hujan umum.

* **uart/**: Skrip untuk komunikasi sensor berbasis UART.
    * `example.py`: Skrip contoh untuk komunikasi UART.
    * `rgA.py`: Skrip untuk pengukur curah hujan A.
    * `rgB.py`: Skrip untuk pengukur curah hujan B.

* `dht22.py`: Skrip untuk berinteraksi dengan sensor suhu dan kelembaban DHT22.
* `relay.py`: Skrip untuk mengontrol modul relai.
* `README.md`: File ini, menyediakan gambaran umum proyek.

**Catatan**: Direktori seperti `log/`, `logger/`, `raingauge/`, `mics/`, `esptest/`, `DFRobot_RainfallSensor/`, `trash/`, dan `__pycache__/`, serta file dengan ekstensi `.log` dan `.json`, diabaikan oleh `.gitignore` dan tidak termasuk dalam repositori.

---

## Prasyarat

Untuk menjalankan skrip dan berinteraksi dengan sensor, pastikan dependensi berikut terinstal:

* **Python 3.x**: Diperlukan untuk menjalankan skrip Python.
    * **Pustaka**: `pyserial`, `smbus2`, `adafruit-circuitpython-dht` (untuk DHT22), dan pustaka khusus sensor lainnya.
    * Instal dependensi menggunakan:
        ```bash
        pip install pyserial smbus2 adafruit-circuitpython-dht
        ```

* **Arduino IDE**: Untuk mengkompilasi dan mengunggah file `.ino` (jika menggunakan sensor berbasis Arduino).
* **Perangkat Keras**:
    * **Raspberry Pi** atau mikrokontroler sejenis untuk menjalankan skrip Python.
    * **Sensor**: DHT22, SHT31, BMP3XX, sensor curah hujan, piranometer, anemometer, dll.
    * **I2C multiplexer** (misalnya, TCA9548A) untuk menangani beberapa perangkat I2C.
    * Antarmuka **RS485** dan **UART** untuk sensor masing-masing.

---

## Penyiapan dan Instalasi

1.  **Klon Repositori**:
    ```bash
    git clone <repository_url>
    cd Microclimate
    ```

2.  **Instal Dependensi Python**:
    Pastikan Python 3 terinstal, lalu jalankan:
    ```bash
    pip install -r requirements.txt
    ```
    (Buat file `requirements.txt` jika diperlukan, daftar dependensi seperti `pyserial`, `smbus2`, dll.)

3.  **Hubungkan Perangkat Keras**:
    * Hubungkan sensor ke antarmuka yang sesuai (I2C, UART, RS485) pada mikrokontroler Anda.
    * Pastikan pengkabelan yang benar untuk sensor seperti DHT22, SHT31, BMP3XX, dan pengukur curah hujan.
    * Jika menggunakan I2C multiplexer, konfigurasikan alamat di skrip yang relevan (misalnya, `sht31.py`, `bmp00.py`).

4.  **Jalankan Skrip**:
    * Untuk sensor I2C, navigasikan ke `i2c/final/` dan jalankan skrip seperti:
        ```bash
        python atas.py
        ```
    * Untuk sensor RS485, navigasikan ke `rs485/final/` dan jalankan:
        ```bash
        python mainA.py
        ```
    * Untuk sensor UART, navigasikan ke `uart/` dan jalankan:
        ```bash
        python rgA.py
        ```

---

## Penggunaan

* **Pengumpulan Data**:
    * Gunakan `atas.py` untuk data sensor tingkat atas (berbasis I2C).
    * Gunakan `mainA.py` dan `mainB.py` untuk sensor RS485 seperti anemometer dan piranometer.
    * Gunakan `rgA.py` atau `rgB.py` untuk pengukur curah hujan berbasis UART.

* **Kontrol Relai**:
    * Gunakan `relay.py` untuk mengontrol modul relai untuk mengalihkan perangkat.

* **Kontrol Sistem**:
    * Gunakan `controller/restart_ssh.py` untuk mengelola layanan SSH jika diperlukan.

---

## Catatan Penting

* Pastikan konfigurasi yang benar untuk alamat I2C dan ID *slave* RS485 di skrip masing-masing.
* Log dan file sementara (`.log`, `.json`) dikecualikan dari repositori agar tetap bersih.
* Untuk sensor berbasis Arduino, gunakan file `.ino` di direktori sensor masing-masing (misalnya, `DFRobot_RainfallSensor/examples/` jika tidak diabaikan).
* Periksa secara teratur kalibrasi sensor dan stabilitas koneksi untuk memastikan data yang akurat.
