👋 1 - İnternette Gezerken Perde Arkası Nasıldır ? 

Normalde tarayıcıdan/internetten alibaba.com sitesine girdin. Günlük kullanımdaki bu telaffuz artık bir yazılımcı için değişmelidir. Girmek yada tıklamak yerine request/istek atılır. Response/cevap alınır. Senin attığın istek servera gidiyor, serverda karşılandıktan sonra sana ilgili sonuç üretilir. Bu sonucu döndürür ve sen tarayıcında bunu görürsün. 

Request : Artık bir web sitenin açılması için yaptığımız eyleme girdik/tıkladık vs değil, istek gönderdik diyeceğiz. 

✨✨
Request atan kim : client,
Bu clientı kullanan kim : user, 
Bu user nereye istek atıyor : hostinge/servera,
Hostinge/servera ne üzerinden istek atıyor : ip,
ip ile domaine yönlendirme yapılıyor vs.(süreç bu şekilde ilerliyor.)
✨✨

👋 2 - Temel Kavramlar - User - Client - Hosting _ Domain - Request - Response

Client, userın kullandığı teknolojidir. Pc, telefon, tv kumandası...

User, bizler/client kullanıcısıdır.

Bir web sitesine girebilmek için onun erişilebilir olması lazımdır. Herhangi bir pc de değil evrensel bir noktada olması gerekir. Bu web sitesi/uygulaması internette bir yerde tutuluyor. 

Webe girmek isteyen kişi userdır. Userın webe girmek için kullandığı teknoloji/cihaz/uygulama clienttır. İnternete girebilmek/istek yapabilmek için kullanmış olduğun uygulama clienttır. 

👉 ! Client, istemci demektir, istek yapan şey demektir. 

User clientı kullanarak internet girer, peki internete nasıl giriyor ? Şimdi internete www.gencayyildiz.com diye bir site var. Bu site internette öyle ortada gezmiyor. Bunu internette 7/24 saat açabilecek bir mekanizma/pc olması lazım. Bu pc ye biz sunucu/server/hosting diyoruz.

👉 ! Client herşey olabilir. Genelde web siteleri ya da kullanıcılar client zannedilir. Aslında hayır Client dediğiniz bir pil bile akıllı pil ise yine client olabiliyor. Yani client istemci demektir. İsteği yapan şey demektir.

👉 ! Örneğin televizyon izlerken, televizyonu izleyen ben userımdır. Kumandayı kullanarak program değiştirmem/bununla istek yapmam kumandanın client olması durumudur. İsteği yapan/bunun iradesine sahip olan kişi user, istemci/client kumanda, televizyon ise benim server'ımdır.

✨ Hosting Nedir ? ✨

Normalde ben kendi web sitemi www.gencayyildiz.com u kendi bilgisayarımda dış dünayaya açabilirim. Hosting firmaları 7/24 yayında tutabilmemizi sağlayan bilgisayarları barındıran firmalardır. Hosting/server/sunucu yerine cloud sistemleri de kullanılabilir (azure, amazon gibi). 

User client üzerinden servera istek atıyor. Bu istek sonucunda hosting uygulamayı çalıştırarak sonucunda bana yani clienta response dönüyor. 

Sunucuya istek atma/gönderme (Request) : Client üzerinden userın yaptığı istektir. Request içerisinde, hangi adrese/ipye/domaine istek gönderildiği bilgisi tutulur. Clientın yeryüzünde binlerce domaini olabilir. Bunlardan hangisine istek göndereceğimizi ayırt edebilir. Buradaki ayırt etme operasyonu ip üzerinden sağlanır. Ip dediğimiz, birbirinden bağımsız unique/farklı/benzersiz kimliktir. Demek ki, hostingin ipsi varmış. Daha doğrusu senin web sitene bir tane ip veriyor bu hosting. Sen bu ipye istek gönderiyorsun. 

Sunucudan clienta istek dönmesi/cevap vermesi (Response) : Sunucu tarafından clienta dönen cevaptır. Bu cevap server tarafından üretilen resultu da barındırabiliyor. İlla ki result olmak zorunda değildir. Örnek bir istek yapılır cevap döner ama bu cevapta result olmak zorunda değildir. 

Request, ip/adres/domain bilgisini taşıyor. Sen bir web sitesine istek göndereceksen giden isteğin headerında www.gencayyildiz.com var oraya istek at diyoruz. İstek sonucunda o isteği web uygulaması arkada çalıştırıyor. O istek hangi sayfayı render edecekese oluşturuyor ve oluşumu sonucunda bir tane result oluşturuyor. Oluşan resultı hosting, response olarak geriye döndürüyor. Yani üretilen web çıktısını bize geri getiriyor. 

API'yi tüketen farklı clientlar vardır. Sonuçlar o clientlarda da elde edilebilir illa browser olmasına gerek yok. Dolayısıyla normal bir internet kullanıcısı tarayıcı üzerinden bu istekleri yaptığı için hostinden/sunucudan gelen render edilen sonuç/result yeniden browsera gönderilir. Request sonucunda gelen result browsera yüklenir. Sende ekranda görmüş olursun. 

👉 ! Ip, anlamsız sayısal değerlerdir. Domain, ip'ye yönlendirilmiş anlamlı metinsel değerlerdir. 

