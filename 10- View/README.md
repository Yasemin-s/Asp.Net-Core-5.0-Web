👋 17 - View Yapılanması ve Viewe Veri Taşıma Kontrolleri - ViewBag/ViewData/TempData

View ile Controller arasındaki ilişkinin nasıl olduğunu, request sonucunda Controller'da elde edilen/üretilen verinin View'e nasıl gönderildiğini/taşındığını ve ilgili verilerin amaç doğrultusunda nasıl render edildiğine odaklanacağız.

✨ View Nedir ? ✨ 

ASP.NET Core MVC uygulamalarında, Controller'da üretilen verinin görselleştirildiği, JS, CSS gibi araçlar kullanılarak render edildiği katmandır. Bu katmana özel geliştirilmiş bir formatta/uzantıda olan dosyaya "View" denir. View dosyalarının uzantısı .cshtml olup sadece ASP.NET Core'da çalışır, evrensel değildir.

.cshtml, View dosyasının uzantısıdır. Yani Controller'da üretilen verinin görselleştirileceği dosyaların karşılığıdır. C# ile HTML üzerinde kodlama yapabilmemizi sağlayan özel bir format geliştirilmiştir ve buna .cshtml denmiştir. C# ve HTML'in birleştiği bir alandır. Siz HTML'i C# ile kodlayabilir ve çıktı olarak/render edildikten sonra yalnızca HTML elde edersiniz. View dosyalarını render ettikten sonra C# kodlarını göremezsiniz, çıktı olarak sadece HTML elde edilir. Dolayısıyla bizim C# kullanarak UI tabanlı çalışmalar yapmamızı sağlayan teknoloji View teknolojisidir.

Peki burada kullandığımız asıl teknolojinin adı nedir? HTML içine C# kodlarını yazmamızı sağlayan bu teknolojinin adı Razor teknolojisidir ve Microsoft tarafından geliştirilmiştir.

✨ View Dosyaları ✨ 

View dosyaları, datalarımızı görselleştirebileceğimiz CSS ve HTML ile kullanabileceğimiz dosyalardır. Bir projede View dediğimiz dosya nerede bulunur? View dosyaları genellikle Views klasörü altında bulunur. Çünkü ASP.NET Core mimarisinde MVC'de Action'ların karşılıkları olan View dosyalarını belirli bir ezbere format üzerinden bulmaktadır. Views klasörünün altında Controller adında bir klasör vardır ve onun altında da Action ismine karşılık gelen .cshtml uzantılı dosyalar ilgili Action'un View dosyaları olarak varsayılan kabul edilir. Mimari bu şekildedir. Bu yüzden View'lerimizin Views klasörü altında olması ilk etapta gerekiyor, ama bu şart değildir.

Nasıl ki Controller'lar Controllers klasörü altında bulunmasına gerek yoksa, View'lerin de aslında Views klasörü altında bulunmasına gerek yoktur. View'i farklı bir klasör altına koysan bile View() fonksiyonu ile o dizini/farklı klasörün dizinini belirterek ilgili View'i tetikleme şansın vardır. Dolayısıyla buradaki varsayılanın dışına çıkabilirsin. Ama biz View'leri Views klasörü altında kullanacağız.

✨ Klasör Yapısı ✨ 

View klasörü altında bir View dosyası tutmak istiyorsanız, ilgili Action'a karşılık olarak tutmanız gerekiyor. Bunun için de Controller'a karşılık bir klasör ve ilgili Action'a karşılık o klasör altında Action isminde .cshtml uzantılı bir dosya olması gerekiyor.

![17-1](https://github.com/user-attachments/assets/820428a9-a12a-4666-b8b6-f7baa395eedb)

![17-2](https://github.com/user-attachments/assets/a7d6531e-6857-4cda-a284-7aa09820c653)

Bir Action için daha .cshtml dosyası oluşturacağız, fakat bu defa Razor View Empty değil, Razor View olarak oluşturuyoruz. Razor View ile bize bir template geliyor. Ekleme işlemi yapacaksan Create, silme işlemi için Delete... şeklinde oluşturabiliyorsun. Eğer bir template seçtiysen kullanılacak olan modeli de bildirmen gerek.


👉 ! View, verileri görselleştirmemizi, Controller ise gelen request sonucunda verileri oluşturmayı sağlıyor ve oluşturulan veriyi View'a gönderip bir yerde kullanmamız gerek. View'de peki nasıl kullanacağız? Yani View ve Controller arasındaki ilişkinin nasıl olduğunu ele alacağız.

![17-3](https://github.com/user-attachments/assets/1b7ba572-ab81-4546-8744-700b710486fc)

👉 ! Bir .cshtml dosyası üzerinde hem HTML hem de Razor ile C# kodlaması gerçekleştiriyorsunuz. Burada gördüğümüz @ bizim için Razor operatörüdür. Razor, bizim için .cshtml dosyası içinde C# kodlarını yazmamızı sağlayan teknolojidir.


✨ Controller ve View Arasında Bir Data Nasıl Taşınır ? ✨ 

Controller'dan View'e 4 farklı şekilde veri gönderebiliyoruz.
Biri model bazlı veri göndermek. Diğer 3'ü veri taşıma kontrolleri ile veri göndermektir. Model bazlı veri gönderme ile beraber biz ekstra kullanıcıdan veri alabilirken, veri taşıma kontrollerinde ise sadece Controller'dan View'e veri gönderme operasyonları yapılır.

✨ Model Bazlı Veri Gönderimi ✨ 


 Elimizdeki datayı, request sonucunda üretilen datayı View'e gönderip oradan render edebilmek için eğer ki model bazlı veri göndermeyi kullanacaksak, burada hem Controller'da hem de View'de yapmamız gereken bazı ayarlar vardır.

![17-4](https://github.com/user-attachments/assets/8cdcf08d-3e86-474a-b6d1-397a03a3dc97)

Controller'da yapılması gereken işlem şudur: Model bazlı verinin gönderilmesidir. Bunun için biz View fonksiyonunu kullanıyoruz. Eğer ki bir veriyi View'e model bazlı göndereceksek View fonksiyonunu direkt return etmek yeterlidir. View fonksiyonu, ilgili Action'a karşılık gelen View'i render edecek, bir yandan da sizin data göndermek istiyorsanız View fonksiyonu 2. overload'da bir model istiyor . Burada boxing işlemi ile gönderilecek.

return View(products);

Burada önemli olan datanın türüdür, adı değil. Bu şekilde kullanım ile model bazlı veri gönderme diyoruz.

View kısmında ise gelen model bazlı veri için şu ayarı yapmalıyız: View'e modeli bildirmek gerekir. Yani bu View'e gelecek olan modelin hangi türde olduğunu bizim bildirmemiz gerekir. Bunu da @model keyword'u ile yaparız:

@model List<OrnekUygulama.Models.Product>

Bu ifade ile sana gelecek olan modelin türü List<Product> diye bildiriyoruz. Controller'dan List<Product> geldiği için View'da da List<Product> olarak karşıladık.

Model keyword'u ile bu sayfaya, bu View'e gelecek olan datanın türünü bildirdikten sonra gelecek datayı ekranda kullanabilmek için @Model (M'si büyük) kullanacağız. Küçük m türü bildiriyor, büyük M ise gelen datayı bildiriyor/sana getiriyor. Dolayısıyla büyük Model, küçük model'dan türünü alıyor.

![17-5](https://github.com/user-attachments/assets/89d3c5c7-c023-4e96-ae72-bd33f267a982)

Burada büyük M, foreach içinde kullanılmıştır.

👉 ! Küçük model genellikle sayfanın en üstünde tanımlanır.

![17-6](https://github.com/user-attachments/assets/5b764496-697b-45a1-afbe-8513bd73571c)

Çalıştırdığımız View çıktısının kaynağını incele desek, C# kodları görünmez. Render sırasında C# kodları açıklanıyor ve sadece render sonucu, yani C# sonucu bize HTML çıktısı veriliyor.
