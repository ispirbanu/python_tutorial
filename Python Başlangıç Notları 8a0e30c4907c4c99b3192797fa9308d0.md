# Python Başlangıç Notları

## Dosya İşlemleri

open() fonksiyonu sayesinde bir dosyayı açabilir üzerinde okuma yazma işlemleri yapılabilir.

```python
# open("file name and path", "file open mode")
f=open("dosyayolu", "w")
f.write("yazılacak metin")
# w--> write- yazma işlemidir. Dosya açılarak üzerinde yazma işlemi yapılır.
# ancak var olan dosyada yazma işlemi yapılırken önceden var olan bilgiler silinerek 
# üzerine yazma işlemi yapar.

f= open("doysayolu", "r")
# r --> read- okuma işlemidir. Bununla istenilen dosya açılarak okuma işlemi yapılabilir.
# read(), readline(), readlines() olarak 3 metot vardır.
f.read()  # -> dosyanın bütün içeriğini veriyor.
f.readline() #-> dosyayı satır satır okuyor ve satır bittiğinde boş eleman dönderiyor. 
f.readlines() #-> dosyanın satırlarının tamamını okuyarak liste şeklinde dönderiyor. 

f= open("dosyayolu", "a")
# a --> appending- ekleme işlemidir. 
# Dosyayı silmeden üzerinde ekleme veya değişiklik yapmak için kullanılır.
f.write("eklenecek metin")

f.close()
```

dosya okumanın bir diğer yöntemiyle de dosyayı kapatma işlemi yapmaya gerek kalmaz. Dosya otomatik kapanır. 

```python
with open("dosyayolu","r") as f: 
	print(f.read())
# bu işlem sonrasında f.close() kullanılmaya gerek yoktur .

print(f.closed()) # dosyanın kapalı mı açık mı olduğunu görmek için kullanılır.
# True --> Dosya kapalı
# False --> Dosya açık
```

## __name__ == __main__

pythonda her modülün __**name**__ özelliği vardır.

Program doğrudan çalıştırıldığında __name__ değeri __**main**__ değerine atanır.

Eğer başka modül (import edilerek) çalıştırılırsa __name__ değerine modulun ismi atanır. 

 __name__ == __main__ ifadesiyle python tarafından ana dosyadan mı yoksa başka dosyadan mı çalıştığı kontrol edilebilir.

```python

# area.py dosyası içerisinde;
def calculate_area(base, height):
		print("__name__:" , __name__)
		return 1/2*(base*height)

if __name__=="__main__":
	print(" in area.py")
	a= calculate_area(10,20)
	print("area: ",a)

# Bu dosya çalıştırıldığında çıktı sırasıyla;

# in area.py
# __name__: __main__
# area: 100.0
```

```python

# caller.py dosyası içerisinde;
import area
print(" in caller.py")
area.calculate_area(5,10)

# area dosyası import edilerek bu dosya çalıştırıldığında çıktı;

# in caller.py
# __name__: area

# şeklinde çıktı alınır. 
```

```python
# __name__ özelliğini tekrar kontrol ettiğimiz basit bir örneğe bakarsak;

if __name__== "__main__":
	print("ana dosyada çalıştırıldı."(
else:
	print("bir dosya tarafından çalıştırıldı.")

# şeklinde bakılarak kontroller sağlanabilir 
# ve bunlara göre gerekli işlemler yapılabilir. 
```

### Sınıf işlemleri

Sınıflar, kullanıcı tanımlı veri yapıları oluşturmak için kullanılır. Sınıflar , sınıftan oluşturulan bir nesnenin verileriyle gerçekleştirebileceği davranışları ve eylemleri tanımlayan, yöntemler adı verilen işlevleri tanımlar .

Sınıf, bir şeyin nasıl tanımlanması gerektiğine dair bir plandır. Aslında herhangi bir veri içermez.

```python
# Sınıf tanımlama;
class SinifAdi:
	pass

# __init__ nesnenin özelliklerinin değerlerini atayarak başlangıç durumunu ayarlar.

class User:
	def __init__(self, name, age):
		self.name= name
		self.age=age 

# sınıf nitelikleri isi tüm sınıf örnekleri için aynı değere sahip olan niteliklerdir.
# Bunlara her zaman bir başlangıç değeri atanmalıdır.
# Sınıfın bir örneği oluşturulduğunda, sınıf öznitelikleri otomatik olarak oluşturulur ve başlangıç değerlerine atanır.
# Her sınıf örneği için aynı değere sahip olması gereken özellikleri tanımlamak için sınıf özniteliklerini kullanılır.

class User: 
	gender:"Women" # bu sınıftaki tüm özellikler için geçerli olacaktır.

	def __init__(self, name, age):
		self.name= name
		self.age=age 

# nesne oluşturmak;
nesne= User("isim", 3)

# özelliklere ulaşmak;
nesne.name # --> 'isim'
nesne.age # --> 3
nesne.gender # --> 'Women'

# Niteliklerin var olduğu garanti edilse de, değerleri dinamik olarak değiştirilebilir;
nesne.age=20
nesne.age # --> 20
nesne.gender= "Man" 
nesne.gender # --> 'Men'

```

### Argparse Modülü

Yazılan her program grafik arayüzüne sahip olmayabilir. Bu uygulamalar için komut satırı daha uygundur ve bu uygulamalara bazı parametreler gerekebilir. argparse kullanıcıdan alınan parametreler için yardım mesajları, nasıl kullanıldığı mesajları üretir. 

```python
import argparse

# ayrıştırıcı kullanmak için ArgumentParser üzerinden bir nesne oluşturulur.

parser= argparse.ArgumentParser(description=" Uygulamanın tanımı") 
# açıklama yapılmayabilir.

# Argümanları eklemek için add_argument() fonksiyonu kullanılır.
# örnek olarak iki sayıyla bir işlem yapmak için argüman oluşturulursa; 
parser.add_argument("number1", help="first number")
parser.add_argument("number2", help="second number")
parser.add_argument("operation", help=" operation") 

# seçenekleri belirtmek için help sonrasında choices ile işlemlerin neler olduğu gösterilebilir.
parser.add_argument("operation", help= "operation", choices=["add", "subtract","multiply"]) 
# bu durumda farklı bir değer girildiğinde hatada 
# choose from 'add','subtract','multiply' şeklinde uyarı olacak. 

args=parser.parse_args() # argümanları ayrıştırmayı sağlar.

print(args.number1)
print(args.number2)
print(args.oparation)

# number1 first number
# number2 second number
# operation operation

# burada sayılar girilirse bize vereceği çıktılar;

# 4
# 5
# add 

#İşlemleri eklersek;

n1= int(args.number1)
n2= int(args.number2)
result=None
if args.operation == "add":
	result= n1+n2
if args.operation == "subtract":
	result= n1-n2
if args.operation == "multiply":
	result= n1*n2
print(result) 

# burada tekrar 4, 5 ve add değerleri verilirse çıktılar; 
# 4
# 5
# add 
# 9 

# Argümana eksik değer gönderildiğinde bir hata alırız çünkü bu durumda eksik argüman gönderilemez.
# Bu yüzden argüman kullanırken kaç değer varsa o kadar argümanı sağlamak gerekir.
# bazı argümanlar atlanmak isteniyorsa bu değerler opsiyonel olarak belirtilmelidir.
# argümana eklenen değerin başına getirilen "--" ifadesi bunu sağlar.

parser.add_argument("--number1", help="first number")
parser.add_argument("--number2", help="second number")
parser.add_argument("--operation", help=" operation")

# Yukarıdaki bütün argümanlar isteğe bağlı olacak.

n1= int(args.number1)
n2= int(args.number2)
result=None
if args.operation == "add":
	result= n1+n2
if args.operation == "subtract":
	result= n1-n2
if args.operation == "multiply":
	result= n1*n2
else:
	print("unsupported operation")

print(result) 

# --number1 4 --number2 5 şeklinde veriler girildiğinde çıktısı;
# 4
# 5 
# unsupported operation
# result None

# Bu işlemleri command'da değilde pycharm üzerinde değerleri denemek için ise
# "run" kısmından "edit Configurations" üzerinden "script parameters" bölümüne değerleri
# girerek çalıştırılabilir.
```

### Decorators

Programcıların bir işlevin veya sınıfın davranışını değiştirmesine izin verdiği için Python'da çok güçlü ve kullanışlı bir araçtır. 

Dekoratörler, sarılmış fonksiyonun davranışını kalıcı olarak değiştirmeden genişletmek için başka bir fonksiyonu sarmalamaktır.

```python
# Örneğin sayıların küpünü ve karesini alan 2 farklı fonksiyon olsun ve 
# Bu fonksiyonların zamanlamasını ölçmek isteyelim.

import time
def calc_square(numbers):
	start=time.time()
	result=[]
	for number in numbers:
		result.append(number*number)
	end=time.time()
	print ("calc_square took " + str((end-start)*1000))
	return result

def calc_cube(numbers):
	start=time.time() # işlem öncesi zaman alınır
	result=[]
	for number in numbers:
		result.append(number*number*number)
	end=time.time() # işlem sonundaki zaman alınır 
	print ("calc_cube took " + str((end-start)*1000)) # saniye cinsinden yazdırmak
	return result

array = range (1,1000000)
out_quare=calc_square(array)
out_cube=calc_cube(array)

# Burada her bir fonksiyonun verilen dizi için hesaplamalarını yaptıktan sonra
# Geçen süresini ekrana yazdırıyoruz ancak hem kod tekrarı var
# Hemde kod karmaşık ve uzun görünüyor.
# Bunun yerine Generatorler kullanıldığında kodlar daha düzenli ve tekrardan uzak 
# bir şekilde istenilen program oluşturulmuş oluyor.

```

```python
# Yukarıdaki kodun aynısını generatorlerle oluşturmak;

import time

def time_it(func):
	def wrapper(*args, **kwargs):
		start=time.time()
		result= func(*args,**kwargs)
		end= time.time()
		print (func.__name__ + " took "+ str((end-start)*1000)+ " mil sec")
		# __name__ fonksiyonun adını verecek.		
		return result
	return wrapper

@time_it 
# sarmalayıcı fonksiyon başta yazılır.
# ile yukarıdaki fonksiyon çalışarak aşağıdaki fonksiyon için hesaplama yapacaktır
def calc_square(numbers):
	result=[]
	for number in numbers:
		result.append(number*number)
	return result

@time_it
def calc_cube(numbers):
	result=[]
	for number in numbers:
		result.append(number*number*number)
	return result

```

### *args ve **kwargs

**“*args”,** Sınırsız sayıda parametreli fonksiyon oluşturmak için parametremizin önüne tek yıldız (*) koyulur. 

fonksiyona verilecek değerin, dizinin uzunluğu vs değiştirildiğinde program çalışmaya devam eder.

 

```python
def show_numbers(*numbers):
	print(numbers)

show_numbers(1,2,3,4)
show_numbers(15,'number',3)

# şeklinde de olsa program çalışacakır.
# Burada, fonksiyon parametresinden önce tek yıldız(*) kullanıldığında sonuç tuple olarak döner.
```

“******kwargs”,**** Çift yıldızlı (**) parametrelerin tek yıldızlı (*) parametrelerden en önemli farkı, fonksiyonu çağırırken anahtar değer ilişkisiyle çağırabilmemizdir.

```python
def show_numbers(**number):
	print(number)

show_numbers(number1=1,number2=2,number3=3, number4=4, number5="seven", number6="eleven")

# Burada, fonksiyon parametresinden önce çift yıldız(**) kullanıldığı için sonuç sözlük (dictionary) olarak döner.
# Parametre ismi yani yukarıda number dediğimiz kişiye göre değişebilir. 
# Ama **kwargs gelenekselleşmiştir. 
# Python kodumuzun kullanıcılar tarafından hem daha rahat anlaşılabilmesi için hem de okunabilirliğini arttırabilmek için 
# kişisel parametre ismi yerine **kwargs kullanımı önemlidir.

# Aynı durum *args için de geçerlidir.

```