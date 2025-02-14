👋 25 - Kullanıcıdan Veri Alma Yöntemleri – Form Üzerinden Veri Alma



Kullanıcıdan veri alabilmenin tek yolu kullanıcının bize bir istek göndermesi. Gelen isteğin kullanıcı, belirli noktalarına kullanıcı verilerini yerleştiriyoruz. Gelen verileri sunucuda karşılayıp/elde edip işleyebiliyoruz.

Form sayesinde inputlara girilen dataların hepsini tek seferde gönderebiliyorsun. Form üzerinden veri alma iki türdür. POST ve GET olarak veri alabiliyorum/veri gönderme ve veri alma. Peki biz kullanıcıdan veri alacaksak formda ne olması gerekiyor? POST olması gerekir.

Controller'daki GET action metodu, formu bize/kullanıcıya getirecek/gösterecek olan metotken, formu doldurup/bilgileri girdikten sonra, o formu karşılayacak olan metotta POST action metottur. CSHTML’de formdaki input değerinin formun tetiklenmesi sonucunda değerini ilgili server’a gönderip değerini yakalayacaksam bu inputa bir tane name değeri vermem gerekiyor. Name, form içindeki ilgili inputların datalarını ayırabilmek için kullanılan bir parametredir. Dolayısıyla formdaki inputları name’ler ile ayırabilmek gerekir. Form tetiklendiği zaman hedef endpoint neresi ise form içindeki tüm inputlar, name değerlerine/isimlerine karşılık ayrılacak ve ilgili sunucuya gönderilmiş olacak.

Formun request neticesinde taşıdığı dataları POST action’unda nasıl yakalayabilirim? Action metota parametre girerek demiştik. AspNet.Core.Http ile gelen IFormCollection ile (IFormCollection datas) POST edilen formun içindeki tüm input nesnelerinin dataları yakalanabilmektedir ve datas üzerinden biz bu dataları name değerlerine göre ayırt edip yakalayabiliyoruz. Yakalanan input adına (name kısmına) keys kısmından bakabiliyoruz.

![25-1](https://github.com/user-attachments/assets/73fe8f5b-2eb3-400e-8667-25d2e46d1210)

![25-2](https://github.com/user-attachments/assets/7dc51800-f396-40da-a21c-06ec0a8eb204)

Gelen değeri görmek/kullanmak için ise datas[inputname] indexer'ı ile alıyorsun ve duruma göre string’e çeviriyorsun.

✨ Diğer yöntem ✨



Name değerleri ile eşleşmiş parametreler ile bu değerleri karşılayabiliyoruz. Action parametreleri ile form inputundaki name isimlerinin aynı olmasına dikkat etmeliyiz ki otomatik olarak bind işlemi gerçekleştirilebilsin.


✨ Diğer yöntem ✨



Kullanıcıdan gelen değerleri bu değerlere karşılık gelecek bir tür ile class/struct/record bunlardan herhangi birinin instance’ı ile yakalayabiliyoruz. İlgili sınıfın property’lerinin form input name ile aynı olmasına dikkat etmeliyiz. Formdan gelecek olan input değerlerinin name’lerine karşılık property’ler barındıran bir class tanımlarsak ve bu class’ı action metotta tür olarak parametresinde kullanırsak nesne üzerinden gelen verileri yakalayabiliriz.

👉 ! Form üzerinden bind edilmiş verileri almayı inceleyeceğiz:



Form üzerinden bind edilmiş verileri alabilmeniz için ilgili view’de input’a karşılık binding işlemi gerçekleştirmek gerekiyor. Eğer ki bu input’a karşılık bind işlemi gerçekleştireceksem, eğer ki binding edilmiş dataları kullanıcıdan alacaksam eğer burada yapmam gereken işlem view’ın @model’ını belirlemek/türünü belirlemek ve bunu input alanlarına asp-for ile bind etmek.

Peki Product’ta bind ettiğimi illa Product’ta yakalamak zorunda mıyım? Aslında değilsin. Çünkü Product’ta bind ettiğin, Product’ta yakalanmasının kolaylaştırıcı unsur olduğunu gör ama aslında veri taşınırken herhangi bir türe bind ettiğinde ilgili input oluşturulurken ona name değerleri veriliyor. Açılan formda kaynağı incele dersek görebiliriz. Foto2... Bind ettiğimiz property’ler ne ise input’lara name değeri olarak ilgili property’ler verilmiştir. Bunu artık POST ettiğimde bu property’lere karşılık gelen/ya da buradaki name’lere karşılık gelen property’ler barındıran bir sınıfta karşılıyorsam yine ilgili sınıf karşılayacaktır.

Bind’da oluşturmuş olduğun input’ları farklı bir türde yakalayabiliyorsun. Ama ideal olan bind’da hangi modeli kullandıysan POST neticesinde o model türünde ilgili dataları karşılamaktır. Ama bazen ihtiyaca göre farklı kullanman gereken bir tür olabilir. İşte bu durumlarda da türe bağımlı kalmadan kullanabilmek mümkündür. Bind etmiş olduğun property’lerine karşılık name değerinde input oluşturulacağından dolayı o name değerlerini barındıran farklı bir türle de karşılama yapabiliyorsun.


👋 26- Kullanıcıdan Veri Alma Yöntemleri - QueryString Üzerinden Veri Alma



Belirli verilerimizi gizli formatlarda taşımayı tercih ediyoruz ama bazı veriler vardır ki güvenlik gerektirmeyen bilgilerdir ve URL üzerinde hızlı bir şekilde taşıyabiliyoruz. URL üzerinde taşımamızın sebebi yapılan istek neticesinde sunucuya hızlı bir şekilde eriştirebilmektir.

👉 ! QueryString: Güvenlik gerektirmeyen bilgilerin URL üzerinde taşınması için kullanılan yapılanmadır.

Bir web sitesine girdiğinizde https://....com/sehir/ankara şeklinde domain yapılanması olur. Ama https://....com/sehir/ankara?ilce=2 şeklinde kullanım olursa buradaki ? ve sonrası QueryString yapılanması oluyor/URL üzerinden taşınan veri oluyor.

![26-1](https://github.com/user-attachments/assets/fd6b3216-dda4-4d07-9fce-2603b3b00047)

QueryString sadece kullanıcıdan veri almakta değil, esasında ilgili yazılımın/uygulamanın istek yapacağı servislere yahut sunuculara bu isteklerle hızlı bir şekilde veri taşımasını sağlayan yapılardır.

QueryString için, normalde kullanıcı değil, sen yazılımsal operasyonel neticesinde QueryString’e değerler koyabilir ve bu değerleri ilgili işlemlerde kullanabilirsin.

👉 ! Nasıl kullanabiliyoruz bunu inceleyelim:



QueryString yapılanmasını uygulamada gösterebilmemiz için öncelikle şunu bilmemiz gerek. QueryString bir POST işleminin sonucu değildir. QueryString’te bir değer taşıyorsak bu değer illaki POST’la değil, herhangi bir istek neticesinde taşınabilir.

QueryString, yapılan request’in türü her ne olursa olsun QueryString değerleri taşınabilir. Yani sen hedef sunucuya/endpoint’e istek mi yapıyorsun, o isteğin türü ne olursa olsun QueryString değerlerini verip sunucuya gönderebilirsin.

👉 ! Tarayıcı üzerinden hızlı bir şekilde GET isteğinde bulunabiliyoruz ama POST için form tasarlamamız gerekiyor.

GET metodu ile tarayıcı üzerinden hızlı bir istekte bulunalım. Bu istek neticesinde ilgili GET action metodunda QueryString değerlerini nasıl elde edebiliyoruz, bunu inceleyelim:

GET metodunda istekte bulunacağım ve bulunurken QueryString değerlerini ilgili URL’ye yerleştireceğim. Şimdi, URL üzerinden QueryString parametresi tanımlamak istiyorsanız URL’in en sonuna ? koyuyorsunuz ve bundan sonra QueryString parametrelerini tanımlayabiliyorsunuz.

![26-2](https://github.com/user-attachments/assets/f902d06e-b081-425b-9e31-7762bc14f4ce)

VeriAl endpoint’i tetiklendi ve bize gelen request’teki QueryString değerleri gönderilmiş olacaktır. Dolayısıyla biz burada QueryString değerlerini istediğimiz şekilde kullanabiliriz.

QueryString değerlerini yakalamak istiyorsanız, parametre üzerinden ilgili QueryString’e karşılık gelen bir parametre tanımlayabilirsiniz. Örneğe göre biz string a diyoruz.

![26-3](https://github.com/user-attachments/assets/adf3bc22-452a-4d72-8066-c5af7feb5fcb)

Kullanıcıdan gelecek olan parametre birden fazla olabilir. Bu durumda ise & operatörünü kullanarak yapıyoruz. 

![26-4](https://github.com/user-attachments/assets/2e73d6e7-8c40-4e58-a0ff-a1d845596902)

👉 ! Dikkat edilmesi gereken bir nokta da şu: QueryString’te 2 farklı string değer varsa, action parametresinde de string ile karşılaman gerek. Ancak QueryString’te biri int, biri string ise action parametrede yine 2 farklı string ile karşılayabilirsin. Gelen int ifade stringe dönüşerek tutulabilir/karşılanabilir. Fakat gelen string olsa ve sen int ile yakalamak istersen o zaman problem olur. Herhangi bir hata vermez ama ilgili parametre değeri yakalanamaz. Ayrıca QueryString’te gelen tüm parametre değerlerini karşılamak da önemlidir.


QueryString’ten gelen değerleri, action metotta parametreyi boş bırakarak da gelen request’in içine girerek karşılayabiliriz/QueryString değerlerini okuyabiliriz. Peki nasıl yapacağız? Gelen request’in içine girebilmek istiyorsanız, direkt metot içine Request yazmanız yeterlidir, base class’tan gelen bir property’dir Request. Ya da HttpContext.Request ile de yakalayabiliriz.

"Request." dediğimizde "Query, QueryString" property’leri çıkar ve gelen request’ten QueryString ile ilgili tüm bilgileri veren property’lerdir. 

![26-5](https://github.com/user-attachments/assets/48997271-5dd4-4a25-bc70-f3741053e466)

👉 ! Peki QueryString nedir? 


Request yapılan endpoint’e QueryString parametresi eklenmiş mi, eklenmemiş mi bununla ilgili bilgi verir. Eğer ki eklenen verilere request üzerinden erişmek istiyorsanız, buna da Request.Query üzerinden erişirsiniz.

Request.Query bize birden fazla QueryString gelebileceğinden IQueryCollection tipindedir. Dolayısıyla sana gelen QueryString’e erişebilmek istiyorsan indexer kullanarak string olarak ve ToString() ile stringe çevirerek ilgili değeri alabilirsin. 

![26-6](https://github.com/user-attachments/assets/8ce65162-0293-45f0-ac98-cc0c905af1cd)

En az bir tane QueryString olduğu zaman HasValue değeri true dönecektir.

![26-7](https://github.com/user-attachments/assets/55b7e1db-2492-4bee-be7b-6be44eb807ef)

✨ Diğer yöntem ✨



QueryString parametrelerine/o parametrelere karşılık gelecek property isimlerini barındıran bir tür tanımlamak yeterli olacaktır. Bunun için model tasarlıyoruz ve action metot parametresinde model türünde parametre kullanarak QueryString değerleri uygun bir şekilde eşleştiriliyor. Değerler model tarafından yakalanıp bizlere tek bir instance’da getirilmiş oluyor.

![26-8](https://github.com/user-attachments/assets/e6b023dd-c545-4126-8625-80696c3e8ef3)

![26-9](https://github.com/user-attachments/assets/02692a34-ed72-473e-927a-99e3909bb329)


👋 27 - Kullanıcıdan Veri Alma Yöntemleri - Route Parametresi Üzerinden Veri Alma



Startup.cs’de Configure içinde UseEndpoints middleware’i içinde, client’tan server’a gelecek olan isteklerin rotalarını belirliyorduk. Peki, route parametreleri nedir?

Bu rota üzerinde biz değerler taşıyabiliriz. Aynen QueryString gibi. Rotanın içine belirli değerleri gömebiliyoruz/kullanabiliyoruz. Bunlarla beraber istek yaptığımızda ilgili değerler sunucuya gönderilmiş oluyor. QueryString’e çok benzemiş olur.

Peki, nasıl değerler gönderebiliyoruz? Rotalar zaten kendi fıtratında parametrelerden oluşuyor. Default olan rotaya bakarsak, bizzat parametrelerden/değerlerden oluşan rotalardan ibaret:

👉 ! controller/action/id bunların hepsi birer parametredir.

![27-1](https://github.com/user-attachments/assets/062caf4b-3e7b-4f48-8545-ad5e49d357d2)

Dolayısıyla, rotalarda custom parametreler tanımlayıp o parametreye uygun koyduğumuz değeri sunucuya gönderebiliyoruz.

👉 ! Peki, bunun QueryString’ten ne farkı var? 

![27-2](https://github.com/user-attachments/assets/063608dc-8162-43a0-801e-1e1780d9936c)

QueryString, güvenli olmayan verilerde kullandığımız bir veri taşıyıcıyken, route’lara yerleştirdiğimiz gömülü parametrelerde en azından güvenlik bir nebze olsun sağlanabilmektedir. Örnekte de ikinci route kullanımında, Max’in name değeri olduğu bilinmemektedir. Daha uygun/güvenli/gizli formatta URL oluşturmamızı sağlıyor.

👉 ! Route üzerinde taşınan veriler nasıl yakalanır?

Route üzerinde veri taşıyabilmek için, route’un ilgili veriyi karşılayabileceği bir parametreye ihtiyacı vardır. Eğer ki default’u kullanıyorsak id parametresi vardır. id haricinde bir şey/parametre olmasını istiyorsan, işte bu durum özelleştirmeye giriyor. Yani artık custom rotalar oluşturmamız gerekiyor.

Önce route yapılanmasında id üzerinden parametre/değer taşımayı inceleyeceğiz. Devamında özel rotalar oluşturup bunların incelemesini yapacağız.


✨ Default'taki Var Olan id İçin İnceleme ✨



Default olarak id parametresi var. Bu id parametresine yerleştirilen değeri action metotta yakalamak istiyorsam, yapmam gereken sadece rotaya uygun/yakalamak istediğim parametreye uygun bir değişken tanımlamak.

Id yi string, int, object hangisinde istiyorsan karşılayabilirsin ve parametre adıyla birebir aynı ismi vererek action metot parametresine yazıyorsun/oluşturuyorsun. 

![27-3](https://github.com/user-attachments/assets/2303cc5b-a12c-4e27-af9d-d3a8b8bd1327)

Parametre adı ile route’tan gelecek olan parametre adı birebir aynıdır ve bu şekilde id parametresi değerini yakalamış oluyoruz. 

![27-4](https://github.com/user-attachments/assets/e1d55c8c-0624-487d-8c0f-1045fc319f67)

![27-5](https://github.com/user-attachments/assets/f43fe43f-0259-444c-bb78-fdeabe1d503a)


✨ Custom Rota Oluşturarak İnceleyelim ✨



"endpoints.MapControllerRoute()" ile özel rota belirleyebiliyoruz. Öncelikle rotamıza isim veriyoruz. Ardından pattern/şablon/şeması nasıl olacak, bunu {} içinde yazıyoruz.

![27-6](https://github.com/user-attachments/assets/22b52687-35c6-467d-85e9-c98b0380e39a)


Controller action içinde ise parametre kısmında, tek tek route’ta kullandığımız parametreleri yakalıyoruz. 

![27-7](https://github.com/user-attachments/assets/b373cc10-57e4-4abb-ac73-159f4ed27e6f)

Aynı zamanda sınıf/model üzerinden de yakalayabiliyoruz.

![27-8](https://github.com/user-attachments/assets/d62d8f1a-eeff-431b-b322-fd6a768d4f4a)

![27-9](https://github.com/user-attachments/assets/d15dec46-59fd-40e8-a887-1033a0b5c708)

![27-10](https://github.com/user-attachments/assets/9ca3d2b2-66d3-4289-bcba-3c90497391af)

Dikkat edilirse A = 0 oldu, ancak hata vermedi. Aslında string gönderdik ama modelimizde int tanımlı olduğu için A = 0 oldu.


👉 ! QueryString ve Route Farkı, route yapılanmaları, veriyi daha gizli taşımayı sağlıyor.

Oluşturduğumuz URL’lerdeki route parametrelerine ve QueryString değerlerine nasıl TagHelper ile değer atayabildiğimizi inceleyeceğiz.

![27-11](https://github.com/user-attachments/assets/47d02e33-d61c-49ab-b08c-a3dfde50403d)

Buradaki değerler bizim rotamızda parametre olarak tanımlandığından, vermiş olduğumuz değerler rotaya uygun bir şekilde yerleştirilecektir.

Ayrıca senin tanımladığın rotada olmayan bir parametre, route’ta yoksa eğer, QueryString olarak yerleştirilecek/kullanılacaktır. Buradaki x gibi.


![27-12](https://github.com/user-attachments/assets/1fa6e87b-e4bb-460b-bf43-05eacaba44c2)

![27-13](https://github.com/user-attachments/assets/f2574a64-e33d-4ba1-952b-d06a0aca0f6f)



👋 28 - Kullanıcıdan Veri Alma Yöntemleri –  Header Üzerinden Veri Alma



Kullanıcının göndermiş olduğu request/HTTP isteğinde bulunan veridir. Header'lar genellikle ilgili istekle alakalı nitelikleri barındırır. Header'lar, isteklerde belirli verileri taşımamızı sağlayan nitelendirici kalıptır/başlıklardır.

Postman, yapısal olarak bir istekte bulunmamızı sağlayan bir arayüz tanıyor bize. Öncelikle route belirliyoruz ve ona göre ilgili sunucuya istekte bulunuyoruz.
Header'lar, request üzerinden Headers property'si üzerinden yakalanır. "Request.Headers" şeklinde. Uygulamayı çalıştırdığımızda Kestrel sunucu ayağa kalkıyor ve route dizinini sana veriyor. 

![28-1](https://github.com/user-attachments/assets/6b119577-954e-45bf-a47e-8ad3da178560)

![28-2](https://github.com/user-attachments/assets/f5e0e22d-f977-4652-8f79-2254d0b27879)

Postman'da isteği yazdık ve Headers kısmına Key (Adi) - Value (Gencay) diyerek istekte bulundum. Action'da ise bu bilgileri Headers kısmında görebiliyorum. 

![28-3](https://github.com/user-attachments/assets/6a87a8b3-48ef-45b2-bd90-c933091c505e)

Header'da taşınan veride Türkçe karakter olmamalıdır.



👋 29 - Kullanıcıdan Veri Alma Yöntemleri –   AJAX Tabanlı Veri Alma


👉 ! AJAX, client tabanlı istek yapmamızı sağlayan ve bu isteklerin sonucunu almamızı sağlayan bir JavaScript temelli mimaridir.

Bir uygulamada client tabanlı çalışabilmek/AJAX tabanlı çalışabilmek için AJAX'ı destekleyen herhangi bir UI teknolojisi/kütüphaneyi kullanmak gerekir. Biz jQuery kullanacağız. jQuery'yi resmi sayfasından indirerek sıkıştırılmış olan linki alıp projemizde "script" tagı içinde "src" kısmına veriyoruz. Daha sonra CSHTML'de gerekli kodlarımızı yazıyoruz. CSHTML'de JavaScript objesi gönderdik POST içinde.

![29-1](https://github.com/user-attachments/assets/cbe45285-45b2-4fc3-8c49-f1329260ad52)

Action metotta yakalayabilmek için obje adıyla birebir aynı bir model/sınıf tanımlıyoruz ve o sınıf üzerinden Action metotta yakalıyoruz. Gelen JSON formattaki datayı ilgili türe dönüşümünü MVC mimarisi kendisi yapıyor.

![29-2](https://github.com/user-attachments/assets/0b8425d0-5025-4f67-b767-66233553d6a7)

AJAXData'ya deserialize işlemi gerçekleştirilmiş oluyor. Normalde bu dönüşüm yapılmasaydı, bizim Action metotta gelen veriyi string olarak karşılamamız gerekirdi ve metot içinde gerekli/uygun türe dönüştürmemiz gerekirdi.

👉 ! Dikkat edilirse Action metotun vermiş olduğu hata şu şekilde açıklanabilir: 


Public olan bir metotun dışarıdan erişilemez bir türe sahip parametresi olduğu için metot hata veriyordu. Dolayısıyla biz AJAXData sınıfını da public yapmalıyız.

Bir API'de çalışıyorsan ve kullandığın UI'in port adresi ya da protokol bilgileri değişiyorsa CORS politikalarına girmek gerekir. İleride incelenecektir.


👋 30 - Tuple Nesne Post Etme ve Yakalama


Tuple nesnesi, tek bir tanımlama ile içine birden fazla değer/nesneyi barındırabilen değişkendir. MVC mimarisinde genellikle View katmanında tekil nesneler model olarak kullanılsa da bazı durumlarda Tuple nesneleri model olarak kullanmamız gerekebilir.

Öncelikle bir View'ın herhangi bir türle bind edilebilmesi için modelin belirtilmesi gerekir. Eğer bu tür Tuple nesnesi ise yine de Tuple nesnesinin türünün bildirilmesi gerek.

![30-1](https://github.com/user-attachments/assets/372b4674-cb7b-486b-9e5d-d28810c79cb9)

Aynı zamanda asp-for da bizim türümüz Tuple olduğu için Item1, Item2 olarak geliyor. Hatırlarsanız, Item1, Item2 isimlerini değiştirmek istersek tür bildirirken istediğimiz ismi de bildirerek değiştirebiliyoruz.

View'da bind edilen nesne artık tekil bir nesne değil, içinde birden fazla değer barındıran bir Tuple nesnesi. Dolayısıyla Tuple nesnesini barındıran ve buna bind edilmiş bir View'ı/Formu post ettiğimizde, yakalayacak olan Action'da farklı bir bind işlemi yapmamız gerekecek.


✨ Yapılabilecek yanlışlıklar ✨

![30-2](https://github.com/user-attachments/assets/7ae9ae7a-7a19-436b-b1d3-1bc467768e15)

![30-3](https://github.com/user-attachments/assets/6ac3803f-1528-4376-af3d-279423ed2e6d)

CSHTML'deki türlere göre Action metotta ilgili nesneyi karşılamaya çalışırsak bu şekilde veriler gelmez/yakalayamayız.

Tuple nesnesi üzerinden bind işlemi yapacaksan, öncelikle Tuple nesnesinin içinde bulunan nesnelerin null olmaması gerekiyor. Tuple nesnesi içinde değerlerin olması gerekir. Peki bu değerleri nasıl vereceğiz? İlgili formu açacak olan GET Action metodundan veriyoruz.

![30-4](https://github.com/user-attachments/assets/447a6f89-fe7b-42ff-9b60-bd2845507cb5)

Şeklinde nesneler oluşturduk, içinde herhangi bir property'ye karşılık gelecek olan değer yok ama null da değildir. Artık property'ler direkt bind edilecektir.

Artık null hatası alınmayacaktır. Ancak proje çalıştırılıp formu doldurup gönder dediğimizde, ilgili nesnelerin Action metodunda karşılanamadığına dair/o nesneleri initialize edemediğine/oluşturamadığına dair hata verecektir.

👉 ! O zaman nasıl karşılayacağız?



CSHTML'de türleri, Action metodunda ayrı ayrı parametre olarak tanımlamalıyız.

![30-5](https://github.com/user-attachments/assets/be3ab6be-a2d9-433a-9af9-7a9c222b12c0)

Ancak bu şekilde değişiklik yaptığımızda da Action metot isteği karşılamış ama verilerin içi null, yani bind işlemi CSHTML tarafında yapılırken Action metotta neden yakalayamadık?

Gönderilen data Tuple türünden olduğu için, Action metotta bizim hangi nesneye ait parametre olduklarını Item ile bind ederek [Bind(Prefix="Item1")] şeklinde bildirmemiz gerekecek.

![30-6](https://github.com/user-attachments/assets/1e42b029-9f90-4b4c-ade1-72f3ab181248)

👉 ! Burada önemli detay:



CSHTML'de Item1 için Product ismini kullandık, peki Action metotta neden vermiş olduğumuz "product" adını kullanmadık da Item1 kullandık?
Biz CSHTML'de her ne kadar farklı isim versek de, Prefix ile bind ederken soldan sağa Item1, Item2 ... olacak şekilde isimlendirmek gerekiyor.

Bu işlemlerden sonra Tuple nesnesi artık Action metot tarafından karşılanabilir hale gelecektir.
