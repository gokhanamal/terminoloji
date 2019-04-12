
Transleted from [Reading 17: Concurrency](http://web.mit.edu/6.005/www/fa14/claşses/17-concurrency/)

# Concurrency (Eşzamanlılık)

Eşzamanlılık, birden fazla hesaplama işleminin aynı anda medyana gerçekleşmesi anlamına gelir. Hoşumuza gitse de gitmese de, modern progralama dünyasında eşzamanlılık heryerde karşımıza çıkabilir :

- Bir ağdaki birden fazla bilgisayarda
- Bir bilgisayarda çalışan birden fazla uygulamada
- Bir bilgisayardaki birden fazla işlemcide (günüzmüzde, bir cipteki birden fazla işlemci çekirdeğinde )

Aslına bakarsak, eşzamanlılık modern programlama dündyasının olmazsa olmazlardandır :

- Web siteleri birden fazla eşzamanlı kullanıcı ile başa çıkmak zorundadır.
- Mobil uygulamalar bazı işlemlerini sunucularda yapma ihtiyacı duyarlar.
- Grafiksel kullanıcı arayüzları (GUI), kullanıcı deneyimini kesintiye uğratmamak için nerdeyse herzaman işlemleri arkaplanda yapmaya ihtiyaç duyar.

Eşzamanlı programlama yapabilmek gelecekte de önemini korumaya devam edecek. İşlemcilerin döngü hızları azami seviyeye ulaştığı için artık döngü hızlarını arttırmak yerine
her yeni nesil yongada daha çok sayıda çekirdek kullanıyoruz. Böylece gelcekte de, daha hızlı hesaplamalar yapabilmek için, hesaplamaları eşzamanlı parçalara ayıracağız.

### Eşzamanlı Programlama Modelleri

Eşzamanlı programlamada yaygın olarak iki ayrı model kullanılıyor: *shared memory* (ortak hafıza) and *message passing* (ileti geçişi)

**Ortak Hafıza :** Eşzamanlılığın ortak hafıza modelinde, eşzamanlı modüller hafızadaki ortak bir nesneye okuma ve yazma işlemleri yaparak birbirleri ile etkileşime geçerler.

![Shared-Memory](shared-memory.png)

Ortak hafıza modeli için örnekler :

- A ve B aynı bilgisayarda aynı hafızayı paylaşan iki farklı işlemci (işlemci çekirdiği) olabilir.
- A ve B aynı bilgisayarda çalışan, okuma ve yazma işlemi yapabileceği dosyalarla birlikte ortak bir dosya sistemini paylaşan iki farklı uygulama olabilir.
- A ve B aynı java programında, aynı java nesnenisini paylaşan iki farklı thread (thread'in ne anlama geldiğini aşgida açıklayacağız) olabilir.

**İleti Geçişi :** İleti geçişi modelinde, eşzamanlı modüller birbirlerine iletişim kanalları aracılığı ile mesajlar  göndererek etkileşime geçerler. Modüller mesaj gönderir ve her modüle gelen mesajlar kullanılmak için sıraya sokulur.

![Message-Passing](message-passing.png)

İleti Geçişi için örnekler:

- A ve B, ağ bağlantıları ile iletişime geçen, aynı ağdaki iki bilgisayar olabilir.
- A ve B, bır web tarayıcı ve bir web sunucu olabilir. A, B'ye bir web sayfası için bağlantı isteği gönderir, ve B web sayfası için gerekli datayı A'ya cevap olarak geri gönderir.
- A ve B anlık mesajlaşma istemcisi ve sunucu olabilir.
- Ave B, girdi ve çıktıları birbirlerine komut istemcisine yazılan `ls | grep` gibi bir veri yolu (pipe) ile bağlanmış bir bilgisayarda aynı anda çalışan iki ayrı program olabilir. 

### Prosesler(Processes), İş Parçacıkları (Threads), Zaman Dilimleme(Time-slicing)

İleti gönderimi ve ortak hafıza modelleri eşzamanlı modullerin nasıl iletişim kurdukları ile ilgililerdir. Eş zamanlı moduller iki farklı türde karşımıza çıkar: prosesler ve iş parçacıkları.

**Proses :** Proses, aynı makinede, diğer süreçlerden izole edilmiş bir şekilde çalışan programın bir kopyasıdır. En önemlisi , proses makine hafızasında özel bir bölüme sahiptir.

Proses soyutlaması bir sanal bilgisayardır. Sanal bilgisayar, çalıştırdığın program tüm makineye sahipmiş gibi hissetmeni sağlar. Sadece o programı çalıştırmak için yeni bir hafıza ile yeni bir bilgisayar oluşturmuşun gibi hissettirir.

Tıpkı ağa bağla bilgisayarlarda olduğu gibi, prosesler normalde birbirleri arasında ortak bir hafıza kullanmazlar. Bir proses hiçbir zaman diğer bir prosesin nesnelerine veya hafızasına erişemezler. Prosesler arasında hafıza paylaşım bir çok işletim sisteminde mümkün ancak bu işlem özel bir efor gerektiriyor. Aksine, yeni bir proses otomatik olarak mesaj göndermek için hazırdır çünkü proses standart girdi ve çıktı akışları ile birlikte oluşturulur. `Sysmtem.out` ve `System.in` Java'da kulandığımız girdi ve çıktı akışlarına örnek olarak gösterilebilir.

**İş Parçacığı :** Bir iş parçacığı , çalışan bir programın içindeki denetim yeri olarak tanımlanabilir. 


