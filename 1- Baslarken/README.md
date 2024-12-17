👋 1 - Asp.Net Core 5.0 Eğitimi

 - Kullanılan mimarinin ne olduğunu bilerek başlamak gerek, asp.net ve asp.net core nedir
 - Web mantığını anlamak
 - Webi programlayacağınız için o programlayacağın web mantığını bilmek gerekir.
 - Web mantığında belirli terimleri öğreneceğiz. User, client vs.
 - Http protokolü nedir? Neye hizmet eder? Webde kullanılan ve bu protokol sayesinde web ile iletişime geçiyoruz.
 - Web mimarilerinin yapılanmaları olan web stratejileri nasıl çalışır ?
 - Web geliştirme modellerinden mvc inceleyeceğiz.
 - Mvc, bir design patterndır.
 - Mvc'ye gelen bir design patterndır.
 - Html helper, tag helper, url helper olan yardımcı yapılanmlardan bahsedeceğiz.
 - Model binding dediğimiz kullanıcıdan veri alma ve veri gönderme işlemleri için kullanılan yöntemden bahsedeceğiz.
 - Layout nedir, nasıl kurulur ?
 - Modüler tasarım yapılanmları
 - Route yapılanmaları
 - Asp.Net Core özellikleri - Dependency Injection
 - Areas

👋 2 - Asp.Net Core Nedir ?

Amacımız web uygulaması/webde çalışan uygulama geliştirmektir. Biz nasıl console uygulamasında çalışacaksak gidip console application oluşturuyoruz yada bir görsel arayüzü olan form üzerinde işlemlerimizi yapacaksak windows form application oluşturuyoruz aynı şekilde web uygulamaları geliştireceksek webin fıtratına uygun bir teknolojide çalışmak gerekir. Bu teknolojiler javanın kendine ait web teknolojisi olabilir. Php dediğimiz programlama dili olabilir. Yahut microsoft tarafından geliştirilmiş asp.net teknolojisi/mimarisi olabilir. 

👉 ! ASP.NET, bir teknolojidir, daha spesifik olarak bir web uygulama çerçevesidir (web application framework). Mimari değil, bir teknolojidir. 

👋 3 - Asp.Net Nedir ? 

Microsoft tarafından geliştirilen bir web uygulama geliştirme mimarisidir. Mimari, programlama dili demek değildir. Php programlama dili ise asp.net nedir ? Asp.net bir programlama dili değil, programlama dili olan C# ile kodlanabilen web uygulaması geliştirme mimarisidir. Mimari dediğimiz belirli bir yaklaşımı kabul etmiş/benimsemiş bir programlama dili ile desteklenen ve belirli bir amaca hizmet eden yapılanmadır. Asp.net ile bir form uygulaması yada salt bir işlem (mesela vt işlemi) yapamazsın yada bir algoritma oluşturamazsın. Asp.net bir mimari/teknolojidir,  C# ile bu mimariler üzerinde kodlamalar yapıp profesyonel/kurumsal web uygulamaları geliştirebiliriz. 

👋 4 -  Asp.Net Core Nedir ? 

Asp.net ve asp.net core farkını bilebilmek için .net ile .net core arasındaki farkı bilmek gereklidir. Microsoft tarafından geliştirilen ücretsiz ve open source olan web geliştirme mimarisidir. Asp.net core open sourcedur ve web geliştirme mimarisidir. Asp.net'in üzerine gelen bir mimaridir. Asp.net windowsta çalışırken asp.net core windows, linux gibi diğer platformda çalışabilir. Tüm asp.net altyapısı yeniden tasarlanarak oluşturulmuş bir mimaridir. 

👋 5 - Asp.Net Core'un Asp.Net'ten Farkları 

 - Asp.net core daha performanslıdır, cross platformdur.
 - Asp.net'de yapısal olarak her şeyin bir bütün olarak kullanılması gerekirken asp.net core bütünlükten ziyade modüler yapılanmaya geçilmiştir.
 - Modüler yapılanma, örneğin arabanın tekeri, farı vs. hepsi ibr bütün olurssa yani modüler değilse arabanın hepsi bir bütünse, arabada oluşabilecek ufacık bir hata arıza arabanın topyekün bütününü ilgilendirir. Halbuki tekerleğin modüler olması akünün modüler olması sadece bu alanlarla ilişkili lcoal problemlerde o alanda çalışıp genelde problemi çözmemizi sağlamaktadır.
 - Yani modüler yapılanma parça bütün ilişkisidir. Siz sistemde kullanacağınız ufacık bir modülü sisteme/devreye sokabilir yada devreden çıkarabilirsiniz. Bu durum sistemin genelini etkilemez.
 - Bir şeyin modüler olmaması her şeyin kendi bünyesinde olmasıdır. Dolayısıyla bu da yönetilebilir/geliştirilebilir vediğer durumları/ölçütleri ciddi manada maliyetli hale getirir.
 - Dependency injection, IoC dediğimiz yapılanmalar vardır. Asp.net'de bunları harici kütüphaneler olarak kullanıyorduk. Asp.ent core da mimari IoC mekanizmasını kendi dahilinde barındırıyor. Dependency injection tasarımını otomatik olarak oluşturmamızı sağlıyor. Asenkron işlemler olsun, kolay bakım osun, razoe pages teknolojisi olsun. Bunun gibi extradan katkılarda bulunan bir mimaridir asp.net core.

👉 ! Asp.net core 5.0 neleer getirdi ? Open api, performans yapıları, belirli sorguların geliştirilmiş hali vs. 




