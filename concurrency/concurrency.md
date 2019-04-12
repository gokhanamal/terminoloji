
Transleted from [Reading 17: Concurrency](http://web.mit.edu/6.005/www/fa14/classes/17-concurrency/)

# Concurrency (Eşzamanlılık)

Eşzamanlılık, birde fazla hesaplama islemlerinin ayni anda medyana gerceklesmesi anlamina gelir. Hosumuza gitse de gitmese de, modern progralama dunyasinda eşzamanlılık heryerde karsimiza cikabilir.:

- Bir agdaki birden fazla bilgisayarda
- Bir bilgisayarda calisan birden falza uygulamada
- Bir bilgisayardaki birden fazla eslemcide (gunuzmuzde, bir cipteki birden fazla islemci cekirdeginde ) 

Aslina bakarsak, concurrency moden programlama dundyasinda olmazsa olmazlardandir:

- Web siteleri birden fazla eszamanli kullanici ile basa cikmak zorundadir.
- Mobil uygulamalar bazi islemlerini sunucularda yapma ihtiyaci duyarlar.
- Grafiksel kullanici arayuzlari (GUI), kullanici deneyimini kesintiye ugratmamak icin nerdeyse herzaman islemleri arkaplanda yapmaya ihtiyac duyar.

Eszamanli programlama yapabilmek gelecekte de onemini korumaya devam edecek. Islemcilerin dongu hizlari azami seviyeye ulastigi icin artik dongu hizlarini arttirmak yerine
her yeni nesil yongada daha cok sayida cekirdek kullaniyoruz. Boylece gelcekte de, daha hizli hesaplamalar yapabilmek icin, hesaplamalari eszamanli parcalara ayiracagiz.

# Eszamanli Programlama Modelleri

Eszamanli programlamada yaygin olarak iki ayri model kullaniliyor: *shared memory* (ortak hafiza) and *message passing* (ileti gecisi)

**Ortak Hafiza.** Eszamanliligin ortak hafiza modelinde, eszamanli moduller hafizadaki ortak bir nesneye okuma ve yazma islemleri yaparak birbirleri ile etkilesime geceler.


