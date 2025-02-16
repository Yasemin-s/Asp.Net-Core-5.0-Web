👋 35 - Layout Yapılanması Nedir? RenderBody ve RenderSection Fonksiyonları Nelerdir?



Layout kullanılmadığında ne gibi olumsuz durumlarla karşılaşıyoruz? Öncelikle bunu ele alacağız. Böylece layout’a neden ihtiyaç duyduğumuzu daha iyi anlamış olacağız. Örneğimizde 3 sayfa üzerinden açıklama yapacağız. HomeController içinde Index, Sayfa1 ve Sayfa2 adında action metotlarımız var ve bu metotlara karşılık gelen view dosyalarını uygun şekilde doldurduk.

![35-1](https://github.com/user-attachments/assets/35f38cf3-ae72-482a-9937-1900835e2ce3)

Burada üst menü hep sabit kalmalı. Üst menüdeki alanlara tıkladığımızda, çıktı olarak "Burası sayfadır." yazan alt kısım değişmeli. Yani, Index.cshtml’in çıktısı "Burası sayfadır." kısmı olacak. Bunu en temel yöntemle yapmak istersek, Index.cshtml kodlarını kopyalayıp Sayfa1.cshtml ve Sayfa2.cshtml içine yapıştırarak gerçekleştirebiliriz. Ancak bu durumda: Ekranda sabit olan (üst bar) kısımlar için her sayfada kopyala-yapıştır yapmış oluruz. Olası bir durumda üst barda herhangi bir değişiklik yapmak istersek, tüm sayfalarda aynı değişikliği yapmak zorunda kalırız. Bu da yönetimi zorlaştırır. Daha doğru bir yaklaşım olarak, her sayfada tekrar eden yapılanmaları ortak bir dosyaya koyup, sayfadan sayfaya değişiklik gösteren içerikleri yalnızca ilgili view içinde oluşturabiliriz. Tekrar eden yapıları ise, ilgili view render edilirken ortak dosyadan alırız. Sonuç aynı olur, ancak süreç daha işlevsel ve yönetilebilir hale gelir. İşte burada, tekrarlamayan alanları tutan ortak yapıya "Layout" denir.

👉 ! Layout Nedir?



Bütün UI teknolojilerinde olmazsa olmazımızdır Layout. Sayfadan sayfaya gezinirken, kullanıcıya tutarlı bir deneyim sağlayan ortak sayfa taslağı oluşturur. Tutarlı bir düzene sahip web sitesi oluşturmak için Layout kullanılır. Sayfadan sayfaya değişiklik göstermeyen alanları Layout ile tanımlıyoruz.

Bir web sitesinde genel olarak taslak şu şekildedir. 

![35-2](https://github.com/user-attachments/assets/6853a6dd-a00b-432f-8c93-af2555071a62)

Header, Left Navigation ve Footer kısmı sabit kalacak, Content kısmını View’de göster dememizi sağlayacak yapılanmadır Layout. Peki, bunu nasıl yapmamızı sağlıyor? RenderBody() metodu ile.


✨ Layout Yapılanması ✨ 



Projemde sabit olacak kısımları Layout dosyasına/sınıfına yazmalıyım. Ayrıca Layout dosyası özünde bir View (cshtml) dosyasıdır. Bu dosya View içinde herhangi bir yerde oluşturulabilir. Ama biz genellikle Layout dosyasını Views klasörü altında Shared klasörü içinde _Layout.cshtml adında oluşturuyoruz. Layout içine her sayfada değişkenlik gösterecek alanlarda değişiklik yapacağız. Bizim örneğimize göre "Burası sayfadır." çıktısıydı değişkenlik gösteren yer. Değişiklik gösterilecekten kastımız, ilgili View’ın çıktısının buraya basılacak olmasıdır. Peki, View’den View’e değişkenlik gösteren veriyi biz buraya nasıl basacağız?@RenderBody() ile. 

![35-3](https://github.com/user-attachments/assets/6eb59b10-a00f-4720-ba73-8d631e5596d3)

Bu şekilde sabit   Layout’a tanımladığımız için, değişiklik gösterecek kısımları sadece ilgili View’lerde kodluyoruz. Ancak diğer View’lerin Layout’u görmesi ve kullanması için yapmam gereken Layout kısmını eklemektir. 

![35-4](https://github.com/user-attachments/assets/ecc1a947-4560-4a8d-b5c4-314c4eba8301)

Bunun için Layout’u kullanacak View’lerde tanımlama yapıyorum.

👉 ! Bir View’ın farklı bir Layout dosyasını benimseyebilmesi için yapmam gereken işlem, Layout property’sini çağırıp Layout olacak View’ın path’ini bildirmektir.




✨ @RenderBody() ✨ 



@RenderBody(), Layout üzerinde o anki render edilen View’in sonucunun nereye basılacağını ifade eden fonksiyondur. 

![35-5](https://github.com/user-attachments/assets/64a3889d-2e34-4b16-ae13-38840b5137c8)

Layout ile tekrar etmeyen yapıları tek bir dosya üzerinden yönetebilmiş oluyorum.

RenderBody, render edilen View’lerin Layout’ta nereye basılacağını temsil eder. Layout’ta tanımlanması zorunludur ve 1 tane olmalıdır.

✨ RenderSection ✨ 

RenderSection, Layout içinde isimsel bölümler oluşturabilmemizi sağlayan metottur. İhtiyaç doğrultusunda bu bölümlere, render edilen View’lerden de içerikler alınabilir. Layout içinde ekstra ana RenderBody’nin dışında farklı parçalar oluşturmak istiyorsanız RenderSection’u kullanabilirsiniz.

Layout dosyasında RenderSection kullandık diyelim. Layout’u kullanan farklı View’ler render edilirken uygulama patlar. Çünkü, RenderSection ilgili View tarafından değer almalıdır. Aksi takdirde hata verecektir.

![35-6](https://github.com/user-attachments/assets/3fa03a85-7890-42c0-9f9f-c92912cbce52)

Eğer ki sen Layout’ta bulunan RenderSection’un zorla kullanılmasını istemiyorsan, View’den View’e göre opsiyonellik gösterecekse RenderSection’un 2. parametresine required: false demen yeterlidir. 

![35-7](https://github.com/user-attachments/assets/e16d6d8b-50de-4b36-8663-e18104998655)

Bunun anlamı, ilgili View tarafından Layout’taki bu Section kullanılmıyor demiş olduk. Eğer true olsaydı (veya default olarak zaten true’dur), bu durumda ilgili View’de RenderSection’u kullanmak zorundasın.

İlgili View’de Layout’taki Section’a bir değer göndermek istesem, yani RenderSection’u kullanmak istesem, ilgili View’de Section’u tanımlamam gerek. @section solmenu { } şeklinde tanımlama yapıyorum. Bu şu anlama geliyor: Layout’ta solmenu isminde tanımlanmış RenderSection alanına, View render edilirken istediğin değerleri gönderebilirsin. 

![35-8](https://github.com/user-attachments/assets/4bfa1be4-8266-4916-bd55-85cde4a78ac5)

![35-9](https://github.com/user-attachments/assets/5bf68873-174f-45f4-b97d-260de488e91e)

![35-10](https://github.com/user-attachments/assets/13450268-7520-4c04-994c-ca12fd68498b)

RenderSection, View’de ekstra alan tanımlamanı sağlar. Ana RenderBody’nin dışında, View’de müdahale edebileceğin sayfadaki noktaları da RenderSection’da tanımlama yapabilirsin.

RenderSection genellikle: JS referansları Sayfadan sayfaya fark eden alanlar için kullanılır. Örneğin, AView ve BView olsun. BView’ında sen JavaScript kullanıyorsan, render ederken JS referanslarına ihtiyacın var. Bunu BView’ında ilgili Layout’a ekletmek istiyorsan Section’u kullanabilirsin. 

![35-11](https://github.com/user-attachments/assets/156c2947-ef8c-49b1-9b40-f39d949d855c)

👋 36 - _ViewStart ve _ViewImports Dosyaları Nedir?


✨ _ViewStart Dosyası ✨ 

_ViewStart dosyasının asıl amacı, tüm view’lerde kullanılması gereken ortak işlemlerin yapılmasını sağlamaktır. _ViewStart da aslında bir .cshtml dosyasıdır. View ile ilgili çalışma yaptığımız tüm operatif view’ler özünde bir .cshtml dosyasıdır, örneğin layout’ta olduğu gibi.

_ViewStart bir nevi tüm view’lerin atasıdır. Herhangi bir view’i sunucuda render ediyorsanız, eğer varsa önce _ViewStart dosyası render edilir, ardından ilgili view’iniz render edilir. Views klasörü altında _ViewStart.cshtml olarak oluşturulması gerekir, aksi takdirde herhangi bir view’in başlangıç view’i olup olmadığını belirleyemeyiz.


✨ _ViewStart ne amaçla kullanılır? ✨



Genellikle tüm view’lerin ortak kullanacağı layout tanımlaması bu dosya içerisinde gerçekleştirilir.

Örneğin, biz üç farklı sayfada ayrı ayrı layout tanımlaması yapmıştık.

![36-1](https://github.com/user-attachments/assets/22898a95-e04e-4e51-a783-bfa696280748)

Dolayısıyla, her sayfa için ayrı ayrı layout tanımlamak yerine tek bir noktada tanımlamak istersek, bunu sağlayacak tek dosya _ViewStart dosyası olacaktır. Views klasörü içinde _ViewStart.cshtml adında bir view oluşturuyoruz. Bu dosya sistem tarafından başlangıç view’i olarak nitelendirilecektir.

Diğer tüm view’lerde kullandığımız layout yapılanmasını _ViewStart içinde tanımladığımızda, proje çalıştığında herhangi bir view çalışmadan önce _ViewStart çalışır. _ViewStart içinde layout tanımlandığı için, önce bu layout ekrana gelir ve daha sonra ilgili view’in çıktısı gösterilir.

Eğer herhangi bir view’de layout tanımlamasını ezmek (iptal etmek) istiyorsanız, yapmanız gereken işlem ilgili view’de Layout = null; yapmak veya kullanmak istediğiniz layout’un path’ini yazmaktır.

![36-2](https://github.com/user-attachments/assets/1929507c-17ee-443b-8054-44d0f0e4c086)


✨ _ViewImports Dosyası ✨ 

Razor sayfaları için kütüphane ve namespace tanımlamalarını her sayfa için ayrı ayrı yapmak yerine, ortak/merkezi bir noktada tanımlamamızı sağlayan bir dosyadır.

_ViewImports ve _ViewStart dosyaları aslında ortak tanımlama dosyalarıdır. Aralarındaki teknik fark şudur: _ViewImports.cshtml → Programatik tanımlamaları yapar (örneğin using blokları, namespace tanımlamaları, TagHelper tanımlamaları). _ViewStart.cshtml → Programatik işlemler dışında, layout gibi ortak kullanılan HTML tabanlı işlemleri yapar. _ViewImports içinde import işlemlerini gerçekleştiririz. Programatik import işlemleri burada sağlanır.

👉 ! Views klasörü altında _ViewImports.cshtml adıyla oluşturulur.


Örneğin, herhangi bir view’de bir türe/nesneye/sınıfa erişmem gerekiyorsa @model ya da @using olarak erişim sağlayabiliyorduk/bildirebiliyorduk.

![36-3](https://github.com/user-attachments/assets/14358c61-7122-4a68-99f5-782c35447229)

Bu şekilde, sınıflarımızı view bazlı kullanılabilir hale getiriyorduk. Peki, tüm view’lerde tek tek bu şekilde tanımlama mı yapacağız? Model katmanındaki entity’lere bütün view’lerden erişmek istiyorum. Bunun gibi genel tanımlamaları _ViewImports.cshtml dosyası altında gerçekleştiriyoruz. Views klasörü altına _ViewImports.cshtml adında bir dosya oluşturuyoruz. _ViewImports dosyası içinde yapılan tüm using tanımlamaları mimaride global bir şekilde erişilebilir olacaktır. Örneğin, _ViewImports.cshtml dosyasında: @using LayoutExample.Models
dediğimde, artık bu namespace altındaki sınıflara tüm view’lerden erişim sağlanabilecektir.

![36-4](https://github.com/user-attachments/assets/1d6819c3-6dc6-4086-8df0-f3483ec5000a)

![36-5](https://github.com/user-attachments/assets/e78e8b93-6451-4aa2-af02-911dce8c3893)

Belirli bir namespace altındaki sınıflara erişebilmem için tekrar tekrar namespace tanımlaması yapmama gerek kalmıyor. _ViewImports üzerinden yapılan bu çalışma neticesinde tüm view’lere gerekli using tanımlamaları tek çatı altında yapılmış oluyor.

_ViewImports dosyasında TagHelper tanımlamasını da yapabiliyoruz.

![36-6](https://github.com/user-attachments/assets/8a4ab702-094a-4d7a-a302-efa711825108)

Bu tanımlamalar sayesinde artık herhangi bir view’de ilgili TagHelper’lara erişim sağlayabilir duruma geliyoruz.

![36-7](https://github.com/user-attachments/assets/234689c7-704b-4868-bb6a-4975dfc5a501)

Dikkat edilirse, asp- dediğimizde otomatik olarak gelmektedir, yani erişim sağlamış oluyoruz. Herhangi bir view tabanlı TagHelper kütüphanesini tek tek tanımlamamıza gerek kalmadan, _ViewImports üzerinden tek çatı altında TagHelper tanımlamasını yaparak, direkt olarak view’lerde operasyonlarımızı gerçekleştirebiliyoruz.
