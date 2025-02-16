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
