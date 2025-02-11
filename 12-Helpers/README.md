👋 20 - URLHelpers - HTMLHelpers Fonksiyonları

Yardımcı metotlarımız olan helpers'ları inceleyeceğiz. Helpers yapılanması ASP.NET Core MVC'de UrlHelper, HtmlHelper, ve TagHelper olarak üçe ayrılır.

👉 ! Neye Yarar Bunlar?


Helpers yapılanmaları, adı üzerinde yardımcı metotlardır.

👉 ! UrlHelper:


URL ile ilgili işlemler yaparken manuel olarak uğraşmak yerine hızlı bir şekilde bu işlemleri, rotalara uygun URL oluşturma gibi durumlarda sağlar.

👉 ! HtmlHelper:


HTML ile ilgili çalışmalarda yardımcı metotlar tanımlamaktadır.

👉 ! TagHelper:


HTML etiketleri ile ilgili ekstra yardımcı olan bir helper'dır.


👉 ! UrlHelper ve HtmlHelper, ASP.NET standart framework ile gelen helper'lardır.

👉 ! TagHelper ise ASP.NET Core mimarisinde eklenmiştir.

✨ UrlHelper ✨


ASP.NET Core MVC uygulamalarında URL oluşturmak için yardımcı metotlar içeren ve o anki URL'ye dair bizlere bilgi veren bir sınıftır. Metotlar ve property'ler ise şu şekildedir:

![20-1](https://github.com/user-attachments/assets/20c8455b-ca9a-4db8-9466-e71208620e3f)


✨ Action Metodu ✨


Verilen controller ve action'a ait URL oluşturmayı sağlayan metottur. Manuel olarak da link oluşturabilirsiniz, ancak Action metodu ile daha pratik bir şekilde oluşturulabilir.

👉 ! Controller veya View dosyalarında URL helper'a erişmek istiyorsanız Url property’sini kullanmanız yeterlidir.

👉 ! Base class'tan geldiği için ayrıca tanımlama yapmanıza gerek yoktur.


![20-2](https://github.com/user-attachments/assets/cb8dab20-cb48-44fe-a6d4-06c26e9c560c)

Hedef controller Product, hedef action Index ise ve varsa parametre tanımlamaları new { id = 5 } şeklinde verilebilir.
Çıktı olarak bize bir URL oluşturur.

👉 ! Action metodu, oluşturulacak URL’in ana dizinini oluşturmaz. Yani host bilgisi, port bilgisi ve protokol bilgisini vermez; sadece URL’in devamını oluşturur.

ASP.NET Core MVC ve Rotalar:

Rotalar, Startup.cs içinde UseEndpoints middleware'inde tanımlanır.
Rotaların yapısına uygun olarak Action metodu bize URL üretir.
Middleware'de controller ve action sıralaması nasıl tanımlandıysa URL de buna göre şekillenir.

ASP.NET Core MVC uygulamalarında rotalar Startup.cs dosyasındaki UseEndpoints middleware'i içinde tanımlanır. Buradaki rotalara uygun olarak action metotları çıktı üretir ve URL oluşturur.
UseEndpoints middleware'inde controller ve action sıralaması nasıl belirlenmişse, URL de buna göre şekillenir.


👉 !  MapControllerRoute: Kullanıcının kendi isteğine göre özelleştirebileceği ve tanımlayabileceği rota şablonudur.

👉 !  MapDefaultControllerRoute: Sistemin varsayılan olarak kabul ettiği, önceden tanımlanmış bir rota şablonudur.

"app.UseEndpoints(endpoints =>
{
    endpoints.MapControllerRoute(
        name: "default",
        pattern: "{controller=Home}/{action=Index}/{id?}");
});
" 
Bu yapı, varsayılan olarak Home controller'ındaki Index action metodu ile başlar ve id parametresi opsiyoneldir.


✨  ActionLink Metodu ✨


ActionLink, belirli bir controller ve action için URL oluşturmayı sağlayan bir metottur. Action metoduna benzer şekilde çalışır, ancak çıktısı farklıdır. Burada protokol, host ve port bilgisi de yer alır.

![20-3](https://github.com/user-attachments/assets/2b9f7279-ade9-4ad8-8306-e95f01c5e82e)

@Html.ActionLink("Anasayfa", "Index", "Home")

çıktısı : https://localhost:5001/Home/Index


✨ Content Metodu ✨


Statik dosyalar (örneğin CSS, JavaScript veya resim dosyaları) için proje içerisindeki dizinlere göre URL oluşturur.

![20-4](https://github.com/user-attachments/assets/fbde769b-e1cd-4951-95d4-8568394f2767)

<img src="@Url.Content("~/images/logo.png")" alt="Logo">

çıktısı : /images/logo.png

✨ RouteUrl Metodu ✨

Mimaride tanımlı olan rota isimlerine uygun şekilde URL oluşturan bir metottur. MapControllerRoute ile istediğimiz gibi rotalar oluşturabiliyorduk ve dikkat edilirse bu rotaların isimleri vardır.

![20-5](https://github.com/user-attachments/assets/5f4bf98c-988c-49d1-a50e-25454a51d5d2)

![20-6](https://github.com/user-attachments/assets/32701089-3c42-4430-87ad-96db420872e3)

Birden fazla rota olduğunda, isim belirterek uygun URL oluşturulabilir.

✨ ActionContext Özelliği/Property ✨


O anki URL'ye dair tüm bilgilere erişmemizi sağlayan bir özelliktir. Gelen isteğe dair bize bilgi veren bu property ile URL, controller, action gibi bilgileri elde edebiliriz.

![20-7](https://github.com/user-attachments/assets/3332d0c3-88dc-40da-8a4b-36efbedb1bcf)

✨ HTML Helper ✨


Hem maliyetli hem de performanslı yapılanmalardır. TagHelper'lar ise daha az maliyetli ve daha performanslı yapılardır.

HTML etiketlerini server tabanlı oluşturmamızı sağlayan sözde yardımcı metotları barındırmaktadır. Sözde yardımcı metot denmesinin sebebi, gereksiz yere servera yük bindirmesidir.

Hedeflenen .cshtml dosyalarını render etmemizi sağlar.
O anki bağlama (context) dair bilgiler edinmemizi sağlar.
Veri taşıma kontrollerine erişmemizi sağlar.

👉 !  Metotlar ve Property'ler:

![20-8](https://github.com/user-attachments/assets/b916a9d2-f2b3-48ed-baf8-e7b3850a1a40)

Buradaki TempData, ViewData ve ViewBag; veri taşıma kontrollerine erişebilmemiz için view üzerinde ekstra bir şey tanımlamamıza gerek kalmaz. HTML Helper üzerinden de erişim sağlayabiliyoruz.

✨ HTML Partial Metodu ✨


Hedef view'ı render etmemizi sağlayan bir fonksiyondur.
Controller'dan gelen istek neticesinde render etmek zorunda değilsiniz. Bir view içerisindeyken belirli bir noktada Html.Partial ile hedef view'i çağırıp onu render edebilir ve çıktısını o noktaya verebilirsiniz. Yani illa controller'dan istek gitmesine gerek yoktur.

![20-9](https://github.com/user-attachments/assets/a8288e4b-0138-423c-9b86-a52fef449dc0)



✨ Render Edilen View’e Model/Data Gönderme ✨


Render edilen view'e ilgili action'dan model/data gönderilebilmektedir. Örneğin bir istek geldi ve A controller içindeki B action'ındasınız. B action'ından B view'ına gittiniz, B view'ında C view'ını çağırdığınızı düşünelim. C view'ına data gönderecekseniz A'dan B üzerinden data taşımanız gerekir. C'yi tetiklediğiniz nokta B view'ıdır. B view'ında da partial üzerinden tetiklediğiniz için, eğer bir model/data ihtiyacı varsa bunu A üzerinden taşımanız gerekmektedir.


👉 !  Örnek:


Views altında Partials klasörü altına ListPartial adında bir view oluşturuyorum. Farklı bir view'e (GetProducts.cshtml) controller üzerinden render talebi geldiğinde, ilgili view'i render ederken bir yandan da ListPartial.cshtml'i render etmek istiyorsam, GetProducts.cshtml'de partial'ın dizinini de belirterek şu şekilde kullanırım: 

![20-10](https://github.com/user-attachments/assets/3c84714c-1826-45f2-97c2-9d78e1023a6d)


Aynı zamanda ListPartial'da belirli bir model/sınıf kullanmak istersek bu veriyi nereden alacağım? Veriyi, hangi controller üzerinde tetikleme gerçekleştiriliyorsa (GetProducts'ı tetikleyen controller) oradan almam gerekir. Controller'dan view'e (GetProducts) taşınan veri, GetProducts'ta kullanılan tüm partial view'lara da taşınır.


👉 !   Dikkat Edilmesi Gereken Noktalar:


Eğer GetProducts'a User adında bir model gönderecekseniz, bu normalde GetProducts.cshtml'deki partial view'e User adlı model gider. Ancak GetProducts'ta User adında bir model kullanıp, GetProducts içindeki partial view'da farklı bir model kullanmak/göndermek isterseniz, işte o zaman partial'ı çağırdığınız yerde 2. parametre olarak göndereceğiniz modeli belirtmeniz gerekir.

![20-11](https://github.com/user-attachments/assets/89048fc9-533b-46a5-bb3d-f1e52743ba70)

Yada ilgili modeli oluşturabilirsiniz.

![20-12](https://github.com/user-attachments/assets/26f3ec84-1e36-4978-b073-752a345f2f7a)


✨ Html RenderPartial Metodu ✨

![20-13](https://github.com/user-attachments/assets/b6f2520c-0ef0-4da8-829d-02b93765fcde)

Partial, scope'a gerek kalmadan tek satırda çağrılabilirken, Html.RenderPartial ise scope içinde çağrılmaktadır. Bunun sebebi, Partial geriye string döndürürken Html.RenderPartial void döndürüyor/yani bir şey döndürmüyor ve bunu da tetikleyebilmek için scope içinde C# kuralları ile kullanmak gerekir.
Html.Partial'a göre, Html.RenderPartial daha hızlıdır.

✨ Html ActionLink Metodu ✨

![20-14](https://github.com/user-attachments/assets/2a489599-442d-43f9-b1e4-e6a18704ab4b)

Hem çıktıyı verir hem de linki oluşturur.

✨ Html Form Metotları ✨

![20-15](https://github.com/user-attachments/assets/a45f7ea4-658b-4a5d-8fce-90d6d4550659)

Burada bir TextBox oluşturmak bile sunucu taraflı gerçekleşeceği için sunucuyu yorar/maliyetli olur. Bu maliyeti ortadan kaldırmak için Tag Helper dediğimiz yapılanmalar ortaya çıkmıştır.
ASP.NET Core MVC ile gelen Tag Helper yapılanmaları, Html Helper'lara göre daha hızlı ve daha efektiftir.


👋 21 - Custom HtmlHelper Fonksiyonu Oluşturma



Html helper'ların nasıl customize edildiğini, yani custom HtmlHelper oluşturmayı ele alacağız.
HtmlHelper'lar, HTML nesneleri oluştururken bize yardımcı olan, hazır metotlarımızı barındıran bir kütüphane/sınıftır. Dolayısıyla bu sınıf üzerinden oluşturduğumuz HTML nesneleri, server tabanlı olarak ilgili sayfayı view'e basabiliyoruz. Bunun maliyeti ve performans zayıflığı vardır. Eğer HtmlHelper'ları kullanıyorsak, varsayılan çıktıları özelleştirebiliyoruz.

![21-1](https://github.com/user-attachments/assets/140b1692-abda-4856-9a53-cbb9b89059cb)

HtmlHelper yapılanmasında TextBox ya da kullandığınız helper fonksiyonu hangisi ise, diğer overload'larına bakarsanız belirli farklı parametreler aldığını görürsünüz.

Biz TextBox nesnesi üzerinden örneklendirme yaparken htmlAttribute ile HTML attributeleri verebiliyoruz. 4. overload'u kullanıyoruz.
Attribute/Property'ye karşılık değerler oluşturulacak, yani generate edilecek olan HTML nesnesine, o input çıktısına attribute/özellik olarak eklenecektir.

![21-2](https://github.com/user-attachments/assets/c04619d7-fbd3-4b0c-b040-616355b23cb3)

![21-3](https://github.com/user-attachments/assets/e488bc9c-a966-40e9-9421-19bcde43e2c4)

Burada "a" verdiğim attribute, çıktıya value/attribute olarak eklenmiştir.

👉 !   Biz her HTML nesnesi talep ettiğimizde, talep ettiğimiz anda bunun ayarlarını vermek zorunda mıyız?


Eğer birçok noktada customize edilecek HTML formatlarına ihtiyaç varsa, biz custom bir şekilde sırf o işe odaklı HTML nesnesi oluşturabiliriz. Nasıl oluşturacağız? Bir extension oluşturarak yazacağız.

![21-4](https://github.com/user-attachments/assets/11fde0e9-5e21-46d9-943a-447011618349)

Extension metot yazmadan önce, HtmlHelper'larımızın türüne bakacağız. TextBox için bize IHtmlContent olarak sonuç dönüyor.
Demek ki benim customize edeceğim extension fonksiyonunun da IHtmlContent döndürmesi gerekiyor.

HtmlHelper üzerinde erişilebilir bir custom HtmlHelper oluşturacağım için, IHtmlHelper’a özel yazmam gerek. 

![21-5](https://github.com/user-attachments/assets/5bf6a255-28a6-442d-b7d9-ebc7691ecd26)

Dolayısıyla hangi türde bir extension oluşturacaksam (IHtmlHelper), bu extension hangi türde sonuç dönecekse (IHtmlContent), bu bilgilere göre artık rahatlıkla extension oluşturabileceğiz.

Başka bir deyişle, custom HtmlHelper'ımı tasarlayabilirim.


✨ Custom HTML Helper Tasarlama ✨


Proje altına Extensions adında bir klasör oluşturuyorum ve içine ismi önemsiz olmaksızın herhangi bir sınıf oluşturuyorum (biz Extensions adında sınıf oluşturacağız).
Extensions sınıfında extension metot tanımlayabilmem için ilgili sınıfı static olarak işaretliyorum.

Ardından static extension fonksiyonumu tanımlıyorum.
TextBox için IHtmlContent döneceğinden, oluşturacağım metoda ona göre dönüş türü veriyorum.
Bu metodu extension metot yapabilmemiz için, IHtmlHelper türünden bir this parametresi alması gerek.

![21-6](https://github.com/user-attachments/assets/1800ac03-47fd-4310-96db-b0e17ad1713f)

Artık bu fonksiyon, mimarideki IHtmlHelper türlerine extension olarak eklenmiştir.

Hangi HTML Helper nesnesi üzerinde çalışıyorsak, metottaki parametre bana o nesneyi getiriyordu.
En son geriye de TextBox’ı döndürüyoruz.

👉 !  @class ile class’ın bir isim olduğunu, keyword olmadığını belirttik.

İlgili oluşturduğum custom TextBox’ı kullanmak istersem,
.cshtml dosyasında ilgili extension fonksiyonunun bulunduğu namespace’i using etmem gerek. 

![21-7](https://github.com/user-attachments/assets/9e05a097-5684-4905-8509-4cebe1acbe9f)

Özetle, Bir şeyin custom halini oluşturmak istiyorsan, extension fonksiyonlarını kullanabilirsin. Bir yapının customize edilmiş halini extension ile çok rahat yapabilirsin.


👋 22 - TagHelpers


TagHelper'lar, HTML Helper'ların yerine gelen yeni yapılanmalardır. Peki, bunlar nedir?
TagHelper'lar, daha okunabilir, anlaşılabilir ve kolay geliştirilebilir bir view inşa etmemizi sağlayan, ASP.NET Core ile birlikte HTML Helper'ların yerine gelen bir yapılanmadır.



✨ TagHelpers vs HTML Helpers ✨

![22-1](https://github.com/user-attachments/assets/8eb6c423-fd06-4d00-8d70-38e54dd23091)

![22-4](https://github.com/user-attachments/assets/b52e3500-3b6d-4ef1-9fc5-38600e75c34a)

✨ TagHelper Entegrasyonu ✨


TagHelper'ı kullanabilmek için öncelikle view'lere belirli bir kütüphaneyi entegre etmemiz gerekecek.
Bir view üzerinde TagHelper kullanacaksam, ilgili kütüphaneyi view'e entegre etmeliyim.

👉 ! @addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers

👉 ! TagHelper'lar özünde bir sınıf olduklarından, belirli bir kütüphaneyi içinde barındırılmalıdır.

👋 HTML Nesnelerinde TagHelper Kullanımı 

✨ Form TagHelper ✨

![22-2](https://github.com/user-attachments/assets/4edb9d51-b49f-46ca-8033-55f0a74d2888)

![22-4](https://github.com/user-attachments/assets/e08dc8bb-a614-4665-8496-fae3eca2c989)

👉 ! TagHelper'ın aktif olup olmadığını kontrol etmek için, bir HTML nesnesi üzerine gelip asp yazdığınızda, eğer ki @asp çıkıyorsa, kütüphane doğru yazılmış ve TagHelper kullanılıyor demektir. 

![22-3](https://github.com/user-attachments/assets/75baf373-9af7-4590-828a-929d64a3a0e8)

✨ Input TagHelper ✨

Input nesnelerinde kullanabildiğimiz, bu nesneler üzerinde belirli model binding işlemlerinde vs. kullandığımız TagHelper'lardır.

![22-5](https://github.com/user-attachments/assets/5fb0dee3-7143-46af-b2e0-60933e044ce2)


✨ Cache TagHelper ✨

![22-6](https://github.com/user-attachments/assets/4ec48d3b-e67b-4083-b9a0-81084312fd87)

![22-7](https://github.com/user-attachments/assets/ac9ba10a-3549-41df-859f-eb7f5b4eb576)

InMemory'de cache'lenir.
Sayfayı her yenilediğimizde, cache tag'li olan kısım cache'den gelir ve yenilenmez.
Ancak diğer kullanımda dikkat edilirse, saliseli kısım değişiyor.

✨ Environment TagHelper ✨

![22-8](https://github.com/user-attachments/assets/7d2913f3-831b-4d06-a3d1-6a3213738e4e)


✨ Image TagHelper ve ETag Kullanımı ✨


Image TagHelper, ETag yöntemini otomatik olarak kullanmamızı sağlar.

ETag (Entity Tag), bir jeton (token) oluşturarak statik dosyalarda değişiklik olup olmadığını belirler.

✔ Eğer bir statik dosyada değişiklik yoksa, istemciye yeniden indirme yapmadan mevcut önbellekteki sürümü kullanmasını söyler.

✔ Bu sayede gereksiz veri transferi önlenir ve performans artırılır.

🔹 Yani, ETag sayesinde statik dosyalarda değişiklik olmadıkça istemciye aynı dosya tekrar gönderilmez.

🔹 Eğer kaynakta bulunan statik dosya değişirse, ETag değeri de değişir.

🔹 Bu durumda, istemcinin önbelleğinde bulunan eski dosya artık geçerli olmaz.

🔹 Sunucu, yeni dosyanın güncellenmiş halini istemciye gönderir.


✅ Bu sayede, önbelleğe alınmış eski içerik yerine en güncel versiyon otomatik olarak kullanılır.

Özet:

📌 Cache'deki dosya, kaynakta değiştiyse, önbellekteki eski sürüm silinir ve size gerçek (güncellenmiş) dosya teslim edilir.

👉 ! ASP.NET Core'da Tag Helper kullanırsan, Image Tag Helper otomatik olarak ETag yönetimini yapar. Ancak, HTML Helper kullanıyorsan, dosyanın değişip değişmediğini manuel olarak kontrol edip, gerekirse yeni sürümünü yüklemen gerekir.


✨  Partial TagHelper  ✨

![22-9](https://github.com/user-attachments/assets/f76d2b9d-01a6-4952-82da-95a51f7ea57c)

👉 ! TagHelper'ları Eklediğimiz View'lerden Tekrar Kaldırabiliriz

![22-10](https://github.com/user-attachments/assets/0de0bf0b-e0f1-467a-a470-2c4cbcf858e1)

![22-11](https://github.com/user-attachments/assets/98269001-bf1b-491b-bd92-1cf22fed4eaa)


📌 İleride göreceğimiz ViewImport.cshtml adında bir dosyamız olacak ve bu dosyada tanımladığımız using direktifleri veya belirli kütüphaneler tüm view'lar tarafından erişilebilir olacak. Dolayısıyla, TagHelper'ı da burada tanımlayacağız. Bu sayede, tek tek gidip tüm view'larda tanımlamak zorunda kalmayacağız. Ancak, bazı view'lerde TagHelper kullanmak istemeyebiliriz. Bunun için ilgili view'de @remove TagHelper kullanarak, yalnızca o sayfa için TagHelper'ı pasifleştirebiliriz.










