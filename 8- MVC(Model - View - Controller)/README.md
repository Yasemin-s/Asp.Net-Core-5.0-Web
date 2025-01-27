👋 1 - MVC Nedir ? Asp.Net Core MVC Pipeline Nasıldır ?

Asp.net core da kullanacğaımız mvc yaklaşımını inceleyeceğiz. Mvc nedir ? 
Mvc, birbirinden bağımsız 3 katmanı esas alan bir mimarisel desen (architectural pattern)' dır. Bazı kaynaklarda tasarım deseni olarak da geçmektedir. Ama tasarımdan daha büyüktür daha derindir yani mimarisel desendir. 

Peki mimarisel desen ve tasarımsal desen arasındaki fark nedir ? 
İleride incelenecektir. Mimarisel desen dediğimiz, design patternlardan daa geniş kapsamlıdır. İçinde bir yada daha fazla design pattern kullanabilirsin ve belirli bir mimarinin oturduğu desenlerdir. Daha geniş kapsamlıdır. 
Design pattern dediğimiz tasarım desenleri belirli senaryolara uygun yerleştirilirken mimarisel desneler ise genel yaklaşımımızı belirler. MVC de olduğu gibi, biz bu yaklaşım üzerinden web geliştireceğiz. Mimariyi bunun üzerine pturtuyoruz/bunu benimsiyoruz. Bu bir mimarisel desendir.  

Ama sen gidite bağımsızlık üstüne çalışma yapacaksan, dependency injection desegn patternı uygularsın. Bu bir mimari değil sen bunun üzerine eb geliştiremezsin. Bu, o senaryo ihtiyacında onu uygulamaktır. Yada başka örnek olarak belirli stratejilerde çalışman gerekir. Starteji design patterni vardır vs... ama mimarisel desen dediğimiz bunlardan daha geniş kapsamlıdır. İçinde bir veya daha fazla tasarım barındırabilirler. MVC özünde observer, decorator gibi design patternları kullanan bir mimarisel desendir. 

👉  MVC ye tasarım deseni dememizde bir sakınca yoktur.

Microsoft, MVC deseni üzerinde oturtulmuş asp.net core mvc mimarisini geliştirmiştir. Mimarisel desen olduğu için, asp.neti' de bu mimarisel desen mantığında çalışılabilir hale getirmiş ve bunu da bize sunmuştur. 


✨  MVC Nedir ?  ✨

![13-1](https://github.com/user-attachments/assets/9e1ec1fe-8f05-40b4-97b6-fa5cdbb5ab8b)

Mvc, temelde bir kodun yapısal olarak işleme sürecinde bunun sunulmasını, değer üretme sürecini yada yönetilme sürecini birbirinden soyutlamamızı sağlar. Mvc, illa webde uygulanan bir tasarım deseni değildir. Bir programda/platformda/programlama dilinde de kullanabilirsin. MVC'yi iki şekilde açıklayacağız. Normalde nedir ve webde nasıldır/nedir şeklinde. 

Model, webde de diğer platformlarda da kullansan işlenecek olan veriyi temsil ediyor. Genellikle veritabanı işlemlerinin yapıldığı katmandır. Genelde, webde, bu katman için entity framework core ile çalışabiliyoruz. 

👉  Entity framework core amacı veridir. Entity modeller verinin ta kendisidir/veriyi modellediğimiz sınıflarımızdır.

Ado.Net çalışmaları da model katmanında olur. Repository design pattern katmanı kullanıyorsan modelde tutarsın. 

👉  Kısaca veritabanı işlemleri models katmanında tutulur.

👉  View, normalde elde edilen detayı görselleştirecek/anlamlı hale getirecek katmandır. Sunum katmanıdır. Web için html,css vs view da tutulur.

👉  Controller, gelen requestleri karşılayacak olan ve requestin içeriğine göre gerekli model işlemlerini üstlenir. Algoritmaları, servis, vt vs. çağırarak/çalıştırarak/sorgulayarak istenilen veriyiy üretmekten ve ihtiyaç dahilinde üretilen bu veriyi view ile görselleştirmekten sorumludur. 

✨  Webde MVC Anlatmaya Çalışalım ✨

![13-2](https://github.com/user-attachments/assets/0a00e3c3-f013-4d0d-9005-633f48297092)

Controllera duruma göre modelden veri gelir. Gelen veri yine duruma göre viewa gider ve viewdan veri döner. Controllera viewdan gelen veri clienta döner.
Mvc, de modelden viewa hiçbir zaman gitmez. Modelden, controllera controllerdan viewa gider.
Veritabanına ihtiyacın yoksa, modela gitmezsin, direkt viewa gidebilirsin. Viewa da ihtiyacın yoksa viewada gitmezsin. İlla bir yere gitmen gerekmiyor. Sonuç en son clienta gider.
View, controllerdan gelen veriyi alıyor/şekillendiriyor vs. ve sana geri dönüyor. İşte bu işelem "render" diyeceğiz. View, ilgili dataları render ediyor. Burda razor teknolojisi vs. kullanılıyor. Render edilen sonuçtan, view result dediğimiz bir sonuç üretiliyor. Üretilen bu sonuç sana gelen view resultta, viewın sonucu, sunumunun sonucu oluyor. 


✨ Asp.Net Core da Sürecin/Bir Requestin İşleme Sürecinin Nasıl Olduğunu Daha Detaylı İnceleeylim ? Asp.Net Core MVC Pipeline ✨

![13-3](https://github.com/user-attachments/assets/d186bd8a-d366-4d45-8008-4c41e442dfe4)

Bir request geldi ve bizim mimarimiz/ugulamamız bu rquesti nasıl karşılıyor ? Buradaki MVC mekanizması nerelerde devreye giriyor. 
Şimdi, MVC ile çalıştığımız için kestrel sunucumuz bu requesti karşılıyor. Önce middleware dediğimiz yapılar devreye girer. Sen ara yazılımları custom şekilde tanımlayıp önceden devreye soktuysan bunlar işlenecektir. Geçtikten sonra routing dediğimiz bir modül var/middleware var. (Şemadakilerin hepsi bir middlewaredır.) Routingde gerekli route işlemleri gerekli endpointler ayıklanacaktır. Hangi alana istek yapıldığına, routingde karar verilir. Rotayı burada belirliyor.

Controller initializer, ilgili controllerı ayağa kaldırıyor. Controller isteği karşıladı. Controller bizim için bir sınıftır. 

Action method execution, controller içinde action metotlar vardır. Controllerın içindeki metotlardır action metotlar. 

Result execution, action metottan gelen ilgili veri result olarak ya direkt clienta gidecek yada viewe gönderilecek.

Viewden render ile geri result dönecek ve clienta gidecektir. Yada isteği alıp başarılı bir şekilde sonlandırılsın bir yere bir şey gönderilmesin. 
