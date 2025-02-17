37 - Modüler Tasarım Açıklaması Nedir? Nasıl Uygulanır?


Modüler Tasarım Nedir?
Küçük parçaların bir araya gelerek bir bütün oluşturduğu yapılanmadır/tasarımdır.

Örneğin, bir araba düşünelim. Arabanın tekeri, kapısı, farı gibi farklı parçaları vardır. Arabanın tekerinde bir sorun olduğunda pencereyi etkilemez. Sadece tekere, yani o parçaya odaklanarak çözüm üretebiliriz.

Modülerlik, parça-bütün-parça ilişkisini ifade eder. Bütün işlemleri tek bir sorumluluğu üstlenecek parçaların bir araya gelerek bütünü oluşturmasıdır. Modüler tasarım yalnızca MVC'ye özgü değildir, bu bir mantıktır ve kullanacağın mimariye uyarlanması gerekir.

Web Uygulamalarında Modüler Tasarım Yapılanmasını Nasıl Kullanabiliriz?
MVC mimarisinde modüler tasarım için iki temel yapılanma vardır:

Partial View
View Component
Bir web sayfasında üst menü, sol menü, alt kısımdaki footer ve içerik (content) bölümleri olduğunu düşünelim. Eğer tüm bu yapıları tek bir sayfadan yönetiyorsan, bu ideal bir tasarım değildir. Bunların her birini farklı .cshtml dosyaları olarak ayırman gerekir.

Bu ayrı parçaları kullanmak istediğin yerlerde referans etmen yeterlidir.

Modüler tasarım sayesinde:

Sayfa değişikliklerini hızlı bir şekilde yapabilirsin.
Eğer bir bölümü taşıman gerekiyorsa (örneğin, alt menüyü üst kısma almak), hızlıca değiştirebilirsin.
Tüm kodları kopyala-yapıştır yapmak yerine referans vererek işlem yaparsın.
Sayfa tasarımına daha hızlı müdahale edebilme şansın olur.
Partial View Nedir?
Modüler tasarım yapılanmasında her bir modülü ayrı bir view olarak tasarlamamızı sağlayan ve bunları parça view olarak ana view’de birleştirmemizi sağlayan bir tekniktir.

Modüler tasarımda:

Her bir modül ayrı bir .cshtml dosyası olarak tasarlanır.
İhtiyaç doğrultusunda ilgili parça çağrılıp kullanılabilir.
Herhangi bir view dosyasını parça (partial) olarak kullanmanı sağlar.
View Component ve Partial View Arasındaki Davranış Farkı Vardır.
View Component ve Partial View aynı amaç doğrultusunda kullanılabilir ancak çalışma prensipleri farklıdır.
