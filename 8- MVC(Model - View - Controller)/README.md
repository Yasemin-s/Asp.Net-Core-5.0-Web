👋 13 - MVC Nedir ? Asp.Net Core MVC Pipeline Nasıldır ?

Asp.net core da kullanacğaımız mvc yaklaşımını inceleyeceğiz. Mvc nedir ? 
Mvc, birbirinden bağımsız 3 katmanı esas alan bir mimarisel desen (architectural pattern)' dır. Bazı kaynaklarda tasarım deseni olarak da geçmektedir. Ama tasarımdan daha büyüktür daha derindir yani mimarisel desendir. 

Peki mimarisel desen ve tasarımsal desen arasındaki fark nedir ? 
İleride incelenecektir. Mimarisel desen dediğimiz, design patternlardan daa geniş kapsamlıdır. İçinde bir yada daha fazla design pattern kullanabilirsin ve belirli bir mimarinin oturduğu desenlerdir. Daha geniş kapsamlıdır. 
Design pattern dediğimiz tasarım desenleri belirli senaryolara uygun yerleştirilirken mimarisel desneler ise genel yaklaşımımızı belirler. MVC de olduğu gibi, biz bu yaklaşım üzerinden web geliştireceğiz. Mimariyi bunun üzerine pturtuyoruz/bunu benimsiyoruz. Bu bir mimarisel desendir.  

Ama sen gidite bağımsızlık üstüne çalışma yapacaksan, dependency injection desegn patternı uygularsın. Bu bir mimari değil sen bunun üzerine eb geliştiremezsin. Bu, o senaryo ihtiyacında onu uygulamaktır. Yada başka örnek olarak belirli stratejilerde çalışman gerekir. Starteji design patterni vardır vs... ama mimarisel desen dediğimiz bunlardan daha geniş kapsamlıdır. İçinde bir veya daha fazla tasarım barındırabilirler. MVC özünde observer, decorator gibi design patternları kullanan bir mimarisel desendir. 

👉  MVC ye tasarım deseni dememizde bir sakınca yoktur.

Microsoft, MVC deseni üzerinde oturtulmuş asp.net core mvc mimarisini geliştirmiştir. Mimarisel desen olduğu için, asp.neti' de bu mimarisel desen mantığında çalışılabilir hale getirmiş ve bunu da bize sunmuştur. 


✨  MVC Nedir ?  ✨

![13-1](https://github.com/user-attachments/assets/9e1ec1fe-8f05-40b4-97b6-fa5cdbb5ab8b)

Mvc, temelde bir kodun yapısal olarak işleme sürecinde bunun sunulmasını, değer üretme sürecini yada yönetilme sürecini birbirinden soyutlamamızı sağlar. Mvc, illa webde uygulanan bir tasarım deseni değildir. Bir programda/platformda/programlama dilinde de kullanabilirsin. MVC'yi iki şekilde açıklayacağız. Normalde nedir ve webde nasıldır/nedir şeklinde. 

Model, webde de diğer platformlarda da kullansan işlenecek olan veriyi temsil ediyor. Genellikle veritabanı işlemlerinin yapıldığı katmandır. Genelde, webde, bu katman için entity framework core ile çalışabiliyoruz. 

👉  Entity framework core amacı veridir. Entity modeller verinin ta kendisidir/veriyi modellediğimiz sınıflarımızdır.

Ado.Net çalışmaları da model katmanında olur. Repository design pattern katmanı kullanıyorsan modelde tutarsın. 

👉  Kısaca veritabanı işlemleri models katmanında tutulur.

👉  View, normalde elde edilen detayı görselleştirecek/anlamlı hale getirecek katmandır. Sunum katmanıdır. Web için html,css vs view da tutulur.

👉  Controller, gelen requestleri karşılayacak olan ve requestin içeriğine göre gerekli model işlemlerini üstlenir. Algoritmaları, servis, vt vs. çağırarak/çalıştırarak/sorgulayarak istenilen veriyiy üretmekten ve ihtiyaç dahilinde üretilen bu veriyi view ile görselleştirmekten sorumludur. 

✨  Webde MVC Anlatmaya Çalışalım ✨

![13-2](https://github.com/user-attachments/assets/0a00e3c3-f013-4d0d-9005-633f48297092)

Controllera duruma göre modelden veri gelir. Gelen veri yine duruma göre viewa gider ve viewdan veri döner. Controllera viewdan gelen veri clienta döner.
Mvc, de modelden viewa hiçbir zaman gitmez. Modelden, controllera controllerdan viewa gider.
Veritabanına ihtiyacın yoksa, modela gitmezsin, direkt viewa gidebilirsin. Viewa da ihtiyacın yoksa viewada gitmezsin. İlla bir yere gitmen gerekmiyor. Sonuç en son clienta gider.
View, controllerdan gelen veriyi alıyor/şekillendiriyor vs. ve sana geri dönüyor. İşte bu işelem "render" diyeceğiz. View, ilgili dataları render ediyor. Burda razor teknolojisi vs. kullanılıyor. Render edilen sonuçtan, view result dediğimiz bir sonuç üretiliyor. Üretilen bu sonuç sana gelen view resultta, viewın sonucu, sunumunun sonucu oluyor. 


✨ Asp.Net Core da Sürecin/Bir Requestin İşleme Sürecinin Nasıl Olduğunu Daha Detaylı İnceleeylim ? Asp.Net Core MVC Pipeline ✨

![13-3](https://github.com/user-attachments/assets/d186bd8a-d366-4d45-8008-4c41e442dfe4)

Bir request geldi ve bizim mimarimiz/ugulamamız bu rquesti nasıl karşılıyor ? Buradaki MVC mekanizması nerelerde devreye giriyor. 
Şimdi, MVC ile çalıştığımız için kestrel sunucumuz bu requesti karşılıyor. Önce middleware dediğimiz yapılar devreye girer. Sen ara yazılımları custom şekilde tanımlayıp önceden devreye soktuysan bunlar işlenecektir. Geçtikten sonra routing dediğimiz bir modül var/middleware var. (Şemadakilerin hepsi bir middlewaredır.) Routingde gerekli route işlemleri gerekli endpointler ayıklanacaktır. Hangi alana istek yapıldığına, routingde karar verilir. Rotayı burada belirliyor.

Controller initializer, ilgili controllerı ayağa kaldırıyor. Controller isteği karşıladı. Controller bizim için bir sınıftır. 

Action method execution, controller içinde action metotlar vardır. Controllerın içindeki metotlardır action metotlar. 

Result execution, action metottan gelen ilgili veri result olarak ya direkt clienta gidecek yada viewe gönderilecek.

Viewden render ile geri result dönecek ve clienta gidecektir. Yada isteği alıp başarılı bir şekilde sonlandırılsın bir yere bir şey gönderilmesin. 

👋 14 - Asp.Net Core 5.0 - MVC Proje Altyapısı Oluşturma ve Temel Konfigurasyonları Sağlama 

Boş bir asp.net core ugulmasını mvc mimarisine nasıl tasarlayabileceğimiz/altyapıyı nasıl kuracağımızı göreceğiz. Projeyi oluştururken mvc olarak değil boş bir asp.net core projesi seçerek ilerliyoruz, çünkü boş olan asp.net de nasıl mmvc olabilir/yapılabilir bunu inceleyeceğiz.

✨ MVC Design Patternda ✨ 

Gelen isteği karşılayan bir controller var. Controller, ihtiyaca göre modela gider. Modelden ilgili veriyi alıyordu. Eğer varsa bu veri üzerinde bir görselleştirme çalışması için viewa gidiyordu. Viewdan giydirilmiş/makyaj yapılmış veriyi requesti yapan clienta, response ediyordu. Şimdi bu mantığı asp.net core uygulamasında nasıl oluşturuluyor buna başlayalım: 

Boş bir asp.net core ugulamasında mvc design patternı kullanabilmek için, sistemin alacağı requestlerin mvc davranışıyla alabilesi/controllerının devreye girebilmesi için startup.cs de öncelikle mvc yi, uygulamaya eklememiz gerekiyor. 

👉  Şimdi ConfigureServices, bizim uygulamaya servisleri/modülleri eklediğimiz bir metottur. Burada parametredeki services üzerinden mvc servisini entegre etmem gerekiyor. Bu ne demek oluyor? Demek ki mvc, asp.net coreda bir modül olarak/servis olarak gelmiştir. Services.Add burada . bastığımızda Add ile gelenler bizim servislerimiz oluyor. Burada olanlar dahili  olanlar bir de eklediğimiz/yüklediğimiz kütüphaneler ile buraya gelecek/eklenecek olanlar var. Şimdi mvc de istekleri alan controllerı kullanacaksanız, controllerların ekli olması gerekiyor. Viewları/Razorları devreye sokacaksan ControlleWithView kullan, sadece controller kullanacaksan Controller kullan. 

![14-1](https://github.com/user-attachments/assets/5792e982-029f-43f1-bcba-db47f307557f)

Biz mvc olarak çalışacağımız için hem controller hem view olacağından ControllerWithView olacak. 

👉  Model, servis değil. Sadece veritabanı işlemlerinin yapıldığı bir katmandır. O yüzden servis ekleme kısmında modeli ekleyemiyoruz. 

![14-2](https://github.com/user-attachments/assets/3b09d421-091d-42ac-b494-653a70a89f3a)

Artık bu servisin eklenmesi ile request, mvc davranışyla karşılanabilecektir.


![14-3](https://github.com/user-attachments/assets/7253c58a-3791-4cca-a869-6f599b2f5910)

Şimdi gelen istekleri karşılayabilmemz için, bu isteğin davranışı daha iyi/net bir şekilde oturtabilmemiz için route(rota) ayarlaması yapmamız gerek. Yani bununla ilgili belirli middlewareleri tasarlamamız gerek. Startup.cs de Configure kısmında middlewarelerimiz var. Burada useRouting middleware var. Pipeline şemasındaki routing kısmı işte burası. Burada, gelen isteğin hangi controllerlara göre ayrılacağı belirlenir/rotalar burada devreye girer. 

Bizim için önemli olan bir diğer middleware, endpoints middlewaredır. Endpoint kavramı, istek yaparken yapmış olduğumuz adresin ta kendisidir. İstek nereye gidecek/varış noktası neresi, işte o enpointtir. Buradaki MapGet fonksiyonu daha sonra açıklanacaktır. MapGet silip yerine MapDefaultControllerRoute yazdık. Bu fonksiyon bize istek yapacığımız temel/default/varsayılan rotayı belirler. Diyor ki , yapacağın istek şu ciste olabilir. 


![14-4](https://github.com/user-attachments/assets/99ad7353-ae63-44b4-b3b6-5302a5c2365b)

![14-5](https://github.com/user-attachments/assets/55535fe5-b2d3-4d7b-b4b5-53e0fa0ec783)

Controller, gelen isteği karşılayyan bir sınıftır. 
Actionda bir metottur.
Bir istek/request gelecek, gelen isteğin nereye olduğunu/neyi ifade ettiğini şu formatta anlayabileceğiz. {controller=Home}/{Action=Index}/{Id?} 

![14-6](https://github.com/user-attachments/assets/a37de8c5-3dc0-45c8-9c94-7eb77ac2b8bc)

Personel controllerım yani sınıfım var. Getir adında bir metotum var. Ayrıca buradaki id? ile nullable dedik.

Normalde https://www.yasemin.com dediğinde hangi controller hangi action olduğu yazmıyor. Bu durumda default olan bilgiye gider. Controllerın boş gelmesi duumunda Home, actionun boş gelmesi durumunda indexe gider.

![14-7](https://github.com/user-attachments/assets/5e053774-b12c-493f-af10-b4f007d559a3)

Hilmi ise ön tanımlı değil tamamen developerın bildiği/yazdığı bir parametredir. 

MapDefaultControllerRoute ile, gelen isteği buradaki rota ile buradaki default tasarım ile eşleştir demiş olduk.

Bir web uygulamasında temel mvc konfigürasyonları yaptıktan sonra artık gelen istekleri karşılayabilmemiz için öncelikle controller tasarlamamız gerekiyor.

Controller : Uygulamaya gelen istekleri karşılayabilmek için kullandığımız sınıflardır. Controller sınıfları genellikle "Controllers" klasörü altında tutulur. Controllers adında değil Ahmet adında da klasör oluşturup controllerları altına koyabilirdik. Sonuçta arkada gelen istek controller initialize edilirken reflection sayesinde mimaride bulunuyor. Dolayısıyla hhangi klasör adı altında controllerların olduğu önemli değil ancak genellikle controllers klasörü altında oluyor. 

Oluşturduğun Controllers klasörüne sağ tıkladığında mvc uygulamasında çalışıyorsan yada asp.net core uygulamasında çalışıyorsan herhangi bir klasöre sağ tıkladığında controller sekmesi gelecektir. Startup.cs de controller, default olarak home adında olduğu için öncelikle Home adında controller oluşturuyoruz. 

![14-8](https://github.com/user-attachments/assets/0cbf6181-41da-447b-844c-ee3289996d39)

Açılan pencerede mvc altında controller seçiyoruz ve empty olanla devam ediyoruz. Daha sonra ismini belirleyeceğimiz sayfa açılıyor 

![14-9](https://github.com/user-attachments/assets/5d439c60-d18b-4fd7-82d6-8ef146666990)

ve adına PersonelController vs diyebiliriz ama biz HomeController diyoruz.

Controller sınıflarının isimlerinin sonuna Controller eki konulması gelenekseldir. IPersonel gibi interfacelerde olduğu gibi. HomeController olmalıdır.

👉  Controller, özünde bir classtır. Bir classın request karşılayabilir bir fıtrata sahip olabilmesi için Controller sınıfından kalıtım alması gerekiyor.

![14-10](https://github.com/user-attachments/assets/a98fd4e6-59b1-4839-8370-1eb555a85f8d)

Controller , Asp.net core mvc den gelmektedir. Yani bizim dahili olan frameworkümüzden gelmektedir.

![14--11](https://github.com/user-attachments/assets/2a7ceed4-31fc-4aca-b49a-8e7344fb2e8e)

Bir asp.net core uygulamasında herhangi bir sınıfı controllerdan türettiğin zaman davranış şu şekilde olacaktır. Controller sınıfına gittiğimizde veri taşıma alanlarımız mevcut get set kısımları, viewa veri taşımamızı sağlıyor. İlgili sınıflar belirli viewla iletişim kurabilen, viewa gerekli sonuçlar dönebileceğimiz fonksiyonlarımız mevcut, virtual olanlar diyebiliriz. 

![14-12](https://github.com/user-attachments/assets/2885cb56-46fe-47a9-a047-a186a916f1e7)

Controller base kısmında ilgili request için bilgiler getiren , responsea ulaşmamızı sağlayan ksıımlardır. Request ile igili bütün dataları sana getirecek ve response ile ilgili konfigürasonları yapmamızı sağlayacak bir sınıftır. 

![14-13](https://github.com/user-attachments/assets/062749c5-b0b0-444d-b04c-f0152f92a99d)

Bir controller sınıfının içine istek geldi, HomeController bu isteği karşıladı. İstek diyor ki homea git içindekş şu actionı tetikle. Sınıf tek başına operasyon gerçekleştiremez. Algoritmalar vs. metotlarda çalıştırılmalıdır. Senin ilgili sınıf içindeki metotun sayesinde aslında response oluşturulacak. Bir controller içinde ilgili istekleri karşılayan metotlara biz action metot diyoruz. Controller sınıfları içinde tanımlanan tüm metotlara artık action metot diyeceğiz. 

👉  Bir sınıf içinde operatif olarak metotları çalıştırır.

![14-14](https://github.com/user-attachments/assets/0ca815da-910f-46a9-9337-e5957d5d490d)

İndex metodu controller içinde olduğundan action metottur ve IAcionResult ile kullanılır. 

Proejyi ayağa kaldırdığında HomeControllerın altındaki indexe istek gönderirken startup.cs içindeki MapDefaultControllerRoute daki formata göre istek gönderilir/tetiklenir.

![14-15](https://github.com/user-attachments/assets/ffbd0e3c-5858-4dd6-9dc6-9fea88090847)

Uygulama ayağa kalkar kalkmaz sayfa/ekran gelmeden istek home altındaki indexe gelir. Neden ? 

![14--16](https://github.com/user-attachments/assets/e52ec7b9-600a-4050-b690-25fec455644c)

Çünkü localhost:5001 yanında hiçbir şey yazmıyor. Yani default olarak çalışacak bu. Default olarak da Home controllerın index actionuna gidiyordu. Breakpoint ile takip edersek görebiliriz. Debuga devam ettiğimizde ise ilgili sayfa gelecektir. 

![14--17](https://github.com/user-attachments/assets/ec065f5f-b138-4b6c-bc25-1f998b4fc588)

Url kısmında controllerın sadece adı yazılmalıdır.

Controllerdan viewe geçelim : Controllerdan viewe nasıl geçiş yapabiliyoruz. bunu inceleyelim. Proeyye sağ tıklanıp Views adında bir klasör oluşturuyorum. Model view controllerdaki bu 3 katman esasında bir klasördür. Controller sınıflarındaki action metotların kullanacağı viewlara gelelim. Bunların kesinlikle Views adındaki klasörün altında tanımlanmış olması gerekiyor. Ayrıca bir controllera ait viewlerin hepsi, Views klasörü altındaki ilgili controller isminin altında olmalıdır. 

![14-18](https://github.com/user-attachments/assets/13c701df-c424-4445-9bd3-42b2b23e5fdf)


Sonuçta HomeController altında da ProductController altında da aynı isimde view olabilir. Bunun ayrımının yapılabilmesi için kategorize yöntemi sağlanmış views klasörü altında.

![14-19](https://github.com/user-attachments/assets/6a5a9cef-c1a1-406f-8e29-2e79568cff2a)

View oluşturma kısmı, 

![14-20](https://github.com/user-attachments/assets/58318f17-6622-41ed-895b-0a1b9122be3c)

Açılan ekranda razor view empty seçtik. Daha sonra açılan sayfada ,

![14-21](https://github.com/user-attachments/assets/6a6804ad-b5a2-40c6-a2f8-fc6cdefb7479)

Viewa isim vermemiz gerek. Bu ismi action ile birebir aynı isim yapmalısın. 



