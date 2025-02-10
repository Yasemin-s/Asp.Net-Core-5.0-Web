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
