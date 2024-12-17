👋 1 - Olay Tabanlı Web Geliştirme Yaklaşımı

Biz bir web uygulaması geliştiriken geliştirme yaklaşımımıza göre mimariyi şekillendiririz. Yani sen, belirli yaklaşımlardan herhangi birini kabul ediyorsun o kabul ettiğin mimariyi ona göre/uygun kodluyorsun/şekillendiriyorsun/planlıyorsun.

Üç tane mimariden bahsedeceğiz. Mvc mimarisi, olay tabanlı web geliştirme mimarisi ve api mimarisi. Api için direkt birebir web uygulaması diyemeyiz ama burada geçebilecek bir yaklaşım olmasından dolayı değerlendiriyoruz. 


Olay tabanlı programlama yaklaşımı, aslında web yaklaşımı değil bir programlama yaklaşımdır. Bu yaklaşımı sen webe uyarladığında web üzerinde kullanıcının eylemlerine göre programı yönlendirdiğini düşün. 

Olay tabanlı yaklaşımda kişinin eylemleri ön plandadır. 
Olay tabanlı programalamaya, olay güdümlü progamlama veya olay yönlendirmeli programlama da denmektedir.
Programın akışını kullanıcı eylemlerine göre yönlendiren bir programlama yaklaşımıdır. 
Kullanıcı eylemlerine uygun bir şekilde olaylar tanımlanmıştır. Bu olaylar çalıştırılacak kodu barındırmaktadırlar. Uygulama hızlı bir şekilde inşa edilebilir. Fakat bakım ve sonraki gelişim süreci oldukça maliyetli olan bir yaklaşımdır. 
Asp.Net'in eski mimarisi olan web form mimarisi vardı, onun temeli olay tabanlı yaklaşımdı. Kodlar ve sunum aşaması iç içe olduğundan ciddi manada maliyete sebep oluyordu.

 ![9-1](https://github.com/user-attachments/assets/0f51745c-7a7d-4a03-9ec3-fcdec57a248e)

👋 2 - Model - View - Controller (MVC) Yaklaşımı

Mvc, model view ve controller olan üç katman üzerine kurulu bir stratejiden ibarettir. Mvc deyince bazen framework akıllara geliyor. Microsoft, Asp.Net üzerinde mvc frameworkü kullanarak bir geliştirme yaptı. Ama mvc esasında bir framework değildir, mvc aslında bir design pattern/tasarım deseni/salt bir stratejiden ibaret akıştır.
Mvc'yi illa Asp.Net'te kullanmak zorunda değilsin, php de kullanırsın, normal console uygukamasında bile kullanabileceğin tasarım desenidir. Belirli bir senaryoya uygun, uygulanabilir bir tasarım desenidir. Asp.Net bu tasarım deseninin üzerine oturtulmuş bir mimari bir franmework sunuyor bizlere.
Yani Asp.Net'in mvc mimarisini benimsemesi ayrıdır. O mimarinin adı mvc frameworktür. Ama mvc yaklaşımı direkt frameworkten bağımsız bir design patterndir.
Mvc, bir design patterndır.
Üretilen veri ile gösterim arasında(sunum katmanında) bir soyutlama esas alınmıştır. 
Model, veri tabanı işlemlerini yapar.
View, görsellik/sunum işlemlerini yaptığımız katmandır.
Controller, istekleri karşılayan gerekli işlemlerin gerçekleştirildiği, model ile view arasında köprüsel işlemlerin üstlenildiği bir katmandır.

![10-1](https://github.com/user-attachments/assets/e03c5a81-539e-4869-bf73-e8b81e525012)

Kullanıcı controllera yani ilgili web sitesine bir istek gönderdiği zaman bu controller tarafından karşılanır eğer veri tabanı işlemi varsa controller modela gider. İlgili veri tabanı işlemini yapar. Elde ettiği/ürettiği veriyi viewa gönderir. View da ilgili veriyi html css e çevirir ve sonucu döner.

👉 ! Asp.Net Core yapılanmasında api ve mvc tasarımı birleştiirlmiştir.

Mvc patternı Microsoft tarafından üretilmiştir. Böyle bir yanılgı vardır. Mvc, Microsoft'un kurulduğu yıllarda(1979 yılından) beri tasarlanmış bir kalıptır. vc mimarisini alıp, mimarini bu tasarım altyapısında geliştirmek ayrı, mvc'yi senin oluşturman ayrıdır. Microsoft şunu yapmış, bir tasarım deseni var bu tasarım desenine uygun bir tane web geliştirme mimarisi geliştiriyor. Bu mimari üzerinden sen web uygulamalarını daha hızlı bir şekilde geliştirebiliyorsun. 

✨✨

MVC bir tasarım desenidir:
Model-View-Controller (MVC), yazılım mimarisi için bir tasarım desenidir.
İlk olarak 1970'lerde Smalltalk için geliştirilmiştir.

MVC'nin amacı:
Uygulama mantığını kullanıcı arayüzünden ayırmak.
Kodun bakımını, test edilebilirliğini ve yeniden kullanılabilirliğini artırmak.

MVC'nin bileşenleri:
Model: Veri ve iş mantığı
View: Kullanıcı arayüzü
Controller: Kullanıcı isteklerini işler, Model ve View arasında iletişimi sağlar

MVC bir framework değildir:
MVC, bir uygulama yapısı için rehberdir, spesifik bir teknoloji veya framework değildir.
Farklı programlama dilleri ve platformlarda uygulanabilir.

MVC tabanlı frameworkler:
ASP.NET MVC, Ruby on Rails, Laravel (PHP) gibi frameworkler MVC prensiplerini uygular.
Bu frameworkler, MVC desenini kendi yapıları içinde yorumlar ve uygular.

Microsoft ve ASP.NET MVC:
Microsoft, ASP.NET platformu için MVC desenini uygulayan bir framework geliştirdi.
Bu, MVC prensiplerini .NET ekosistemi içinde kullanmayı kolaylaştırdı.

MVC'nin esnekliği:
MVC, farklı uygulamalarda farklı şekillerde yorumlanabilir ve uygulanabilir.
Temel prensipleri korurken, spesifik ihtiyaçlara göre uyarlanabilir.

MVC ve diğer desenler:
MVC, MVVM (Model-View-ViewModel) veya MVP (Model-View-Presenter) gibi benzer desenlerin temelini oluşturur.

Sonuç olarak, MVC bir framework değil, bir tasarım desenidir. Frameworkler bu deseni uygulayabilir, ancak MVC'nin kendisi belirli bir teknoloji veya implementasyona bağlı değildir. 

✨✨

👋 3 - Application Programming Interface (API) Yaklaşımı

Uygulama programlama arayüzüdür.
Webde çalışabilen ve web uygulamaları, işletim sistemleri, veri tabanı, donanımlar veya yazılım kütüphaneleri ile iletişim kurabilen bir arayüzdür. 
Direkt olarak web uygulaması yaklaşımıdır diyemeyiz. Çünkü web uygulamasının dışındada kullanılan bir yapılanmadır. Bu yüzden her yerde kullanabilirsin ama web uygulamasında da kullanabildiğimiz için bu yaklaşımı benimseyebiliriz. Bir web uygulaması backendde api ile verileri üretebilir. Api genellikle web tabanlı uygulamalarda client ve server arasındaki iletişimi sağlayan bir sözleşme olarak kullanılmaktadır. Bu forma web api denmektedir. 

Apiyi, web üzerinde çalışan bir backend oalrak düşün. Herhangi bir görsel yanı yok ve http protokolü üzerinden her yerden istek alabiliyor. Eğer ki sen bir apiye web sayfası üzerinden istek gönderiyorsan client olarak, buradaki client web sayfası oluyor server ise api oluyor. İşte burada apiye gönderdiğin istek sonucunda sana gelecek olan verilerer burda sözleşme olarak nitelendirilebilir. Şöyle düşün, bana tüm personelleri getir şeklinde apiye istek yapıyorsun bu istek sonucunda sunucudan/serverdan/apiden sana personeller belirli formatta geliyor. Belirli formatın türünü vs. sözleşme diye nitelendirebiliyoruz. Burda entity kavramı bizim için sözleşmedir. 

Apiyi web uygulamalarında kullanıyorsak biz buna web api diyoruz. Peki api sadece webde mi kullanılıyor? Tabiki hayır, nesnelerin interneti denen olay bunun temeliden geliyor. Siz telefonu tableti vs. apiye bağlayıp internetten yönetebilir yada farklı nesnelerle iletişim kurabilir hale getirebilirsiniz eğer ki bu nesnelerden biri web ise buna web api diyoruz. Api ile bir çok nesneyi internete bağlayabilirsiniz. Api bir web geliştirme mimarisidir.
