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
