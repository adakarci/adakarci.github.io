---
layout: post
title:  "Blogumu hosta nasıl yükledim?"
date:   2015-06-24 17:32:40
image: /assets/img1.png
image2: /assets/img2.png
image3: /assets/img3.png
image4: /assets/img4.png
image5: /assets/img5.png
image6: /assets/img6.png
image7: /assets/img7.png
image8: /assets/img8.png
image9: /assets/img9.png

categories: jekyll update
---


How do I deploy a Django project?

Bu yazıda hosting hizmeti veren Webfaction'ı kullanarak localde bulunan django projemi hosta nasıl yüklediğimi anlatacağım. Öncelikle [buraya][webfaction] girerek bir account oluşturuyoruz. Daha sonra siteye login oluyoruz ve başlıyoruz.

1 - Home/ webapps dizininde sizin oluşturacağınız projeler olacak. Önce bir application oluşturacağız. Menüde bulunan DOMAINS/WEBSITES sekmesine gelerek Applications seçiyoruz. Burada Add new application diyoruz ve karşımıza gelen pencerede şu seçimleri yapıyoruz. Denemeapp benim kendi verdiğim bir isim, siz istediğiniz ismi verebilirsiniz.
<img src="{{ page.image }}" /><p>

Daha sonra save yapıyoruz. Bizim ihtiyacımız olan dosyalar bu uygulamanın içinde oluşturuluyor.

2 - Static dosyalarımız için bir tane daha application oluşturuyoruz. Aynı şekilde Add new aplication diyoruz. Bu sefer App category ve App type farklı oluyor.
<img src="{{ page.image2 }}" /><p>

Resimde gördüğünüz gibi ben static_media ismini verdim. Bu uygulamamızı da save yapıyoruz ve şimdi web sitemizi oluşturalım.

3 - DOMAINS/WEBSITES menüsünün altındaki WEBSITES menüsüne geliyoruz ve sitemizi oluşturmaya başlıyoruz. Add new website butonuna tıklıyoruz. Karşımıza çıkan pencerede gereken yerleri dolduruyoruz.

<img src="{{ page.image3 }}" /><p>

-Burada sitenize bir isim veriyorsunuz. Ben resimde gördüğünüz gibi mysite adını verdim.

-Daha sonra domain name ekliyoruz. Ben ada.adalovelace.webfactional.com diye bir alan adı verdim. Bu arada adalovelace benim kullanıcı adım.

-Domain name verdikten sonra az önce oluşturduğumuz uygulamaları sitemize ekliyoruz. Add an application bölümünden Reuse an existing application diyerek static_media ve denemeapp uygulamalarını seçiyoruz. (siz hangi ismi verdiyseniz onu seçeceksiniz.)Burada static_media uygulamasını eklerken altta bulunan URL bölümüne "static" yazmayı unutmuyoruz.

4 - Var olan django projemizi FileZilla (ya da siz hangi programı kullanıyorsanız) ile hosta atacağız. FileZilla ile bağlandığımız zaman kullanıcı adınızın altında webapps dizinini altında oluşturmuş olduğunuz application'ları göreceksiniz.

-denemeapp dizinin içinde webfaction tarafından oluşturulan "myproject" adlı default bir django projesi var. Biz bu projeyi kullanmak yerine kendi projemizi yükleyeceğiz. Yani "myproject" adlı klasör ile aynı dizinin içinde olacak. FileZilla kullanarak dosyamızı yüklüyoruz. Ancak burada önemli olan static dosyaları(css, js, img) static_media klasörünün altına kopyalamamız gerekiyor.

5 - Şimdi geldi sıra ssh bağlantısı ile sunucumuza bağlanıp komutlarımızı vererek sitemizi çalışır hale getirmeye. Ama önce dosyalarımızda bir kaç yeri değiştirmemiz gerekiyor.

6 - Projemizin içinde bulunan settings.py dosyasını açıyoruz ve şu eklemeleri yapıyoruz, tabi siz kendi bilgilerinizi yazacaksınız:

<img src="{{ page.image4 }}" /><p>

veritabanına isim veriyorsunuz ve mutlaka yolunu gösteriyorsunuz yoksa no such table tablename hatası alırsınız.<p>
<img src="{{ page.image5 }}" /><p>

static dosyalarınız için yolu gösteriyorsunuz.
<img src="{{ page.image6 }}" /><p>

Bir güvenlik durumu olarak aşağıdaki satırı ekliyoruz. Tabiki siz kendi site adınızı yazıyorsunuz.
<img src="{{ page.image7 }}" /><p>

7 - Sıra geldi apache web sunucumuza hangi projeyi çalıştırması gerektiğini söylemeye. Oluşturduğunuz denemeapp uygulamasının içinde apache2/conf/httpd.conf dosyasını açarak orada bulunan tüm "myproject" ismini kendi django projenizin adıyla değiştirmelisiniz. Çünkü azönce webfactionun ilk olarak kendisinin "myproject" adlı bir proje oluşturduğunu söylemiştik ancak biz filezilla kullanarak kendi projemizi yüklediğimizi sunucuya söylememiz gerekiyor. Bu satırlardaki "myproject" gördüğünüz yere kendi proje adınızı yazın o kadar. Benim projemin adı myblog olduğu için myproject olan yerlere myblog yazdım:
<img src="{{ page.image8 }}" /><p>

ssh bağlantısı yapalım ve gereken dizine geçelim.

8 - Şimdi artık veritabanımızda tablolarımızı oluşturabiliriz. python2.7 manage.py syncdb diyerek tabloları yaratıp, superuser oluşturabilirsiniz. Ancak no module named hatası alırsanız paket kurulumu gerekiyor demektir. Burada önemli bir nokta var. Hangi python sürümünü kullanıyorsanız lib klasörünün altında o sürümü bulup oraya kurulum yapmanız gerekiyor.

9 - Şimdi static dosyalarımız için python2.7 manage.py collectstatic komutunu veriyoruz:
<img src="{{ page.image9 }}" /><p>

10 - İşte bu kadar. Şimdi apache restart yapıyoruz ve sitemize ulaşabiliriz./ /apache2/bin/.restart


[webfaction]: https://www.webfaction.com/

