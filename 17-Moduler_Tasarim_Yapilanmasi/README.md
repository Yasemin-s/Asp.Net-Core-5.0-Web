👋 37 - Modüler Tasarım Açıklaması Nedir? Nasıl Uygulanır?



✨ Modüler Tasarım Nedir? ✨

Küçük parçaların bir araya gelerek bir bütün oluşturduğu yapılanmadır/tasarımdır.
Örneğin, bir araba düşünelim: Arabanın tekeri, kasası, farı gibi farklı parçaları vardır. Tekerinde sorun olduğunda pencereyi etkilemez. Sadece tekere, yani ilgili parçaya odaklanarak çözüm getirebiliriz. Modülerlik, parça-bütün-parça ilişkisidir. Tüm işlemleri tek bir sorumluluğu üstlenecek parçaların bir araya gelerek bütünü oluşturmasıdır.
Modüler tasarım yapılanması yalnızca MVC'ye özel değildir; bu bir mantıktır ve kullandığın mimariye göre uyarlaman gerekir.

✨ Web Uygulamasında Modüler Tasarım Yapılanması Nasıl Kullanılır? ✨

MVC mimarisinde bunun için iki yapılanma vardır: Partial View , View Component. Bir web sayfasında üst menü, sol menü, alt kısım (footer) ve içerik bölümü olduğunu düşünelim. Bunların hepsini tek bir sayfadan yönetmek ideal bir tasarım değildir. Bunları parçalaman gerekir; yani her birini farklı .cshtml dosyaları olarak kullanmalısın. Bu ayrı parçaları kullanmak istediğin yerlerde referans etmen yeterlidir. Modüler tasarım yapılanması sayesinde sayfa değişikliklerini de hızlı bir şekilde yapabilirsin. Eğer modüler olarak .cshtml dosyalarını referans ediyorsan ve örneğin alt menüyü üst kısma taşımak istiyorsan, bunu hızlı bir şekilde yapabilirsin.
Tüm kodları kopyala-yapıştır yapmak yerine, referans vererek işlem yaparsın. Böylece sayfa tasarımına hızlı bir şekilde müdahale edebilme şansı yakalamış olursun.


✨ Partial View Nedir? ✨

Modüler tasarım yapılanmasında her bir modülü ayrı bir View olarak tasarlamamızı sağlayan ve bunları parça View olarak ana View'de birleştirmemizi mümkün kılan bir tekniktir.
Modüler tasarımda her bir modülün ayrı bir .cshtml dosyası olarak tasarlanmasını ve ihtiyaç doğrultusunda ilgili parçanın çağrılıp kullanılmasını sağlayan yöntemdir.
Herhangi bir View dosyasını parça olarak kullanmanı sağlar.

👉 ! View Component ile Partial View Arasında Davranış Farkı Vardır.


✨ Partial View Yapılanması Nasıl Oluşturuluyor? ✨

Modüler tasarım yapacağın View üzerinde hangi bölümleri parçalayacağını belirlemelisin (üst menü, alt menü vs.). Partial View, ayrı bir View dosyasıdır. Bunları bir dizinde tutup çağırmamız yeterli olacaktır. Hangi Controller'a ait Partial View oluşturacaksan: Views klasörü altında Home'a ait olan View klasöründe "Partials" adında bir klasör oluşturmalısın.
_HeaderPartial.cshtml adında bir View oluşturmalısın. Burası bizim üst menümüz olacak ve içeriğini UI'a uygun şekilde dolduracağız. _Layout.cshtml dosyasında oluşturduğumuz _HeaderPartial'ı çağırmak istersek 3 farklı şekilde yapabiliriz:

@Html.Partial()

@Html.RenderPartial()

<partial> TagHelper kullanımı

✨ Partial View Kullanımı ✨


👉 ! Partial Fonksiyon ile : @Html.Partial("~/Views/Home/Partials/_HeaderPartial.cshtml")

👉 ! RenderPartial Fonksiyon ile : @Html.RenderPartial("~/Views/Home/Partials/_HeaderPartial.cshtml")

👉 ! TagHelper ile : Eğer ViewImports içinde TagHelper tanımlıysa, <partial name="~/Views/Home/Partials/_HeaderPartial.cshtml" />

✨  Partial Yapılanmasının Avantajları ✨

Yönetilebilirliği artırır.
Sayfa değişikliklerini hızlı yapma imkânı sunar.
Kod tekrarını önler.
UI değişikliklerini merkezi bir yerden kontrol edebilme imkânı sağlar.


✨  Partial View Veri Gönderme Kritiği ✨

Tasarlanan modüler yapılara nasıl veri gönderebiliriz?
View'lere ayırdığımız modüllere nasıl değer gönderebiliriz?
Controller'da üretilen veriler ilgili modüllere nasıl taşınabilir?

Controller'da oluşan veriyi önce View'e taşımamız gerekir.
Veri gönderildiğinde ilk olarak hangi View render ediliyorsa ona taşınır.
View'in render edilmesi sırasında Layout da bir yandan render edildiği için, fark etmeksizin Partial View'lere otomatik olarak veri taşınacaktır.

25..dk 
