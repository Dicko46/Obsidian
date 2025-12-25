1. `len()` - menghasilkan panjang dari sebuah string,
2. `lower()` - menghasilkan string dengan karakter huruf kecil,
3. `upper()` - menghasilkan string dengan karakter huruf kapital.

```python
fakta = "Belajar Python di CodeSaya itu menyenangkan..!"

print len(fakta)

print fakta.lower()

print fakta.upper()
```

contoh format print untuk mengisi {} secara berurutan

```python
nama = "Komodo"
spesies = "kadal"
tempat = "Nusa Tenggara"

print "{} adalah spesies {} terbesar di dunia yang hidup di {}.".format(nama, spesies, tempat)

print (f"{nama}{spesies}{tempat}") # python3 / now
```
 Nilai pada python dimulai dari 0

cara import datetime
```python
from datetime import datetime

sekarang = datetime.now()
print sekarang # bisa tambahkan sekarang.year/month/day

```
 
 datetime.now() bisa menghasilkan :
 year, month, day, hour, minute, second
 