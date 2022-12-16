# Python Numpy

Numpy array’ler dizilere çok benzer.

Dizilerdeki gibi index ile arama yapılabilir ve bir çok diziyle ortak işlevleri vardır.

Numpy array’lerin normal dizilere göre önemli 3 faydası

(main benefits of numpy array over a python list)

- Az bellek (Less Memory)
- Hız (Fast)
- Uygunluk (Convinient)

```python
import numpy as np

# numpy array oluşturmak için;
a= np.arange(6).reshape(3,2) # 0-6 arasında sıralı sayılardan oluşan 3 satırlık ve 2 sütunluk matris oluşturur.
b= np.arange(6,12).reshape(3,2) # 6-12 arasında sıralı sayılardan oluşan 3 satırlık ve 2 sütunluk matris oluşturur

# iki diziyi vertical (dikey) virleştirerek bir dizi elde etmek 
np.vstack((a,b))
# array([[0, 1],
#			[2,3],
#			[4,5]
#			[6,7],
#			[8,9],
#			[10, 11]])

# bu birleştirmeyi horizontal (yatay) olarak yapmak için;
np.hstack((a,b))
# array([[0,1,6,7],
#				[2, 3, 8, 9],
#				[4, 5, 10, 11]])

# bir diziyi farklı uzunluklarda dizilere bölmek için
k=np.arange(30).reshape(2,15) # 2 satır 15 sütunluk bir dizi
# bu diziyi 3 farklı aynı boyutta diziye horizontal olarak bölmek için
result= np.hsplit(k,3)
# result[0]: 0-4,15-19 a kadar 1. 
# result[1]: 5-9,20-24 a kadar 2.
# result[2]: 10-14,25-29 a kadar 3.

# bu diziyi 3 farklı aynı boyutta diziye vertical olarak bölmek için
result= np.vsplit(k,2)
# result[0]: 0-14 e kadar 1.
# result[1]: 15-29 e kadar 2.

# bir dizinin elemanlarının belirli bir şartı sağlayıp sağlamadığı;
d= np.arange(12).reshape(3,4)
f= d> 4
# f true ve false dan oluşan d boyutunda bir matrix olur.
# 4 den büyükse -> True değilse False şeklinde

# f ile elde edilen diziyi d içerisinde yazdırıldığında değerler görülür.
d[f] 
# array ([5,6,7,8,9,10,11])

# 4 den büyük olan bu değerleri başka bir değerle değiştirmek için;
d[f]= -1

# martixi yazdırmanın iki yolu vardır. 
# C order ve Fortran order olarak.
# c order satırdaki elemanları teker teker yazar
# fortran order sütun elemanları teker teker yazdırır.
# bu işlemler için nditer(dizi,order="") komutu kullanılır.

a=np.arange(12).reshape(3,4)
for x in np.nditer(a,order="F"):
	print(x)
# 0,1,2,3,4,5,6,7,8,9,10,11

for x in np.nditer(a,order="F"):
	print(x)
# 0,4,8,1,5,9,2,6,10,23,7,11
```

nditer(dizi,order=”C” or “F”);

![Untitled](Python%20Numpy%20358679d6136946d78085d85a9ebaf411/Untitled.png)

 

```python
# nditer() fonksiyonunun bazı flags parametreleri var
# Örneğin dizinin elemanlarının kareleri alınarak güncellenmesi isteniyorsa;

for x in np.nditer(a, op_flags=['readwrite']):
	x[...]=x*x

```