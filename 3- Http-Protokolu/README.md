👋 1 - HTTP Protokolü Nedir ? Çalışma Mantığı Nasıldır ?

Client ile server arasında ilişkiyi sağlayan http protokolünü inceleyelim. 
Protokol dediğimiz yapılanma iki farklı yapılanmanın ortak buluşmasıdır. Client farklı bir yapılanma server farklı bir yapılanmadır. Dolayısıyla client ile server arasındaki bu ilişkiyi/haberleşmeyi sağlayan model bizim için http protokolüdür. Http protokolü, client ile server arasındaki haberleşmeyi sağlayan bir protokoldür. Sen bir web uygulaması yapacaksan http protokolünü öğren gerisi zaten geliyor.

✨ Peki Http Protokolü Nasıl Bir Çalışma Sergiler ? ✨

Http, client ile server arasındaki ilişkiyi 9 farklı fonksiyon ile gerçekleştirir. 

![5-1](https://github.com/user-attachments/assets/a5c10002-1c02-4011-a703-34cf956e7043)

Bu fonksiyonlar kullandığım client üzerinden herhangi bir veriyi elde etmek istiyorsam get, veri göndereceksem post, sunucudan veri silinecekse delete, sunucuda veri güncelleme yapacaksam put fonksiyonunu kullanırım. 

👋 2 - HTTP Fonksiyonları - Get - Post - Put - Patch - Delete

Http fonksiyonları 9 tane ama biz genellikle 5 tanesini kullanıyoruz. Http protokolü, client ile server arasındaki iletişimi sağlayan bbir protokoldür. Dolayısıyla bu iletişim esnasında http diyorki, ya client senin serverdan istediğin şey neyse ona uygun bir fonksiyon ile bu isteği gerçekleştir. 

![5-2](https://github.com/user-attachments/assets/6234ad3b-4dc7-4f1c-befd-f9b94ac8f2c1)

Sunucudan verileri listelemek yahut elde etmek için get kullanılır. Genellikle veri tababındaki sorgu karşılığı da selecttir. 

Sunucuya client veri gönderecekse post kullanılır. Bu veri ilk defa sunucuya gidecekse post kullanılır. Veri tabanında genelde insert sorgusu çalıştırılır. 

Sunucuda var olan bir veri üzerinde değişiklik yapacaksak yani güncelleme yapacaksak put ile yaparız. Eğer ki elinizdeki verinin tümünü değiştiriyorsanız var olan verinin yüm her şeyini değiştiriyorsa bu bi puttur.  Fakat var olan verinin sadece belirli bir kısmı değişiklik gösteriyorsa biz bunu patch ile sağlarız. Aslında ikiside put ve patch güncelleme odaklıdır ama biri bütünü değiştirirken diğeri bir kısmı günceller. 

Var olan verileri silmek için delete kullanılır. 
