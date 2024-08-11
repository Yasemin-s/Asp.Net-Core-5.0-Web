👋 1 - Sunucu Çeşitleri - IIS - Kestrel - Nginx - Apache - Http.Sys - Docker

Web uygulamalrını ne tarz bir sunucuda ayağa kaldırıyoruz bunu inveleyeceğiz. Sunucu incelememiz web mimarisinden bağımsızdır ama yine de inceleyeceğiz. Biz web ugulamalarını bitirmişiz elimizde bir ürün olmuş ve bu ürünü hostinglerde yada cloud yapılanmalarında ne tarz suncularda yayınlayabileceğimiz derdine düştüğümüzde bu bilgilere ihtiyacımız olacak. 

IIS (Internet Information Services) : Asp.net core dahil olmak üzere web uygulamalarını barındırmak için esnek , güvenli ve yönetilebilir bir web sunucusudur. 

Kestrel : Asp.net core uygulamalarında dahili olarak gelen bir web sunucusudur. Asp.net core kendi bünyesinde kendi sunucusunu taşıyabilen uygulamadır. İşte bu sunucu kestreldir. 

![7-1](https://github.com/user-attachments/assets/a9f4cf4a-30f2-49f9-8c10-d1710e41c1e8)

Yani IIS olmadan herhangi bir microsoft platformuna bağlı olmadan kendi bünyesinde sunucusunu taşıdığı için kendi kendini ayağa kaldırabiliyor ve linux, ubuntu gibi noktalarda da kullanılabiliyor. 

Nginx : Ubuntu/Linux sistemlerde asp.net core uygulamalarını çalıştırabilmemizi sağlayan bir sunucudur. Reverse proxy olarak asp.net core uygulamalarındaki dahili sunucuyla(kestrel) işlevsellik gösterir. 

![7-2](https://github.com/user-attachments/assets/80287080-c030-4597-a5b6-4a77836779fb)

Burada core uygulamasında kendi bünyesinde kestrel vardır. IIS, Nginx, Apache sunucular diğer işletim sistemlerinde kestrel ile iletişim kurabilecek şekilde tasarlayabiliyoruz. Dolayısıyla ben hangi işletim sistemiyle çalışırsam çalışayım işletim sistemine olan bağımlılık ortadan kaldırılıyor. Bunların kestrel ile olan senkronizasyonu sayesinde ilgili uygulama ayağa kaldırılıp kullanılabiliyor. 

Apache : 

![7-3](https://github.com/user-attachments/assets/c7525379-f7e8-4012-b082-ff1465e181ff)

Linux vs. gibi ortamlarda apache ile asp.net core uygulamalarını ayağa kaldırabiliyorsun. 

Docker : Yazılım geliştiriciler ve sistem yöneticileri için geliştirilmiş açık kaynak olan bir yeni nesil sanallaştırma platformudur. Docker tek başına bir sunucu değildir bir sanallaştırma platformudur. Kendi içine biz sunucu kurup farklı çalışmalar tercih edebiliyoruz. Sanallaştırma platformunun da amacı budur, senin bulunduğun platformun dışında ondan bağımsız farklı platformlar yaratabilmektir. 

Http.Sys : Yine uygulama içinde gelen bir sunucudur. Yalnızca windows üzerinde çalışan asp.net core için web suncusudur. Kestrelin bir alternatifidir.

![7-4](https://github.com/user-attachments/assets/9c745515-7558-4310-a90a-ad82f3676242)
