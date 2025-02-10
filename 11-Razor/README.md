👋 19 - Razor Nedir? Kullanım Durumları Nelerdir?


Razor, ASP.NET Core MVC mimarisinde CSHTML dosyasında C# kodları yazabilmemizi sağlayan bir teknolojidir. Microsoft tarafından geliştirilmiştir. HTML ile beraber kod yazmamıza olanak tanır ve C# kodlarının server tarafında çalıştırılmasını sağlar.

ASP.NET Core MVC'de HTML içine gömerek C# kodlarını yazmamızı sağlayan bu söz dizimi, güçlü bir yapı sunar.

CSHTML içinde @ operatörü, Razor'ı ifade eder ve Razor operatörüdür.

👉 ! Yorum satırı: @* ...... *@ şeklindedir.

✨ Razor ile Değişken Oluşturma - Razor'da Değişken Okuma ✨


![19-1](https://github.com/user-attachments/assets/a5071ae8-9ea2-4ce6-9b35-298136230708)

@{
    var name = "Merhaba Dünya";
}
Bu şekilde Razor operatörü ve scope ile bu scope içine oluşturacağın/yazacağın her şey C# kodu olacaktır. Değişken tanımlaması ve farklı işlemler yapabilirsin.

✨ Razor ile Parçalı Scope Yapısı ✨


Razor'da @{} şeklinde parçalı birden çok scope olabilir. Bu yapılar derlendiğinde tek bir scope haline gelir. Dolayısıyla ilk scope'da name adında bir değişken tanımladıysan sonraki scope'larda da name değişkenine erişebilirsin.

Burada aynı derecede olmaları önemlidir. Örneğin, ilk scope içinde farklı bir yerde name tanımlasaydın ve diğer scope'lardan erişmeye çalışsaydın erişemezdin, çünkü dereceleri farklı olurdu. Dereceyi aynı hiza/aynı yerde kullanmak olarak düşünebilirsin.

✨ Razor İçinde HTML Kullanımı ✨


![19-2](https://github.com/user-attachments/assets/58f23253-e7de-4755-8365-e7559ebd806d)

✨ Koşul Yapıları ve Döngüler ✨


![19-3](https://github.com/user-attachments/assets/f5686800-8d05-449a-94ac-0e41e1194dd6)

![19-4](https://github.com/user-attachments/assets/12046295-2cd8-431c-9b6f-92022f482257)

Koşul ve döngü yapılarında illa scope kullanman gerekmez.
