# Python-2 Python unit testing

### ****Python unit testing****

Python birim testleri yazmak için 3 temel framework sunar.

- Unittest
- nose
- pytest

Birim testi örnek olarak pytest ile yapmak için öncelikle consol üzerinden indirmek gerekiyor. ( pip install pytest ) 

! testin yapılabilmesi için dosya isminin önünde test_ prefixi olmalı.

```python
# Basit bir birim test için çarpma ve toplama yapan iki fonksiyon yazılsın
# mathlib.py

def calc_total(a,b):
	return a+b

def calc_multipy(a,b):
	return a*b

# Test için de ayrı bir python dosyası oluşturuldu.
# test_mathlib.py

import mathlib # diğer dosya import edildi
def test_calc_total(): 
	total= mathlib.calc_total(4,5) # toplama fonksiyonu çağırılıyor.
	assert total == 9 # doğrulama ifadesi kullanılıyor. İşlem sonucu 9 olmalı.

def test_calc_multiply(): 
	multi= mathlib.calc_multiply(10,3) # çarpma fonksiyonu çağırılıyor.
	assert multi == 30 # doğrulama ifadesi kullanılıyor. İşlem sonucu 30 olmalı.

# testi başlatmak için command prompt üzerinden dosyanın bulunduğu dizine girilir
# ardından pytest kullanarak unit testi gerçekleştirilir. Bunun iki yolu var;

# 1-> Python -m pytest 
# bu komutla tekrar tekrar tüm dosyalara ve alt dizinlere gidecek ve test_ şeklindeki 
# bütün dosyalara test yürütecek. 
# eğer sorun yoksa işlem sonunda " 2 passed " ifadesi olacaktır.
 

# 2-> py.test 
# bu yürütmenin ayrıntılı çıktısı için -v eklemesi yapılır. 
# -v -> verbose
# bununla başarılı olup olmayan testlerin listesi gelir. 
```

### ****Python unit testing - skip/selectively run tests****

Bir testi çalışmadan geçmek için;

```python
# test_mathlib içerisindeki toplama testini çalıştırmadan geçmek için;

import mathlib
import pytest

# pytest içerisinde bulunan özel decorator'ü kullanarak
@pytest.mark.skip(reason="i dont want to run this for now") 
def test_calc_total(): 
	total= mathlib.calc_total(4,5)
	assert total == 9 

def test_calc_multiply(): 
	multi= mathlib.calc_multiply(10,3) 
	assert multi == 30 

# bu işlem sonrasında test çalıştırıldığında 1 test çalışır ve buna göre çıktı alınır.
# testi atlamanın nedenini görmek için ise komutta "-rxs" eklemesi yapılır.
# pytest -v -rxs
# bu komut ile ' i dont want to run this for now ' çıktısı alınır.

# Belirli bir koşul durumunda testi geçmek için;
# skipif kullanılır. 
# örneğin versiyonu belirli bir versiyondan büyükse çalışması isteniyor olsun.

import sys

@pytest.mark.skipif(sys.version_info < (3,5), reason="i dont want to run this for now")
def test_calc_total(): 
	total= mathlib.calc_total(4,5)
	assert total == 9  

# Testin ismine göre çalıştırmak istenirse komutta "-k" eklenir ve isim belirtilir.
# komut;
# pytest -k multiply 
# Bu ifade ile sadece multiply testi yapılacak

# pytest -k calc -v 
# yukarıdaki komut çalıştırıldığında iki test de çalışacak çünkü calc kelimesi ikisinde de bulunuyor.

# belirli bir kategoriye göre test yapılsın isteniyorsa;
# windows ve mac kategorileri için testler olduğu varsayılsın.

import pytest

def test_windows_1():
	assert True

def test_windows_2():
	assert True

def test_mac_1():
	assert True

def test_mac_2():
	assert True

# işletim sistemi windows olduğu için mac testlerinin geçilmesi gerekiyor olsun.
# bu tarz testlerin binlerce olduğu durumlar var tek tek isimlerle bu işlemleri yapmak
# imkansıza yakındı rbunun için bir decorator kullanılır.

@pytest.mark.windows
# buradaki windows biz tarafından oluşturulan özel bir etiket (herhangi bir isim olabilir)
def test_windows_1():
	assert True

@pytest.mark.windows
def test_windows_2():
	assert True

@pytest.mark.mac
def test_mac_1():
	assert True
@pytest.mark.mac
def test_mac_2():
	assert True

# bu decorator sayesinde testler kategorilenmiş olur.
# kategorilere göre çalıştırmak için ise "-m" komutu kullanılır.

# pytest -m windows -v
# bunun sonucunda 2 test çalışmış olur.

# seçilen kategori dısındakilerin çalışması gibi tersi bir işlem için
# "not" komutu eklenir.

# pytest -m "not windows" -v 
# 2 mac testi çalışmış olacak.

```

### Pytest fixtures framework

Basit Mock (fake) bir veritabanı oluşturulmuş olsun. 

```python
# mydb.py dosyasında mock sorgular olan bir veritabanı sorgusu var

class MyDB:
	def __init__(self):
		self.connection=Connection()
	def connect (self,connection_string):
		return self.connection

class Connection:
	def __init__(self):
		self.cur=Cursor()
	def cursor(self):
		return self.cur
	def close(self):
		pass

class Cursor():
	def execute(self,query):
		if query == "select id from eployee_db where name=John":
			return 123
		elif query == "select id from employee_db where name==Tom":
			return 789
		else:
			return -1
	def close(self):
		pass

# test_mydb.py dosyasında testler yazılacak
# 2 birim test yazılacak.
# 1. test -> John çalışanının kimliğini doğrulamak
# 2. test -> Tom çalışanının kimliğini doğrulamak

from fixtures.mydb import MyDB

def test_johns_id():
	db=MyDB()
	conn= db.connect("server") # server kısmı normalde uygun bağlantı dizesi olacak.
	cur =conn.cursor()
	id= cur.execute("select id from eployee_db where name=John") # sorgulamayla id alınacak
# ve bu id nin 123 olup olmadığı kontrol edilecek.
	assert id==123 

def test_tom_id():
	db=MyDB()
	conn= db.connect("server") # server kısmı normalde uygun bağlantı dizesi olacak.
	cur =conn.cursor()
	id= cur.execute("select id from eployee_db where name=Tom") # sorgulamayla id alınacak
# ve bu id nin 789 olup olmadığı kontrol edilecek.
	assert id==789

# bu test yürütüldüğünde iki test de geçecektir. 

# Ancak burada temel 2 sorun var 
# birinci sorun kod tekrarına düşülüyor.
# ikinciisi ise veritabanı bağlantısının maliyetli olduğu. 
# binlerce test durumunda bunlar zaman alacak ve bazı kaynakları boşa harcayacak.

# bu sorunları düzeltmenin 2 temel yolu var;
# 1 -> setup ve teardown metod kullanılır. (xunit)
# 2 -> fixtures kullanılır. Bu yöntem daha çok önerilir.

# 1. Yöntem 
conn =None
cur=None

def setup_module(module):
	global conn
	global curr
	db=MyDB()
	conn= db.connect("server")
	cur =conn.cursor()

# bu motod test durumlarından sonra yapılacak bazı işlemler için kullanılır.
def teardown_module(module):
	cur.close()
	conn.close()
# mydb.py dosyasındaki kapatma methodları çağırıldı.

def test_johns_id():
	id= cur.execute("select id from eployee_db where name=John")
	assert id==123 

def test_johns_id():
	id= cur.execute("select id from eployee_db where name=Tom")
	assert id==789
	
# bu işlem sonrasında iki test de çalışır. 

# 2. Yöntem 

import pytest

@pytest.fixture()
def cur():
	db=MyDB()
	conn=db.connect("server")
	cur=conn.cursor()
	return cur

def test_johns_id(cur):
	id= cur.execute("select id from eployee_db where name=John")
	assert id==123 

def test_johns_id(cur):
	id= cur.execute("select id from eployee_db where name=Tom")
	assert id==789

# Bu kod bloğunda cur isimli fonksiyon çağırılarak cur nesneleri alınacak  
# ve bu nesneler diğer fonksiyonlara parametre olarak gönderilecek 

# Bu işlemler sonucunda 2 test de çalışır.

# ancak bu haliyle sorun nesne seferinde veri tabanını oluşturuyor. 
# yani her test için fonksiyon yeniden çalıştırılıyor.
# bunun için eklenecek olan şey "scope" parametresidir.
# scope="module" ifadesiyle bu sadece bir kez kurulacaktır.
# ayrıca bağlantının kapatılması gerekiyor. Bunun için return yerine yield kullanılır.
# ardından da bağlantı kapatılır.

@pytest.fixture(scope="module")
def cur():
	db=MyDB()
	conn=db.connect("server")
	cur=conn.cursor()
	yield cur
	curs.close()
	conn.close()
# Bu işlemler sonrasından cursor objesi sadece bir kez oluşturulacak ve tüm testlere geçecek.
# Tüm test seneryoları bittikten sonra yield sonrasındaki kapatma ifadeleri çalışarak bağlantılar kapatılacak.

# 2. yöntemin avantajı global değişkenler oluşturmak zorunda kalınmıyor.
# ayrıca bu yöntem bağımlılık enjeksiyonu (dependency injection) konseptine uyumludur. 
```

### Bağımlılık enjeksiyonu (dependency injection)

Sınıfın ve nesnenin bağımlılıklardan kurtarılması amaçlanır. 

Bir sınıfın bağımlı olduğu nesneden bağımsız hareket edebilmesini sağlayabilir ve kod üzerindeki geliştirilmelerle değişiklik ihtiyacını kaldırmak amaçlanır.

özetle yazılımı oluşturan yapılar kaçınılmaz olarak birbirleri ile ilişkilidir. Ancak bu ilişkinin bir bağa ve sınırlandırmaya sebep olmaması için mümkün mertebe ilişkiyi gevşek tutmanın önemidir. (Loosely Coupled yani Gevşek Bağlılık)

Bundan dolayı yazılımı oluşturan yapıların birbirleri ile olan sıkı bağ azalacağı için uygulamaya yeni özellikler eklenip çıkartılabilmesi kolay hale gelir.

****Dependency Injection uygulamanın avantajları;****

- Bağımlılık oluşturacak nesneleri direkt olarak kullanmak yerine, bu nesneleri dışardan verilmesiyle sistem içerisindeki bağımlılığı minimize etmek amaçlanır.
- Unit testlerin yazımını kolaylaştırırken doğruluğunu da artırır. Yazılım geliştirmedeki en önemli konulardan biri de yazılım içerisinde bulunan componentlerin **“loosely coupled”** (gevşek bağlı) olmasıdır.
    
    Dependency Injection’da bunu sağlayabilen önemli tekniklerden birisidir. Böylece bağımsızlığı sağlanan sınıflar tek başına test edilebilir.