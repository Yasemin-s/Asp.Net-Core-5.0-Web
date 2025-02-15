👋 31 - Kullanıcıdan Gelen Verilerin Doğrulanması - Validations


Validation: Bir web uygulaması tek taraflı veri akışı sağlamaz. Yani web uygulaması sadece kullanıcıya veri vermez, kullanıcıdan da veri alır. Gelen her veri alınacak mı/kullanılacak mı? Biz genellikle kullanıcıdan gelen verileri doğruladıktan sonra işleme tabi tutarız.

👉 ! Bu doğrulamadan kasıt şudur: 


Örneğin, bir e-posta formatında değer girilmesi istenirse, doğru formatta mı girilmiş, bunun kontrolünü yapmamız gerekir. Gelen değerin e-posta olup olmadığını formatından yola çıkarak anlarız. Ya da TC kimlik numarası istedin, ancak kullanıcı sana 11 karakter yerine 15 karakterlik bir değer girdi. İşte bu tarz durumlarda kontrol yapmak gerekir.

Yani her gelen veriyi kullanmıyoruz. Bizim belirlediğimiz şartlara göre uygun olup olmama durumlarını değerlendirip ona göre işlemleri yapıyoruz.

👉 ! Kullanıcıdan gelen verinin sunucu tarafında kontrol edilip doğrulanmasına "validation" denir.

Kullanıcıdan gelen veri, sistemdeki şartlara uygunsa, bu veri işlenmeyi hak eden veridir.

Validation: Bir değerin içinde bulunduğu şartlara uygun olması durumudur. Belirlenen koşullara ve amaca uygun olup olmama durumunun kontrol edilmesidir. Bu kontrole göre verinin işleme tabi tutulması durumudur.

Validation, web yazılımında iki türlüdür. Client'tan server'a belirli datalar geliyor. Client, dataları gönderirken gelen dataları server'da validation işlemine tabi tutuyoruz. Eğer ki yapılan validation server tarafında gerçekleştirilirse, biz buna "server-side validation" deriz. Aynı zamanda client tarafında da validation yapılması gerekir.

Client'tan gelecek olan veriyi önce client'ta denetleyip kontrol edersen, server'daki yükü de azaltmış olursun. Client tarafında yaptığın doğrulamaya ise "client-side validation" denir.

Client tabanlı alınan validation'lar, aynı şekilde server tabanlı da alınmak zorundadır. Validation 2 türlüdür. Hem kullanıcının kullanmış olduğu client'ta doğrulama yapmalısın hem de gelen verileri server'da doğrulama yaparsın/yapmalısın.

Peki, client'ta validation'u yaptıysam, istediğim şekilde bana veri gelecekse, istediğim şekilde veri girişi yaptırdıysam, ben server'da tekrar validation yapmama gerek var mı? Kesinlikle server'da validation kontrolleri yapmamız gerekir. Çünkü client'taki validation'lara çok rahat müdahale edilerek aşılabilir, yani bu bir güvenlik açığıdır/risktir. Dolayısıyla client'tan gelen veriler çok da güvenli değildir. En son server tarafında doğrulama yaparak kontrol ederiz ki, duruma göre işlemler yapalım ya da yapmayalım.

Kullanıcı deneyimini artırmak için client validation her zaman yapılır. Yanlış girildiyse (TC kimlik no vs.), kullanıcıya "Bu hatalı giriş yaptınız." şeklinde bir uyarı gösterilir.

👉 ! Validation, paralel bir şekilde hem client hem de server tarafında uygulanmalıdır.


✨ Validationlar Nasıl Uygulanır ✨


Öncelikle kullanıcıdan veri almamız gerekiyor ve bunun için cshtml'de form oluşturuyorum. cshtml'de şartlarımı belirliyorum. Örneğin, bu alan boş olmamalı, metinsel uzunluk maksimum 100 karakter olmalı, eğer email ise email formatında olmalı. Bu şartları yerine getiren bir bilgi girişi yapılmasını istiyorum.

![31-1](https://github.com/user-attachments/assets/ba16b56a-fc6b-4702-9d98-51b0d4c6fce4)

Action'da if ile bu şekilde uzun uzun yazmak zahmetlidir. Gelen dataları belirli bir doğrulamaya tabi tutacaksak eğer bunu if, else veya switch ile yapmamalıyız. Çünkü bu şekilde yapılan yapılanmalar/kodlar direkt çöp kod olur.

Peki if, switch kullanmıyorsak validationlarda ne kullanıyoruz?
Model'e validation kuralları oluşturuyoruz. Yani kullanıcıdan gelen datayı yakalayacak model'e belirli annotations bildiriyorum. Ve bu bildirilen annotations'lar üzerinden gelen dataları kontrol ediyorum. Zaten annotations'lar, benim belirlemiş olduğum kurallara/şartlara uyup uymadığına dair ilgili verilerle alakalı bilgiler döndürmektedir. Bu da bizim için efektif bir çözüm demek oluyor.

👉 ! Örnek:



Uygulayacağımız validation Product nesnesi üzerinden olacaktır. Yani ilgili değeri karşılayacak olan nesnemiz Product sınıfıdır. Biz bu sınıftaki property'lere validation şartlarımızı bildireceğiz. Bu şartları attribute ile bildiriyoruz ve buna annotation attribute diyoruz.


✨ Required Attribute ✨



İlgili property'e giriş yapılmış olması gerekiyor, yani boş bırakılamaz. İstersek kullanıcıya hata mesajı da verebiliriz.

![31-2](https://github.com/user-attachments/assets/f90d8983-1d3d-47bb-889c-1a10bc1ca4c5)

Formdan action method'a gelen datayı action method'ta doğrulayabilmek/kontrol edebilmek için ModelState yapılanmasını kullanacağız. ModelState, MVC'de bulunan bir yapılanmadır.


✨ ModelState ✨



MVC'de bir type'ın data annotations'larının durumunu kontrol eden ve geriye sonuç dönen bir property'dir.

👉 ! Şu mantıkla çalışır:

Sen isteği gönderdin.
Gelen isteği Product nesnesinde karşıladın.
Bu Product nesnesinde varsa validation ayarları/attributes'leri, sistem buna göre arkada işlemekte ve validation durumunu ModelState'de tutmaktadır.
"if (ModelState.IsValid){}" ile modeli doğruladıysan, artık içinde yazmış olduğun kodları çalıştırabilirsin diyoruz. Doğrulanmadıysa da şu işlemleri yap diyebilirsin.

Formdan gelen verilerin validationlarının doğrulanıp doğrulanmadığını nereden, nasıl göreceğiz?
ModelState > Values > Results View kısmında, hangi duruma/validasyona dair hata olduğunu görebiliriz. 

![31-3](https://github.com/user-attachments/assets/a515c8c0-04bc-4ff3-bc02-bc31da627a88)

Burada Invalid olan kısmı açarsak, ModelState’de hangi alanın hata verdiğini Errors kısmında hata olarak görebiliriz. 

![31-4](https://github.com/user-attachments/assets/f775140a-3048-4e8e-bb53-93ba88f8fae9)

Peki, programatik olarak mesajın bilgisini nasıl elde edebilirim?
Hata alınması durumunda, hangi alanın hata verdiğini şu şekilde gösterebiliriz. 

![31-5](https://github.com/user-attachments/assets/e54aac13-a994-4874-b19b-9a6b0b9e25b9)

Kullanıcının girmiş olduğu verilerde eğer ki validasyonlara uymayan veriler söz konusu ise, alınan hataları kullanıcıya doğrudan hata mesajı olarak gösterebiliriz. Bunun için şunları yapmalıyız:

View'de ilgili input alanlarına karşılık hata mesajlarını gösterebileceğimiz "span" etiketleri oluştururuz.
<span asp-validation-for=""> ile bind edilen property, eğer ki validation doğrulanmadığı takdirde, mesajı alıp buradaki span içerisine yazdıracaktır. 

![31-6](https://github.com/user-attachments/assets/7ce558de-d728-4cd9-9e08-2d3b81e97497)

.cshtml tarafında bunu yaptıktan sonra, ilgili action method içinde ModelState doğrulanmadıysa, gelen modeli return View(model); ile tekrar View’e göndermeliyiz.

![31-7](https://github.com/user-attachments/assets/fcde06ff-f7cc-45f3-be86-b43ecd7a9bc5)

👉 ! Burada aslında şu oluyor:



Bize gelen model’de eksiklikler olduğu için, uygun doğrulamalar sağlanmadığı için Errors kısmı dolu oluyor ve biz bu model'i tekrar cshtml tarafına gönderiyoruz. .cshtml tarafında, Errors kısmı dolu olarak gelen modelin Errors bilgisini asp-validation-for üzerinden gösteriyoruz/eşleştiriyoruz.


✨ Kötü niyetli kullanıcılar client tabanlı çalışmaları nasıl aşabiliyorlar? ✨

![31-8](https://github.com/user-attachments/assets/321ab7ad-a57f-4b76-9e9c-99e1b6eaf117)

Sayfa kaynağını inceleyip, bizim maxlength="100" olarak belirttiğimiz kısmı maxlength="250" olarak değiştirebilirler.
Ya da email kısmına yanlış formatta "yaseminbulut" gibi bir giriş yapabilirler ve client tarafında bir hata mesajı alırlar. 

![31-9](https://github.com/user-attachments/assets/7e68f3d2-8547-4bfb-8b31-5fe3e303bc4c)

Ancak, "Ögeyi Denetle" kısmından input type'ını text olarak değiştirirlerse, gönder butonuna tıkladıklarında veriler bu defa gider. Fakat! Server tarafında doğrulama yapıldığında, gerekli ve ilgili hata mesajları döndürülür.

![31-10](https://github.com/user-attachments/assets/39c32bd3-a2eb-45f2-8196-345acf2a7e60)

![31-11](https://github.com/user-attachments/assets/4fca9763-99e0-4c17-a267-2099cb409259)

ModelState dediğimiz property bizim hata durumlarını yönetmemizi ve incelememizi sağlayan, hata mesajlarını elde etmemizi sağlayan, etkili bir validation kontrolü sağlayan yapılanmadır. MVC mimarisinde hazır olarak bulunmaktadır. Aynı zamanda tüm hataları view kısmında tek tek span ile göstermek zorunda değiliz. Tüm hataları tek seferde bir div içinde gösterebiliriz.

👉 ! Div içinde tek bir tag helper kullanılır:



<div asp-validation-summary="All"></div>
Bu div içine, sayfaya gelen modelin state’inde hata varsa, tüm hatalar buraya doldurulacaktır. 

![31-12](https://github.com/user-attachments/assets/a77d0b38-a636-44b3-aaf6-ce075a7bfe85)

👋 32 - ModelMetadataType ile Validation Sorumluluğunu Başka Bir Sınıfa Yükleme


Validationları entity sınıflarında/modellerde, yani veritabanındaki tablolara karşılık gelen ve onları modelleyen sınıflarımızda oluşturmak istemeyiz. Peki, validationları nerede uygulayacağız? ViewModel'lerde uygularız. Ancak, ViewModel'lerde kullandığımız validationlar, SOLID prensiplerinden Tek Sorumluluk (Single Responsibility Principle) ilkesine aykırılık oluşturabilir. Çünkü bir sınıf sadece tek bir amaca odaklanmalıdır.


✨ Tek Sorumluluk (Single Responsibility Principle) Nedir? ✨

Bu prensip, bir sınıfın, bir metodun veya bir yapının yalnızca tek bir amaca odaklanması gerektiğini savunur. Peki, böyle bir durumda Data Annotations (Validation Kuralları) nasıl daha efektif kullanılabilir? ModelMetadataType Attribute ile validation tanımlamalarını farklı sınıflara yükleyebiliriz. FluentValidation yapılanmasını/kütüphanesini kullanabiliriz.


✨ ModelMetadataType Kullanımı ✨

Eğer ViewModel veya Entity sınıfında herhangi bir validation tanımlaması yapmayacaksak, ModelMetadataType kullanılabilir.

👉 ! Nasıl Kullanılır?



"Models" klasörü altında "ModelMetadataTypes" adında bir klasör oluşturuyoruz.
Burada elimizdeki ViewModel'lerin veya Entity'lerin validation kurallarını içeren Metadata sınıflarını oluşturuyoruz. Örneğin: Eğer Product sınıfımız için validation gerektiren tüm property'leri, ModelMetadataTypes klasörü altında oluşturduğumuz ProductMetadata sınıfına taşırsak, validation'lar burada tanımlanmış olur.

![32-1](https://github.com/user-attachments/assets/a3d6452f-c6cc-4fd0-a918-ae54a624341a)

![32-2](https://github.com/user-attachments/assets/1b47085f-23b9-407c-b01a-942a0e0c61f1)

Peki, ProductMetadata sınıfının, Product validationlarını uygulayan Product sınıfına ait olduğunu nasıl bildireceğiz? Product sınıfına ModelMetadataType ile ilgili validationları uyguladığımız sınıfı bildiriyoruz. 

![32-3](https://github.com/user-attachments/assets/b31ad10e-6e6b-4c8c-8536-d527158e3767)

👋 33 - FluentValidation Kütüphanesi ile Validation İşlemleri

FluentValidation nedir?
Validasyon işlemlerini daha efektif bir şekilde kullanabilmemizi sağlayan hazır bir kütüphanedir. Peki, neden hazır bir kütüphane kullanıyoruz? Eğer ki data annotations ile validasyonel operasyonlar gerçekleştirirsek, bunlar SOLID prensiplerinden tek sorumluluk prensibi dediğimiz Single Responsibility Principle ilkesine aykırı olacağından dolayı, SOLID prensibini yüzde yüz uygulayan ve validasyon operasyonlarını farklı sınıflara taşımamızı/sorumluluğunu yüklememizi yüzde yüz sağlayan FluentValidation’u tercih ediyoruz.

FluentValidation’u MVC mimarisinde kullanabilmek için ilgili kütüphaneyi projeye yüklememiz gerekiyor. Projeye sağ tıklayıp Manage NuGet Packages kısmından FluentValidation.AspNetCore olanı yüklüyoruz. Sonrasında FluentValidation servisini uygulamamıza entegre etmeliyiz. Startup.cs'de ConfigureServices içinde: services.AddControllersWithViews().AddFluentValidation(); 
ile entegrasyonu sağlıyoruz.

Kullanıcıdan/clienttan gelecek verileri karşılayıp gerekli validasyonel operasyonları üstlenecek olan entity’lerimin üzerinde yapacağım validasyonları uygulamada bir yerde tutmam gerek. Bu validasyonların nerede tutulursa tutulsun sisteme bildirilmesi lazım. Bu bildirimi tek tek yapabilirsin ya da sistemden/servisten, mimarideki reflection üzerinden kendisinin bulmasını isteyebilirsin. Onlarca validator olabiliyor ve bunların hepsini tek tek sisteme entegre etmektense mimariye bulduruyoruz.

![33-1](https://github.com/user-attachments/assets/49ef9239-cea5-4df4-a17d-690c5dd4d122)

Burada bütün validator sınıflarını buldurmuş ve sisteme otomatik entegre ettirmiş olduk.

Sonrasında, kullanıcıdan gelecek olan dataları karşılayacak olan view modellerin ya da entity sınıflarının üzerine validasyon operasyonları uygulamam gerekiyor. Models klasörü altında Validators klasörü içine ProductValidator sınıfını oluşturuyoruz. İlgili/oluşturduğumuz sınıfın validator sınıfı olarak algılanabilmesini sağlamak için AbstractValidator’dan türetiyoruz ve içine generic olarak hangi türü/modeli/view modeli validate edeceğiz, bunun da bilgisini veriyoruz.

![33-2](https://github.com/user-attachments/assets/d824e8a1-e176-4b36-9b35-f221e3a3dafb)

RuleFor ile validasyonlarımı gerçekleştireceğim/uygulayacağım. RuleFor, benim genericte girmiş olduğum entity’ye/türe göre uygulama yapıyor.

![33-3](https://github.com/user-attachments/assets/52e8d6cb-ab8a-43c8-a4ae-8fdc26b666c8)

Burada NotNull ve NotEmpty kısmında NotNull durumu için mesaj yazdık ama NotEmpty kısmı için mesaj yazmadık. Aslında NotNull değil NotEmpty deyip mesaj yazmalıydık. Bizim yaptığımıza göre mesaj yazmadığımız validasyon, default mesaj ile bize dönüş sağlayacaktır.

![33-4](https://github.com/user-attachments/assets/af021ff0-85bb-4122-96b0-d6db6dfe9932)

Action metotta Product’a gelen bir model/data eğer ki ProductValidator’daki validasyonları sağlamıyor ise, ilgili kontrol neticesinde ModelState’in gerekli error mesajları doldurulacak ve key’lere karşılık mesajlar cshtml'de bind ettiğimiz yerlerde gösterilecektir.


👋 34 - Server'daki Validasyonları Dinamik Olarak Client Tabanlı Uygulamak


Server'da tanımladığımız validasyonların client'a nasıl taşındığını ve client tabanlı bu validasyonların sağladıklarını ele alıyoruz.

Backend'de alınan validasyonlar (Metadata, FluentValidation, DataAnnotations) client'ta tekrar yazmaya gerek kalmaksızın nasıl oraya taşıyıp client tabanlı validasyonların uygulanabildiğini bu dersimizde inceliyor olacağız.

Şu ana kadarki çalışmalarımızda client tabanlı validasyon uygulamadık. Şimdi validasyon uygulanan formda/modelde getirilecek olan verilerin formata uygun olmadığı duruma bakarsak, Gönder butonuna tıkladığımızda Action Metot'ta server bu datayı/post'u alıyor. Server'da validasyonu gerçekleştiriyoruz. Eğer ki doğrulanmıyorsa client'a yeniden mesajları gönderip uyarıda bulunuyoruz. Eğer form kısmında da validasyonumuz olsaydı, istek server'a gidip gelmeden de kullanıcıyı uyarabilirdik.

👉 ! Bu neye yarar?

Server'daki iş yükünü azaltır.
Kullanıcı dostu bir arayüz sunar. Kullanıcı, her defasında düzeltme yapmaya gerek kalmadan veri girişi yapar. Client Tabanlı Validasyonları Nasıl Alacağız? Client tabanlı validasyonları manuel şekilde alabilirsin. jQuery, JavaScript ya da farklı kütüphaneler ile backend'deki mantığa uygun validasyonları birebir client'ta da uygulayabilirsin. Ama sunucuda yazmış olduğun validasyonlar zaten var, aynısını client'ta yazmak yerine, sunucuda yazılmış validasyonları client'a nasıl taşıyabiliriz? Bunu da ilgili kütüphaneler ile yapacağız. Yani client'ta ekstra validasyon kodları yazmadan, server'da backend'de oluşturulmuş validasyon kodlarını client'a taşıyabilir ve client üzerinde AJAX tabanlı validasyon işlemlerini gerçekleştirebiliriz.


✨ Kullanacağımız 3 farklı kütüphane ✨



jQuery (Normal/base kütüphane, diğer kütüphaneleri çalıştırabilmeyi sağlar)
jQuery Validate (Client doğrulamayı yapacak olan kütüphane)
jQuery Validation Unobtrusive (Sunucudaki validasyonları client'a taşıyabilmek için bizlere yardımcı olacak kütüphane)


Client-side eklentisini kullanarak harici UI tabanlı kütüphaneleri yükleyeceğiz. wwwroot’a sağ tıklayıp "Add" dedik, "Client-side Library" sekmesi ile UI tabanlı kütüphaneleri yükleyebiliyoruz. 

![34-1](https://github.com/user-attachments/assets/e6d77c41-bdb7-41f9-9cad-95cd7cc6883f)

![34-3](https://github.com/user-attachments/assets/9a9f81cd-d392-49e4-9cd9-5232804fdf04)

Ayrıca CSS, jQuery kütüphanelerini wwwroot dizini/klasörü içine yüklemeliyiz. Harici kütüphaneler wwwroot dizininde tutulur. Tabi wwwroot klasörüne erişebilmek için Startup.cs’de app.UseStaticFiles middleware’i çağırman gerekir.

![34-2](https://github.com/user-attachments/assets/c665029f-548a-4f27-b576-940d18cae6f6)

Nerede client tabanlı validasyon yapacaksan, bu kütüphaneleri ilgili view’da kaynak olarak göstereceksin (her kütüphane için min dosyalarını sürükle bırak yapacaksın).

![34-4](https://github.com/user-attachments/assets/cdccb680-be11-4cf9-b147-36656df1e06c)

Bu çalışmayla server’daki validasyonlar view’e taşınacak ve client tabanlı validasyon işlemlerini yapmanı sağlayacaktır.

Client tarafında form için öğeyi denetlersek, inputlara validasyonların hepsi yüklenmiştir. Yüklenen bu validasyonlar hızlı bir şekilde client tabanlı sonuç gösterecek. 

![34-5](https://github.com/user-attachments/assets/c64c2c2d-48a0-4613-9950-56aa7d0882ca)

Cshtml kısmında kütüphaneleri ekledikten sonra bind mekanizmasını kullanarak form oluşturduysan, gerekli hata mesajları client tabanlı alınacak/çalışacaktır. Projeyi çalıştırıp formda gönder butonuna bastığında ve breakpoint ile takip ettiğinde, server’a istek gelmiyor ama UI’da doğrulama mesajları gösteriliyor.

![34-6](https://github.com/user-attachments/assets/d3ec4dc2-e756-46d0-b29a-1a1b4477d713)

Aynı şekilde form girişine uygun veri girildiğinde hata mesajı gidiyor ya da ona göre bilgiye göre güncelleniyor, yine client tabanlı dinamik bir şekilde çalışmış oluyor yani.

![34-7](https://github.com/user-attachments/assets/cd74de9e-c64f-433e-9af4-28ecec5bfb18)

Bütün şartlar sağlandığında istek sunucuya gidecektir. 

![34-8](https://github.com/user-attachments/assets/2053d675-45f4-4957-bc51-642474ca1cca)
