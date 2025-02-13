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
