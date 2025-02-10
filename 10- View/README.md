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

✨ Veri Taşıma Kontrolleri - ViewBag ✨ 

![17-7](https://github.com/user-attachments/assets/00c39123-1f86-4851-b14c-df453e5c504e)

![17-8](https://github.com/user-attachments/assets/580283b2-92cb-49a9-80c9-8130e3d0d19f)

View'e gönderilecek/taşınacak datayı dinamik şekilde tanımlanan bir değişkenle taşımamızı sağlayan bir veri taşıma kontrolüdür.
ViewBag, ViewData ve TempData'ya erişim sağlayabilmek için Controller'da, yani base class'ımızdaki tanımlanmış olan bu property'leri kullanır.

![17-9](https://github.com/user-attachments/assets/e6afe8d8-65b3-491e-9986-b7557ecc7ad8)

![17-10](https://github.com/user-attachments/assets/032f06e6-270d-44e7-96af-98c10c48d572)

![17-11](https://github.com/user-attachments/assets/4e4909c6-cce2-42da-a2f6-839af7032b8a)

Ben eğer ki action içinde ViewBag. deyip herhangi bir değişken tanımlarsam, örneğin ViewBag.Ahmet dersem, view'e "Ahmet" olarak gidecektir. Bu çalışma sonucunda hangi view'e render ediliyorsan, o view'e ViewBag ile veri gönderilmiş olur. Controller ve view kısımları görseldeki şekildedir.

![17-12](https://github.com/user-attachments/assets/92c216b2-910e-4b0b-8ee1-2190949467f8)

Burada gelen datamız dinamik olduğu için runtime'da şekillenecektir. Runtime'da türü belli olacak. Bizim derleme zamanında, yani development aşamasında da bu türü belirleyebilmemiz için ilgili dönüşümü sağlamamız gerek. as List<..> kısmını <li> kısmında @Product. dediğimizde değerlerin bu şekilde gelebilmesi için development aşamasında türünün belli olması gerekiyordu ve o yüzden bu şekilde yazdık.

Diğer türlü türünü belirtmeseydik, as List ile . dediğimizde herhangi bir şey gelemeyecekti çünkü dinamik olduğu için tür runtime'da belli olacaktı.


✨ Veri Taşıma Kontrolleri - ViewData ✨ 

ViewBag'de olduğu gibi action'daki datayı view'e taşımamızı sağlayan bir kontroldür. İlgili datayı boxing ederek taşır. ViewData, indexer ile kullanılıyor.
ViewBag, ilgili datayı dynamic ile yani runtime'da türü belli olacak şekilde taşıyordu. ViewData ise ilgili datayı boxing ile taşıyor. Dolayısıyla view'da senin bu datayı unboxing ederek taşıman gerekecektir.

![17-13](https://github.com/user-attachments/assets/d502563f-7305-4fde-b655-6fc74dbcf2b6)

Burada ViewData object olarak değer alır, yani kullanmak istersen unboxing yapmalısın. as ile ya da cast ile unboxing edebilirsin. 

![17-14](https://github.com/user-attachments/assets/6eb16790-11ef-4cfc-b2fd-fa65107827d5)


✨ Veri Taşıma Kontrolleri - TempData ✨ 


ViewData'da olduğu gibi action'daki datayı view'e taşımamızı sağlayan bir kontroldür. İlgili datayı boxing ederek taşır. Yine indexer olarak kullanılır. View'da unboxing yaparak kullanmanı bekler. Peki, TempData ve ViewData arasındaki fark nedir?

Biz action'larda kendi aralarında yönlendirme yapabiliyoruz. Örneğin, Index action'ı işlemleri bitirdikten sonra kullanıcıya response göndermeden önce başka bir action'a daha giderek/redirect işlemi gerçekleştirilebiliyoruz/yönlendirilebiliyoruz. O action'da da operasyonlar gerçekleştirdikten sonra kullanıcıya response dönebiliriz. Böyle bir durumda farklı bir action'a yönlendirme söz konusu olursa TempData kullanılır. TempData yapılanması arka planda esasında bir cookie kullanılır. Cookie üzerinden veri taşır.

![17-15](https://github.com/user-attachments/assets/d0f90628-48af-4640-af00-2f7f805be6ef)

Burada TempData bir cookie oluşturmuş.

TempData için gelin yönlendirme kısmını inceleyelim.

![17-16](https://github.com/user-attachments/assets/a2b2fd6e-a8f3-4a69-a33f-18410a3cd28e)

Burada Index2 action'ına yönlendirmiş olduk. Eğer controller adını da vermek istersen 4. overload'da çıkar. Controller belirterek de ilgili controller altındaki action'a yönlendirme yapabilirsin.

![17-17](https://github.com/user-attachments/assets/b353eb01-3787-4afb-a8f1-14c599e8f4b3)

TempData'da yönlendirme esnasında bir nesne/koleksiyon kullanıyorsan, yani başka controller altındaki action'a ya da farklı action'a gönderecek veri nesnesi ise bu atayı evridir. Dolayısıyla bizim bu nesneyi bir şekilde serileştirmemiz gerekiyor. İlerleyen başlıklarda açıklamasını yapacağız.

![17-18](https://github.com/user-attachments/assets/54a6335f-dbb4-4a75-8023-f607acac6afb)

Burada complex/nesne değil de direkt değer ile taşıma işlemine bakacağız. Sadece TempData ile ilgili veri taşınmıştır, diğerleri null gelmiştir. Yani TempData, action'lar arasında veri taşımamızı sağlayan veri taşıma kontrolüdür. Peki, nasıl taşıyor bu veriyi? Hata sayfasında kaynağı incele dersek, cookie sayesinde veriyi taşıdığını görürüz.

![17-19](https://github.com/user-attachments/assets/6746ed0e-1931-4390-9af5-42756e4e1822)

TempData, cookie üzerinden veriyi taşıyor. Dolayısıyla, cookie'ye ilgili verinin dönüştürülebilmesi yani serialize edilebilmesi gerekiyor. Serialize edilebilmesi için basit türlerde sıkıntı yok ama bu nesne/complex tür olursa burada ekstra bir maliyet olacaktır ve bunu normalde gerçekleştiremediği için proje patlar. Eğer ki taşımaya çalıştığımız veri complex type ise hata veriyor; complex türün cookie'ye dönüştürülemediğinden dolayı. Dolayısıyla bizim yapmamız gereken şu: TempData'ya complex tür vereceksek, bu complex türü de serialize ederek vermemiz gerekir. Bunun için de JSON serialize dediğimiz .NET 5.0'da gelen bir kütüphaneyi kullanabiliriz. Bu kütüphane üzerinden elimizdeki complex türü JSON formata serialize edebileceğiz. 

![17-20](https://github.com/user-attachments/assets/0c7718f1-ff99-4102-aeba-fe03a9330430)

![17-21](https://github.com/user-attachments/assets/aaa9cec3-1b2b-46c5-8ad6-cd6edc17ecea)

Bu işlemle artık serialize edilen complex değer, string formatta data'ya atanacak ve data değeri ilgili action'a gönderilecektir. İlgili action'da tekrar yönlendirme olmayacaksa orada kullanılacaksa, tekrardan deserialize işlemine tabi tutulması gerekir.

Yani ,

![17-22](https://github.com/user-attachments/assets/434703eb-bfad-4f90-b9d5-8f93cf7c980f)

Buradan ne olarak elde etmek istiyorsam, generic olarak da bildiriyorum. Aynı zamanda bizim TempData'ya verdiğimiz değer object olarak geleceğinden, önce bunu string olarak elde etmeliyiz. Ondan sonra deserialize için string olarak elde edilen datayı veriyorum.


👋 18 - View'e Tuple Nesne Gönderimi ve Kullanımı


Controller'da elde edilen bir Tuple nesnesinin nasıl View'e gönderildiğini inceliyor olacağız. Controller'da üretilen Tuple nesnesi birden fazla nesneyi tarif eden bir nesne olacağı için, bunu bu semantikle View'e nasıl taşıyabildiğimizi ele alacağız. Birden fazla değeri bir Tuple olarak kullanmaksızın veri taşıma kontrolleri ile de verileri taşıyabiliriz.


✨ Tuple Nesnesi ✨


İçinde birden fazla değeri/veriyi/nesneyi referans edebilen ve semantik açıdan dilin bize kazandırmış olduğu söz dizimine sahip olan bir nesnedir. Şöyle düşünebilirsin: Biz birden fazla veri/nesneyi bir bütün olarak kullanabilmek için ne yapıyoruz? ViewModel dediğimiz modelleri tasarlıyoruz. Bir ViewModel üzerinde birden fazla nesneyi referans edip temsil edip tek bir nesne üzerinde kullanabiliyoruz. Ya da Tuple syntax'ı ile hızlı bir şekilde ViewModel gibi değerler üretebilirsiniz.


![18-1](https://github.com/user-attachments/assets/7105d8a0-62c7-4f4a-8230-832b085e3bac)

Biz şunu yapacağız: Action içinde 2 farklı nesne var, bu nesneleri tek seferde ilgili View'a göndereceğiz. Bunu normalde 2 farklı işlemle yapıyoruz: biri Tuple, diğeri ViewModel.

ViewModel ile taşımak istersek: Öncelikle yapmam gereken bir ViewModel oluşturmak. Models klasörü altına ViewModels adında klasör oluşturuyorum ve içinde UserProduct adında sınıf oluşturuyorum. Aslında göndereceğim 2 farklı nesneye referans edebilecek bir sınıf/nesne oluşturuyorum.

![18-2](https://github.com/user-attachments/assets/ca4fffbe-4b1a-4aa9-96d4-4d18f8f49eaa)

Burada referanslara vermiş olduğum ilgili nesneleri UserProduct nesnesi üzerinden kullanacağım/erişebileceğim ve biz buna ViewModel diyeceğiz.

![18-3](https://github.com/user-attachments/assets/1c3c6029-076d-4d5e-99bc-26fc82827e0e)

İlgili Action içinde, UserProduct'ta oluşturduğum ilgili property'lere elimdeki nesneleri referans ederek ViewModel ile çalışabiliyoruz. UserProduct'ı da View ile return ediyoruz.

![18-4](https://github.com/user-attachments/assets/08f31e3d-9779-4087-a31f-bdc9769f8864)

GetProduct.cshtml kısmında ise namespace ile gelecek olan verinin türü belirtildi ve kullanıldı.

👉 ! Tuple nesnesi ile nasıl yaparız:

![18-5](https://github.com/user-attachments/assets/24c5cdd6-d3d6-4d03-ab2c-8ba38060b51d)

Yine ilgili Action içinde Tuple nesnesi olarak nesnelerimizi verdik. View ile de return edip gönderdik. Bu nesne View tarafında karşılanacaktır. View kısmında gelen nesnenin türüne göre tanımlama yapıyorduk/tür bildiriyorduk. Gelen nesne Tuple olduğu için birden fazla nesne içerdiğinden

![18-6](https://github.com/user-attachments/assets/500dbe88-d24a-4d87-be9c-81c48ea007a3)

şeklinde türlerimizi bildirdik. Bu nesneleri kullanmak istediğimizde @Model kısmında Item1, Item2 şeklinde kullanım olacaktır. Editör bunu soldan sağa hizalı olarak atamalar yapıyor. Yani Product için Item1, ... şeklinde oluyor.

![18-7](https://github.com/user-attachments/assets/ec314f7b-531a-46ff-a9ac-778fe107a971)

Ama sen bunları Item1 ... şeklinde değil, kendin isim vermek istersen tür bildirirken bunları da bildirmen gerek.
