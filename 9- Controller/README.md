👋 15 - Action Türleri Nelerdir ?

Asp.net core ugulamasında clienttan gelen request sonucunda bu requesti karşılayan controller sınıfının içinde gerekli aksiyonu almamızı sağlayyan action fonksiyonları üzerine konuşuyor olacağız. Action türlerinin birden fazla dönüş türü var. Bunları inceleyeceğiz.

Gelen request controller tarafından karşılanıyor ve controller ilgili isteğe uygun actiona yönlendiriyor/tetikliyor. Duruma göre/ihtiyaca göre actionda veri üretilmesi için modela gidiyor yada viewa gidiyor. En sonunda clienta gösteriyor. 

Daha önce actionun geriye döndürdüğü değeri sadece view result yani bir view cshtml dosyasının render edilmiş halini gönderdik. Burda öyle bir ihtiyaç doğuyor. Biz clienta hiç mi metinsel değer/boş bir değer/json formatta değer göndermeyeceğiz ? Peki bunları nasıl gönderebiliyoruz, ne şekilde çalışabiliyoruz bunları inceleyelim. 

![15-1](https://github.com/user-attachments/assets/7ac52606-6922-4a7c-93be-cdf67cc96f93)

Geri dönüş türlerine uygun değer üretmemiz gerekiyorsa, bu değerleri üretecek fonksiyonlar bizim base classımız(controller) tarafından bizlere sunulmaktadır. ViewResult(166. satır) ile bir değer üretmem ggerekiyorsa base classtaki view fonksiyonunu kullanmam yeterlidir. Yahut JsonResult ile elimdeki değeri jsona dönüştürmem gerekiyorsa JsonResult(44. satır) kullanmam yeterlidir. Yani sen hangi türde clienta değer döndüreceksen bu türe uygun fonksiyonu çağırman yeterlidir.

👉 ! ViewResult : Response olarak bir view dosyaysını/.cshtml render etmemizi sağlayan action türüdür. 


![15-2](https://github.com/user-attachments/assets/436fea66-f4f3-4933-85bd-74b134548a77)

Bir action fonksiyonu ViewResult geriye döndürüyorsa bu bir view render etmek ve ilgili render edilen sonucu/ViewResultu clienta göndermektir. ViewResultta, viewı render etmek istiyorsan base classtaki view fonksiyonunu kullanman yeterlidir. View fonksiyonu ilgili controller ismine karşılık gelen views klasörü altındaki bir klasörün içindeki action metodunu ismine karşılık gelen .cshtmli render eden/otomatik render ettiği viewı bize sonucunu ViewResult olarak döndüren bir fonksiyondur. 

✨ PartialViewResult ✨


![15-3](https://github.com/user-attachments/assets/ca037188-2857-409d-a5e2-780f4180dc46)

Yine bir view dosyasını(.cshtml) render etmemizi sağlayan bir action türüdür. ViewResulttan temel farkı, client tabanlı yapılan ajax isteklerinde kullanıma yatkın olmasıdır. ViewResult backendde clienttan yapılan istek client tabanlı değilse biz ViewResult kullanıyoruz. Eğer client tabanlıysa ajax teknolojisi ile işlem gerçekleştiriliyorsa sen PartialViewResult kullanmalısın. Çünkü, bir web safası düşün, bu web sayfasının ggenelini sana oluşturan ViewResulttur. Ama web sayfasındaki belirli bir noktayı/locali oluşturan PartialViewResulttur. 

✨ ViewResult ✨


ViewResult, ViewStart.cshtml dosyasını baz alır. Bu dosya viewların kabul edildiği/viewların başlangıç dosyasıdır. Bu dosya tüm viewlar tarafından render edilmeden önce render edilir. Haliyle ViewResult bu dosyayı baz alır. Fakat PartialViewResult, bu dosayı baz almadan render eder.

✨ ViewStart ✨


![15-4](https://github.com/user-attachments/assets/c2d5935e-d663-4bfc-9eba-75b37f3c2635)

ViewStart, içinde layout(genel tasarımı) tutan başlangıç viewdır. Dolayısıyla ViewResult bu başlangıç viewı ile render edilidği için genel sayfayı render eder. Sen genel sayfayı değil belirli bir alanı render edip onun çıktısını o alanda kullanmak istersen sayfanın genelini render etmeden belirli bir parçasına odaklı render işelmmini yapmak istiyorsan/yani ViewStartı baz almak istemiyorsan PartialViewResultu kullanman gerekiyor. 

✨ JsonResult ✨


![15-5](https://github.com/user-attachments/assets/f4a84e3c-c6e7-44e3-8b79-806f811dd156)

Sen clienta gelen istek neticesinde json formatında bir değer döndüreceksen JsonResult döndürebilirsin. Hangi değeri json nesnesine dönüştüreceksek onu benden nesne olarak istiyor ve sonuç olarak JsonResult döndüreceğini bildiriyor. Json fonksiyonu, kendisi otomatik jsona dönüşüm yaptığı için senin extra bir şe yapmana gerek yok. 


✨ EmptyResult ✨

![15-6](https://github.com/user-attachments/assets/638b1dfa-3d9b-4888-949c-35ff69692f7b)

![15-7](https://github.com/user-attachments/assets/6ec1fab0-4eee-4cae-b480-42b19c400698)

Bazen gelen istekler neticesinde herhangi bir şey döndürmek istemeyebiliriz. Böyle bir durumda EmptyResult action türü kullanılabilir. Geriye boş bir result döndürmek istediğinde EmptyResult kullanırsın. Yani response var ama result yok. Geriye direk EmptyResult nesnesi döndürmen gerek. Base classta kullanabileceğin bir metot yok çünkü. 

![15-8](https://github.com/user-attachments/assets/e5a8fe5e-aa76-4de2-abc3-b161c4204a32)

Aynı zamanda void ile de aynı şeyi yapabilirsin. 

👉 ! Http protokolü üzerinden sen request yaptığın zaman mutlaka bir tane response olur. Ama response da result olup olmama durumu değişir. 


✨ ContentResult ✨


İstek neticesinde cevap olarak metinsel bir değer döndürmemizi sağlayan action türüdür. Base classtaki content fonksiyonu ile content sağlanır. 

![15-9](https://github.com/user-attachments/assets/74cd5c93-c674-4721-9588-2cecb92e450f)

Buradaki davranış önemli. Sana cevabı/sayfnın formatını sana text olarak gönderir. Örneğin sen "<br/>" şklinde tırnak iinde tag kullanırsan çıktı olarak yine aynı şşekilde <br /> görünür/render edilmez. Çünkü, html olarak değil text/metinsel değer olarak algılanıyor. Bu yüzden JsonResult ve ContentResultu ajax tabanlı işlemlerde kullanıyorz.

✨ ViewComponentResult ✨


Asp.net core'da gelen modüler bir yapılanmadır. Dolayısıyla bunu anlayabilmek için ViewControlResultu bilmek gerekir. Kısaca şu şekilde açıklanabilir: İsteğe cevap olarak bir ViewComponent render etmmemizi sağlaan action türüdür. 


✨ ActionResult ✨


Bütün result türlerinin base classıdır. Gelen bir istek neticesinde geriyye döndürülecek action türleri değişiklik gösteerbildiği durumlarda kullanılan bir action türdür. Yapılan istek sonucunda geriye json//partial/content döndürmen gerekebilir. İşte bunların hepsini tek bir fonksiyon içinde dönebilmen için bunların bir ortak türe ihtiyacı var. Bu tür action resulttur. Action result bir base classtır/atalarıdır. 

![15-10](https://github.com/user-attachments/assets/a3fedb3c-5ece-4019-9710-f444eef65396)

ActionResult, tüm aciton türlerini karşılayan ana türdür.

👉 ! IActionResult ise, actionResultun bir interfaceidir. Polimorfizm kurallarını uyygulayabilmek için kullanacağız. 

👋 16 - NonAction ve NonController Attributeleri

Controllerların genelde requestleri karşşılayan, actionların ise bu requestler gereği gerekli operasyonları tetikleyen fonksiyonlar olduğunun farkındayız. Controllerın temel amacı sadece requestleri karşılamamaktır. Algoritmaları/servisleri tetiklemelidir.  O algoritmaları barındıran servisleri çağırmalıdır. Controller, bir nevi yönlendirme yapıyor gibi düşünebilirsin. Örneğin ayın kampanyalı ürünlerini listeleyen bir istek geldi. Controller bu isteği alıp sonucu döndüren şu sınıfa şu metoda git diyor/kendisi karşılayıp yyönlendiriyor. Yani controller içinde kesinlikle işş mantığı olmamalıdır. 

Action metotları, işi yapacak olan servislerin tetiklenmesinde gerekli yönlendirmeyi sağladığımız algoritmik opperasyonları sağladığımız metotlarımız action metotlarımızdır. Controller içinde actionlar gerekli noktalarda yönlendirme yapar ama iş yapmaz. Actionlar iş yapmak için değil iş alan iş mantığını yürüten sınıfları/servisleri çağırmak için vardır. 

Dışarıdan isteği karşılayabiliyorlarsa yani action metotsa kesinlikle bir iş mantığı üstlenmemelidir. İş mantığını üstlenen servislere yada katmanlara gerekli taleplerde bulunmalıdır. Eğer ki ihtiyacınız, bir controller sınıfı içinde oluşturulan metot iş mantığı yürüten metotsa yani requestt karşılamaktan ziyade bir işe odaklıysa ki bu tavsiye edilmez. Controllerların içindeki actionlar genellikle request alacaklarından dolayı iş mantıklarını actionlarda tanımmlamayız. Başka sınıflarda tanımlarız. Ama diyelim ki böyle bir ihtiyacımız oldu. Yani controller içindeki bir action, requesti üstlenmeyecek direk işi üstlenecek. Bu durumda ne yapılması gerek ?

ProductControllerda void X i action değil iş mantığını üstlenen metot olarak tanımlamak/tasarlamak istersem ve buna request neticesinde değilde action metotların içinde tetikleme esnasında çağırıp/kullanmak istiyorsam, burda x() i iş mantığı olarak kullanacaksam void x kısmında x e  gelecek olan requestleri engellemem gerekir. Çünkü x sadece iş mantığı olarak çalışsın istiyorum. İşte böyle bir durumda biz controller sınıfları içinde tanımlanmış olan metotların iş mantığı amaçlı kullanılmasını ani dışarıdan gelen requestlerin alınmasını engellemek istiyyorsak sadece işş mantığıla o amaçla kullanacaksak ilgili metodun bir action metot olmadığını bildirmemiz gerekir. Bunun içinde nonAction attributeu kullanılır. 

![16-1](https://github.com/user-attachments/assets/23fb09f5-2756-4b16-8ad5-971cb75566ff)

X bir action değilse sadece bir iş mantığı üreten operasyonel fonksiyon ise bu metotu nonAction ile işaretlemem gerekir. 

👉 ! Controller içinde nonAction attributeı ile işaretlenen fonksiyonlar dışarıdan request alamazlar. Adı üstünde nonAction/bu artık bir action değil. Normalde default olan hali bir actiondur. Ancak nonAction ile işaretlenirse artık request karşılamaz durumda olur. 

✨ NonController Attribute ✨


![16-2](https://github.com/user-attachments/assets/0c5d52bf-c591-4e5a-ac0c-e919bfbf49a7)

Controller seviyesinde kullandığımız attributedur. Sistemde var olan tüm controllerlar dışarıdan istek alabilirler. Siz hem controller tanımlar hemde dışarıdan istek almasını istemiyorsanız ilgli controllerı nonController ile işaretleyebilirsiniz. NonController attribute ile sıradan bir sınıf yapmış olduk.  
