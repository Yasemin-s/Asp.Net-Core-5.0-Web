👋 24 - Model Binding Mekanizması



Model binding, HTTP request ile gelen verilerin ayrıştırılarak, ilgili controller'daki bulunan action metotlarında uygun herhangi bir türe dönüştürülme işlemidir.

Biz sunucuya, kullanıcıların yapmış olduğu isteklerde bazen kullanıcıdan gelen verileri de göndereceğiz.
Bu verileri biz POST neticesinde alıyoruz. Gelen verileri anlamlı ve bu verilere karşılık gelen türlerle yakalamak istiyorsanız, gelecek olan verilerin senin projende/uygulamanda bir sınıf ya da bir struct ile bind edilmesi gerekiyor.

Bir form olduğunu düşünelim. Butona tıkladığında formdaki verilerin hepsi hedef action'a / endpoint'e POST edilecektir.
İşte bu POST neticesinde, veriler controller tarafında karşılanır.

✨ Controller'da karşılama durumu ✨ 

Direkt olarak gelen veri salt halde karşılanabilir. Ya da gelecek olan verilere karşılık bir sınıf/model tasarlayabilirim. Tasarladığım bu model ile gelecek olan verileri bind edeceğim. Bu bind sonucunda, hangi veri hangi property'e gidecek, bunu bildiğimden dolayı formdan/kullanıcıdan gelen dataları daha anlamlı sınıflarla ve bu sınıfların instance'larıyla karşılayıp yönetebileceğim.

İşte Model Binding bunu yapmamızı sağlıyor.

Bize gönderilecek verilere karşılık olarak tüm property'leri bir sınıf oluşturarak tanımlıyoruz. Binding mekanizması içinde şunu yapıyoruz: Formdaki isimlerle sınıftaki aynı isimdeki property'leri bind ediyoruz.

![24-1](https://github.com/user-attachments/assets/73c5e9db-c245-4d6e-b266-b4b1866310dd)

Kullanıcı datayı gönderdiği zaman, bizim controller'da gelecek olan veriyi eğer Personel türünde/Personel nesnesiyle karşılamaya açıksam, bu karşılama neticesinde verimiz otomatik olarak Personel türüne dönüştürülecek.
İşte bu dönüştürülmeye biz binding diyoruz.

👉 ! ASP.NET Core MVC mimarisi binding işlemini kendisi yapıyor. Bizim ekstra bir şey yapmamıza gerek yok.

Kullanıcının form üzerinden girmiş olduğu dataları, biz controller'larla kendimize ait türlerde yakalamak istediğimizde, burada Model Binding kullanıyoruz.
Gönderilen data, bizim tanımladığımız ve bind ettiğimiz modele dönüştürülüp, ilgili sınıfın instance'ı üzerinden gelen dataları yönetmemizi sağlamaktadır.

✨ Model Binding'i nasıl yapıyoruz, bunu göstereceğim ✨ 



Product ekleme işlemi yaparak örneklendireceğim. Controller'a CreateProduct adında bir action oluşturuyorum. Bu action metot, normalde CreateProduct sayfasının açılmasını sağlar, yani GET isteğini karşılar. Açılan sayfa üzerinden yapılacak POST işlemi neticesinde, gönderilen dataları farklı bir action fonksiyonunda yakalayacağız.

👉 ! Bir action metot varsayılan olarak HTTP GET türündedir. Dolayısıyla formdan gelecek olan veriyi CreateProduct'ta yakalayamam, çünkü GET türündedir.

CreateProduct view'ını oluşturduk ve içine bir form tasarladık.
Form için POST işlemi yapacağız. Nereye POST edeceğimi TagHelper ile bildiriyorum.
asp-action ile belirttiğim action'a POST isteği gönder dedim. Dikkat edilirse burada controller adı vermedik. Bu durumda default olarak, yani controller adı verilmezse, view’ın bulunduğu controller baz alınır. 

![24-2](https://github.com/user-attachments/assets/5f9110b8-13b3-4d44-b152-db045e426f23)

Eğer ki özellikle belirtmek istersem, asp-controller ile controller adını bildirebilirim. Formu tetikleyebilmek için içinde herhangi bir yerde button veya submit nesnesi olması gerekiyor.
Controller'daki GET fonksiyonu, formun gösterilmesini sağlayan bir action'dır. View’da gönderilen POST isteğinin/datanın yakalanabilmesi için, Product altında CreateProduct isimli POST türünden bir fonksiyon oluşturmam gerekir. POST olduğunu ifade etmek için [HttpPost] attribute ile ilgili action’ı işaretliyorum. Böylelikle POST ile gelen request’lerin tetikleneceği bir metot tanımlamış oluyorum.

👉 ! Türe uygun olmayan metotlar kesinlikle tetiklenemez.

👉 ! Web mimarilerinde bir form POST olarak tetikleniyorsa, işlendiği endpoint’e içindeki input’ların değerlerini hedef endpoint’e POST olarak gönderir.

Peki, POST olarak gönderilen verileri hedef action’da nasıl yakalayacağız?

Request’ler neticesinde action’lara gelen veriler, metodun parametresinde yakalanır.
Formda her input’a name değeri giriyoruz ve controller’daki action’ın parametresine, formdaki name değeri ile birebir aynı parametreyi veriyoruz. 

![24-3](https://github.com/user-attachments/assets/66ce0f0a-c4c7-4f8f-bcdc-e51854e41b3e)

![24-4](https://github.com/user-attachments/assets/60f6ef7f-8858-4d44-9f9a-e9be6d7aa5f2)

Bazen formdan çok fazla veri gelebilir. Her bir input’a karşılık tek tek parametre tanımlayarak action metotta tutmak zahmetlidir ve yönetimi zorlaştırır. Gelecek olan fazla verileri karşılamak ve yönetmek için daha efektif bir sürece ihtiyacımız var.
İşte tam da burada Model Binding kullanabiliriz. Formdaki input’lardan action’a gidecek olan verileri bir model olarak/tür olarak/nesne olarak elde etmek daha kolay olacaktır.
Kullanıcıdan gelen verilere karşılık, bu verileri modelleyen bir modele/entity’e/sınıfa ihtiyacımız var. Gelecek olan veri neyse, o verileri birebir karşılayacak olan Product adında bir model oluşturduk. 

![24-5](https://github.com/user-attachments/assets/3de1d8b2-8c51-4a6d-a222-bfde7d29c010)

![24-4](https://github.com/user-attachments/assets/3bd67fd1-01dd-48dc-b0c6-3f1c56f27eba)

Gelecek olan veri ne eksik ne fazla olacak şekilde birebir model/sınıf/entity olarak tanımlanır ve oluşturulur. Buna ileride ViewModel diyeceğiz.
Artık action metoduna, "Gelecek olan verileri Product türünden bir nesne ile karşıla" dedik. 

![24-7](https://github.com/user-attachments/assets/86323a29-2b9c-432b-85c9-c9bd1ec78a3e)

![24-8](https://github.com/user-attachments/assets/ccabea88-8ddf-4842-a6fc-0a1e5cacd4d9)

----

![24-9](https://github.com/user-attachments/assets/de680abb-5013-4a33-92ec-fa09fa916589)

👉 ! Input’taki name ile action’daki parametredeki sınıfın property’leri birebir aynıysa, sistem tarafından otomatik olarak bind edilirler.

Biz bind işlemini daha fiziksel hale de getirebiliriz. Formdaki input’lardaki name alanlarını kaldırıp, bu input’ları direkt Product sınıfından/modelinden/türünden bir nesne oluşturarak otomatik bind edebiliriz.

Peki, bunu nasıl yapacağız?
Bunun için sayfanın modelini (@model ile tür bildirmemiz gerek) kullanabiliriz.
Modeli bildirdikten sonra tag helper ile input’lara asp-for fonksiyonu/direktifi ekleyerek, sayfanın modelindeki (Product modeli) hangi property ile bind edileceğini belirtiyoruz. 

![24-10](https://github.com/user-attachments/assets/1c2eb05f-0c6a-40bd-b00f-c6430a20a63b)

👉 ! Hatta dikkat edilirse, asp-for kısmında Product’taki property’ler otomatik olarak gelmiştir.


✨ HTML Helper ile Bind İşlemi ✨ 


Eğer HTML Helper kullanarak bir textbox oluşturuyorsan ve bind edilmiş bir textbox olacaksa,
sonu "For" ile biten HTML Helper’ı kullanman gerekir. Sonu "For" ile biten helper’lar bind edilebilir fonksiyonlardır.

![24-11](https://github.com/user-attachments/assets/21543b56-ba18-48c4-886a-c4c713fc117d)

![24-12](https://github.com/user-attachments/assets/bea7c787-d1c7-4d1f-b691-6139e8c5c9bb)

Sayfanın modeli neyse, ona göre property’ler gelecektir.


✨ Önemli Noktalar ✨ 


Controller’dan Bind Edilmiş Bir Modele Instance Göndermeme Durumu
Bind işlemi iki yönlüdür. Bazen boş bir form üzerinden işlem yapmamız ya da formun boş gelmesini isteyebiliriz. Bu durumda Controller’daki GET action’dan View’i render ederken herhangi bir nesne göndermemize gerek yoktur. Eğer nesne göndermezsek, boş bir form gelecektir.


✨ Formun Gelme Süreci ✨ 


GET action’ı tetiklendiğinde, View oluşturulur ve boş bir form gösterilir.
Kullanıcı formu doldurur ve butona tıkladığında, bir nesne oluşturulur ve ilgili Controller action’ına o şekilde gider. Başlangıçta nesne yoktu. Kullanıcı formu doldurup POST ettiğinde, bir nesne oluşturulup gönderilir.



✨ Controller’dan GET Metodunda Nesne Gönderme Durumu ✨ 


Eğer Controller’daki GET metodunda bir nesne gönderirsek,
Gönderdiğimiz instance form’a bind edilecek ve üzerinde değişiklik yapıldığında, o instance üzerinden değişiklik yapılacak.

POST edildiğinde yeni bir nesne oluşturulmayacak.
Mevcut nesne üzerinde yapılan değişiklikler, Controller’daki ilgili action’a gidecek.


✨ Kısaca Özetlersek ✨ 


GET metodunda nesne göndermezsem: Boş form gelir. Kullanıcı formu doldurur, gönderdiğinde yeni bir nesne oluşturulup ilgili action’a gider.
GET metodunda nesne gönderirsem: Form, gönderilen nesne ile dolu gelir. Kullanıcı bilgileri güncelleyip gönderdiğinde, mevcut nesne üzerinde değişiklik yapılır ve değişmiş haliyle action’a gider.

✨ İki Taraflı Bind İşlemi✨ 


Bind işlemi iki taraflıdır.
Eğer nesne dolu şekilde giderse,
👉 Açılan formda veriler dolu gelir.
👉 Formda değişiklik yapılırsa, gelen nesne üzerindeki bilgiler güncellenir ve Controller’daki ilgili action’a o şekilde iletilir.
