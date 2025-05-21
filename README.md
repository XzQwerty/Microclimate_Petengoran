## Struktur Folder

Berikut penjelasan direktori dan file utama yang dilacak Git dalam repositori ini:

### `i2c/`
Berisi folder terkait komunikasi sensor berbasis I2C.

- `test/`  
  Folder uji coba awal sensor I2C (jika terdapat file yang dilacak Git).
  
- `final/`  
  Folder finalisasi pembacaan sensor I2C. Saat ini hanya berisi file hasil kompilasi Python (`.pyc`) yang **tidak dilacak Git**.

### `rs485/`
Berisi folder terkait komunikasi sensor berbasis RS485.

- `test/`  
  Folder pengujian sensor RS485 (jika berisi file `.py` yang dilacak Git).
  
- `final/`  
  Folder finalisasi pembacaan sensor RS485. Saat ini hanya berisi file `.log`, `.json`, dan `.pyc` yang **tidak dilacak Git**.

### `uart/`
Folder untuk komunikasi berbasis UART (hanya file `.py` akan dilacak jika ada).

---

**Catatan:**  
Banyak file seperti `.log`, `.json`, `.pyc`, dan folder sementara seperti `__pycache__` telah dikecualikan dari pelacakan Git menggunakan `.gitignore`. Oleh karena itu, README ini hanya menjelaskan file dan folder yang **aktif dilacak Git**.
