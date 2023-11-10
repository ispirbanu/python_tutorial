# statistics beginner basic notes

### ****The average | Descriptive statistics | Probability and Statistics****

Ortalama | Tanımlayıcı istatistik | Olasılık ve İstatistik

****Descriptive (Tanımlayıcı):**** Diyelim ki çok fazla veri var ve bu verileri vermeden bundan bahsedilmek istendiğinde tüm verileri gözden geçirmeye gerek kalmadan tüm bu verileri bir şekilde temsil eden gösterge niteliğinde sayılar bulunabilir. Bunlar Tanımlayıcı istatistikler oluyor.

**Inferential (Çıkarımsal): B**ir şeyler hakkında sonuçlar çıkarmak için verilerin kullanıldığı zamandır. Örneğin seçimler için birkaç kesim üzerinde anketler yaparsak kesin sonucu alamayız ancak bazı matematiksel ifadeyle sonuçlar çıkartabiliriz.

## Descriptive

**Central Tendency - Average**

Bir sayının merkezi eğilimini veya ortalamasını ölçebileceğiniz bir sürü yol var. 

Mean, Median, Mode

Örneğin;

5 5 5 5 5 5 100 gibi bir veri kümesi olsun

Mean: 130/ 7 = 18.57 (Sayıların ortalaması)

Median: 5 (Büyükten küçüğe sıralı dizide ortadaki değer)

Mode: 5 (En çok tekrar eden değer.)

Basit bir örnek gibi görünebilir ancak bunu bir şehrin ev değerlerinin olduğu bir veri kümesi olarak düşünürsek. Evler benzer fiyatlarla verilirken bir ev ekstrem bir değere veriliyorsa ve ortalama olarak iki değere bakıldığında ortalama bizi yanlış yönlendirebilir ve ekstrem değer bir yanlış ölçüm olabilir bu yüzden bu yüzden bu üç değerin bilinmesi önemlidir. 

**Sample (Örneklem) and Population (popülasyon)**

Örneğin Amerikadaki erkeklerin ortalama boyunu bilmek istiyorsam. Amerikadaki tüm erkeklerin 15 milyon olduğunu varsayarsak gerçekten Amerikadaki erkeklerin boyunun ortalamasını bulmak imkansız denebilir çünkü bu ölçüm tamamlanana kadar bir kısmı ölebilir verilerin değeri değişiyor olacak.

Bu yüzden örneklemin ortalaması alınabilir. 

![Untitled](statistics%20beginner%20basic%20notes%207f79b3abd3d5451282cfd1a836f700aa/Untitled.png)

**μ: popülasyon ortalaması** 

**μ = ∑X / N**

**x̄: örneklem ortalaması** 

**x̄ = ( Σ xi ) ÷ n**
.

**Dispersion (Dağılım)**

2 2 3 3 ve 0 0 5 5 olarak iki veri kümesi düşünelim. 

**μ1= 10/4= 2.5** 

**μ2= 10/4= 2.5**

ikisinin ortalamasına bakarsak bu iki veri kümesine aynı diyebiliriz ama 1. kümedekilerin ortalamaya uzaklıkları 2. kümedeki elemanların ortalamaya uzaklıklarından daha yakındır. Yani ikinci küme dağınık kümedir. 

Bunların bu ölçüsünde **varyans (variance)** denir.

**σ**² **(variance): [Σ xi(xi -μ)**² ] **÷ N**

S**ample variance:  s**²= **[Σ xi(xi -x̄)**² ] **÷ (n-1)**

(Her sayı ile o kümenin ortalaması arasındaki mutlak mesafenin karesi.)

2 2 3 3

μ=2.5

**σ**2= [ (2-2.5)² + (2-2.5)² + (3-2.5)² + (3-2.5)² ] **÷** N

**σ**2 = 1**÷** 4 = 0.25

0 0 5 5 

μ=2.5

**σ**2= [ (0-2.5)² + (0-2.5)² + (5-2.5)² + (5-2.5)² ] **÷** N

**σ**2 = 24 **÷** 4 = 6.25

**Standard Deviation (Standart Sapma):**

**σ=** √ ∑(xi−μ)²**÷** N (populations)

![Untitled](statistics%20beginner%20basic%20notes%207f79b3abd3d5451282cfd1a836f700aa/Untitled%201.png)