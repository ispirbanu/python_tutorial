# OOP (Nesne Tabanlı Programlama)

Eski programlama dilleriyle oluşturulan programlar bir dizi talimatlardan ibaret olarak yazılıyordu.

Programı modüler hale getirmek için prosedürlerden  ve alt programlardan yararlanılırdı. Bu programlamalar veriden çok mantığa odaklanırdı. 

Object-Oriented Programming (OOP) yani Nesne yönelimli programlama yazılımın tasarımını işlevler ve mantık yerine, veriler ve nesneler ile düzenleyen bir programlama modelidir.

Nesne, benzersiz nitelikleri ve davranışı olan bir veri alanı olarak tanımlanabilir.

Nesne, programınızda modellemek istediğiniz bir şey veya fikirdir. Bir nesne herhangi bir şey olabilir, örneğin, çalışan, banka hesabı, araba vb.

Java, C#, Pythonve C++ gibi modern programlama dilleri Nesne yönelimli bir yaklaşım izler. 

### ****Nesne yönelimli programlamanın yapısı****

**Sınıf (Class),** nesne oluşturmak için bir plandır. Nitelikleri ve davranışı tanımlar.  

**Nesneler (Object)** , özel olarak tanımlanmış verilerle oluşturulmuş bir sınıfın örnekleridir.

**Yöntemler (Methods),** bir nesnenin davranışlarını tanımlayan bir sınıf içinde tanımlanan işlevlerdir. Sınıf tanımlarında yer alan her yöntem, bir örnek nesneye yapılan başvuruyla başlar. Ek olarak, bir nesnede bulunan alt programlara örnek yöntemler denir.

**Nitelikler(Attributes)** , sınıf şablonunda tanımlanır ve bir nesnenin durumunu temsil eder. Nesneler, nitelikler alanında saklanan verilere sahip olacaktır. Sınıf nitelikleri sınıfın kendisine aittir.

Nesne yönelimli programlama denildiğinde akla ilk gelen gerçek dünya örneği bir araba programıdır.

Bir araba modellenecekse o arabanın yakıt, model, marka gibi nitelikleri ve kalkış, hızlanma gibi davranışları tanımlanabilir. Bunlarla araba genelleştirilmeye çalışılıyor. Daha sonra bu sınıfı nesneler oluşturmak için kullanırken beliri ayrıntılara sahip araba nesneleri oluşturuşturulur.

![Untitled](OOP%20(Nesne%20Tabanl%C4%B1%20Programlama)%201a01a9280ef5496e90454a8bc16edf70/Untitled.png)

### OOP'nin temel ilkeleri

**Soyutlama (Abstraction),** birbirleriyle bir şekilde etkileşime girebilen bağımsız modüller oluşturmaya, zaman içinde ek değişiklikleri veya eklemeleri daha kolay yapmasına yardımcı olur.

**Kapsülleme (Encapsulation),** Bu ilke, tüm önemli bilgilerin bir nesnenin içinde bulunduğunu ve yalnızca belirli bilgilerin açığa çıktığını belirtir. 

Her nesnenin uygulaması ve durumu, tanımlanmış bir sınıf içinde özel olarak tutulur. Diğer nesnelerin bu sınıfa erişimi veya değişiklik yapma yetkisi yoktur. Yalnızca genel işlevlerin veya yöntemlerin bir listesini çağırabilirler. 

Veri gizlemenin bu özelliği, daha fazla program güvenliği sağlar ve istenmeyen veri bozulmasını önler, bütünlüğü korur.

**Miras (Inheritance),** Kalıtım, Nesne yönelimli programlama dillerinin güçlü bir özelliğidir. Kalıtım, sınıfları bir hiyerarşide düzenlemeye ve bu sınıfların, hiyerarşide yukarıdaki sınıflardan nitelikleri ve davranışları devralmasını sağlamaya yardımcı olur.

Kalıtım ile ortak bir uygulama/davranış tanımlanabilir ve daha sonra özel sınıflar için bunu değiştirilebilir veya özel bir şeye dönüştürülebilir. Kalıtım geriye doğru çalışmaz.

Gereksiz kod tekrarını önleyebilir.

**Polimorfizm, bilgisayar sistemlerinin, oluşturulan yeni özel nesnelerle genişletilmesine izin verirken, sistemin mevcut bölümünün yeni nesnelerin belirli özellikleriyle ilgilenmeden yeni bir nesneyle etkileşime girmesine izin verir.**

Örneğin;

bir kağıda bir mesaj yazmanız gerekiyorsa, bir tükenmez kalem, kurşun kalem, kullanılabilir. Sadece kullanılan eşyanın tutulabilecek boyutta olması ve kağıda bastırıldığında iz bırakabilmesi yeterlidir. Dolayısıyla yazma eylemi, kağıt üzerinde bir işaret yapmanıza yardımcı olur ve hangi işaretlemenin veya yazma aracının kullanılacağı bir karar meselesidir. 

Başka bir örnek, bir uçak ve uzay mekiğidir, her ikisi de Uçan nesneler olarak adlandırılabilir. Ancak her ikisinin de uçma amacı farklıdır, yani uygulamada bir fark vardır. Ancak bir izleyicinin bakış açısından her iki nesne de uçabilir.

### ****OOP'nin Faydaları****

- M**odülerlik - Modularity**
    
    Kapsülleme, nesnelerin bağımsız olmasını sağlayarak sorun gidermeyi ve işbirliğine dayalı geliştirmeyi kolaylaştırır.
    
- **Tekrar Kullanılabilirlik - Reusability**
    
    Kod, kalıtım yoluyla yeniden kullanılabilir, yani bir ekibin aynı kodu birden çok kere yazılması gerekmez.
    
- **Verimlilik - Productivity.**
    
    Programcılar, birden çok kitaplık ve yeniden kullanılabilir kod kullanarak yeni programları daha hızlı oluşturabilir.
    
- **Kolayca yükseltilebilir ve ölçeklenebilir - Easily upgradable and scalable**
    
    Programcılar, sistem işlevlerini bağımsız olarak uygulayabilir.
    
- **Arayüz açıklamaları - Interface descriptions**
    
    Nesnelerin iletişimi için kullanılan mesaj aktarma teknikleri nedeniyle, harici sistemlerin açıklamaları basittir.
    
- **Güvenlik - Security**
    
    Kapsülleme ve soyutlama kullanılarak karmaşık kod gizlenir, yazılım bakımı daha kolaydır ve internet protokolleri korunur.
    
- **Esneklik - Flexibility**
    
    Polimorfizm, tek bir fonksiyonun yerleştirildiği sınıfa uyum sağlamasını sağlar. Farklı nesneler de aynı arayüzden geçebilir.