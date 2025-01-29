👋 1 - Proje Oluşturma ve Dosya Yapısı 

Asp.net core uygulamasının nasıl ayağa kaldırıldığını/oluşturulduğunu inceleyeceğiz. Boş bir asp.net core uygulamasında temelde bir web uygulamasının temel dosyalarının neler olduklarını göreceğiz.
Önce asp.net core uygulamasını nasıl ayağa kaldırıyoruz/oluşturuyoruz ? Seçeceğin/oluşturacağın asp.net templatenin içinde core olmasına dikkat ediyoruz. 

Templatelerin hepsi web api olur, razer page olur, mvc olur farketmez. Bunların hepsinin temeli asp.net core uygulamasıdır. Dolayısıyla biz önce asp.net core uygulamalarının temeldeki dosyalarını bilmeliyiz ki artık mvc de çalışıyorsan kendine göre tasarımı/gerekli kodları/yapılanmasını öğrenirsin. Peki bu yapılanma nedir ? Gelin boşta bir proje oluşturarak değerlendirelim. Proje boştayken nasıl mvc'ye yada nasıl api'ye çevirdiğimizi göstereceğiz. 

Asp.net core empty seçtik. Şuanda temelde bir webde çalışacak web projesi oluşturdum. 

Önce dosyaları tanıyalım:

 
✨ Program.cs ✨

![12-1](https://github.com/user-attachments/assets/ce538b9b-4d79-4102-8a2e-e3d55004acb4)

Akla direkt console uygulaması gelir. Esasında asp.net core içinde program.cs barındırdığı için özünde bir console uygulamasıdır. Bir web uygulamasından bahsediyoruz ama fıtratı console uygulmasıdır. Program.cs içerisinde Main fonksiyonu ve CreateHostBuilder fonksiyonu vardır. 

Program classı, asp.net core uygulamaları özünde console uygulamalarıdır. Bu console esasında yapılandırılmış varsayılanlarla web barındırıcı oluşturmak için bir yöntem bir metot çağırıyor.   O metot da CreateHostBuilder metotudur. 

Asp.net core kendi bünyesinde kendi fıtratında sunucusunu taşıyor demiştik. Dolayısıyla o sunucuyu bir şekilde ayağa kaldırması lazımdı. Bünyesinde bulundurduğu kestrel sunucusunu ayağa kaldırmak istiyorsan createhosbuilder metotunu tetiklemen gerekir. Aynı şekilde IIS sunucusunu da benimseyip konfigürasyonları yapabilirsin. 

Asp.net core kendi dahilinde/fıtratında sunucu barındırır demiştik. İşte o sunucuyu ayağa kaldırdığı/dışarıdan başka bir sunucuya ihtiyaç duymadan kendi bünyesindeki sunucuyu ayağa kaldırdığı sonra web uygulamasını da onun üzerinde ayağa kaldırdığı (bu şekilde sen linuxta da apachede de çalışabiliyorsun.) nokta bu program.cs dosyasıdır.

"CreateHostBuilder" metotunda host üstünden (host)sunucuyu ayağa kaldırıyor. "Program.cs" içinde host ayağa kaldırılır. Peki bu host ayağa kalkarken hangi ayarlara göre ayağa kalkacak? Bu ayarlar konfigürasyonları da nerden alacağını bildiriyor. "UseStartup" diye bir metot var. <startup> ile bu sınıfı baz al diyor. Demek ki bu asp.net core uygulaması ayağa kalkarken startup dosyası/sınıfındaki konfigürasyonları baz alarak ayağa kalk diyor.

👉 ! Startup, temel konfigürasyon sınıfımızdır.

✨ Startup ✨

![12-2](https://github.com/user-attachments/assets/ec5b8c31-9781-4524-95bd-8ee0cc755a3e)

Temel web uygulamasında bu mvc olur api olur vs. fark etmiyor, web uygulamasında belirli konfigürsyonları yaptığımız bir dosyadır. Startup'ın ismi startup olmak zorunda değildir, ahmet mehmet de olabilir. Ama o ismi program.cs de kullanırken de ilgili yerde (startup yazan her yerde) değiştirmen gerekir. 
 
Startupta temelde 2 tane fonksiyon vardır. Biri ConfigureServices diğeri Configure. 

ConfigureServices'da , uygulamada kullanılacak olan servislerin eklendiği/konfigüre edilidği metottur. 

Configure'de, uygulamada middleware dediğimiz ara katman/ara yazılımdar vardır.  Burada kullanılacak olan middleware/ara yazılımlar çağırıyoruz.

👉 ! Servis nedir : Asp.net core modüler bir yapılanmaya sahiptir demiştik. İşte o modül, parça bütün ilişkisi o parçalar (belirli işleme/amaca uyarlanmış özel tasarlanmış sınıflar hepsi bizim için birer servisi ifade ediyor.) Yani servisler, belirli işlere odaklanmış ve o işin sorumluluğunu üstlenmiş kütüphanelerdir/sınıflardır. 

Örnek, yapacağım uygulamada ödeme modülü yok. Ödeme ile ilgili konfigürasyonları/işlemleri tek tek oturup yazarsam uzun sürer. Ama bununla ilgili paket bulduk diyelim bir kütüphane bulduk, Bu kütüphaneyi bu uygulamaya dahil edebilmem için yani bu modülü bu uygulamaya dahil edebilmem için gelip burda ConfigureServices'da bunu çağırmam gerekir. Yani modülü uygulamaya eklemen lazım. İşte bu modüle, kütüphane/servis diyoruz. 

👉 ! servis = modül = kütüphane

İlgili modülü ConfigureServices'a eklemem gerekir ve IServisCollection'dan ekleme yaparım.

✨ Appsetting.json ✨
 
Uygulamada belirli static değerleri tuttuğumuz bir konfigürasyon dosyasıdır. Örnek vt'de ConnectionString değeri tutuyoruz. Tutup da bunu kod içinde değil burda yazıyoruz ve sonrasında buradan çağırıyoruz. Yazılımda bazen uygulamanın her yerinde kullanmak isteyeceğimiz metinsel değerler olabilir. Yazılımda kullanmamız gereken statik olan metinsel değerler kodun içerisine yerleştirilmez. Çünkü gün gelir bu değer değiştirilmesi gerekirse eğer kodda her yerin düzeltilmesi gerekecektir. Halbuki bu durum biizm için maliyetli olacaktır. Böyle maliyetlerden kaçınabilmek için statik olan metinsel değerleri appsetting.json dosyasında tutmalıyız.

✨ Appsetting.development.json ✨
 
İleride environment diye bir konudan bahsedeceğiz. Ortamlardan, environment değişkenlerden bahsedeceğiz. İşte, environment'tan kısaca bahsetmek gerekirse, bir web uygulaması oluşturursun, oluşturulmuş bu web uygulaması/oluşturma şeması, development seviyesidir. Sen bunu yayına aldığın zaman yayınlamış olursun.

Web uygulamasını yapma aşamasında, geliştirme ve inşa aşamasına "development" denir. Yayınlanma aşamasına da "production" denir. Production ortamı, development ortamıyla aynı değildir. Bunların arasında test durumları da vardır. Test ortamına genellikle "staging" denir.

Bu 3 ortam aynı değildir. Ortam dediğimiz kavram geliştirdiğimiz uygulamanın bulunduğu seviyedir/aşamadır, gibi düşünebilirsin. Ya geliştirme sürecindedir yada yayınlama sürecindedir. İşte farklı ortamlara göre belirli değişkenler tanımlayıp operasyonlar gerçekleştirebiliyoruz. Environment'tan bahsederken o zaman appsettings.development.json dosyasından bahsedeceğiz. Adı illa bu olmak zorunda değil, sen ahmet ortamında çalışıyorsan appsettings.ahmet.json diyebilirsin.

✨ Properties ✨

Üstüne tıkladığınızda bir uygulama açılıyor ve bu uygulamanın içinde properties klasöründe yer alan launchSettings.json dosyası bulunuyor. launchSettings.json dosyasında environment profillerini yönetebiliriz.

launchSettings.json dosyası, properties klasörüne tıkladığınızda açılan uygulamanın sol tarafında yer alan debug seçeneğini yönetmeyi sağlar. Debug modunda gördüğünüz her şey aslında bu dosya aracılığıyla yapılandırılmış olur. Kodda yaptığınız değişiklikler de doğrudan debug modunu etkiler.

![12-3](https://github.com/user-attachments/assets/57abd84d-52aa-4867-aa3e-de592f318e00)

✨ Dependencies ✨

.NET Core'da kullandığımız kütüphaneler, frameworkler ve bağımlılıklara dependencies denir. Bu bağımlılıklar hem harici hem de dahili kütüphaneleri barındırır.

Bir uygulama ayağa kalktığında öncelikle Program.cs tetiklenir. Gerekli host burada oluşturulur ve yapılandırılır. Ardından, uygulamanın çalışması için ihtiyaç duyulan konfigürasyonlar buradan alınır. Uygulama, benimsenen model ve davranışlara göre çalışmaya başlar.

Bu aşamadan sonra hangi yaklaşımla kodlama yapmak istiyorsam, o doğrultuda kodlarımı yazacağım. Gerekli servisleri tanımlayacak, middleware'leri çağıracağım.

Bir uygulamayı IIS ya da Kestrel üzerinde çalıştırabilirsiniz. Proje çalıştığında, proje ismiyle aynı olan bir sekme göreceksiniz (Kestrel), diğer seçenek ise IIS olacaktır.

![12-4](https://github.com/user-attachments/assets/b70d9190-f20d-482e-84c5-87c287767ffc)

Bu kavramları ileride environment profillerini anlatırken daha net bir şekilde açıklayacağız.
