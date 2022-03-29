# Web Uygulama Güvenliği
**1. XSS**(siteler arası betik çalıştırma)
- Tarayıcının zararlı kodu websitesinin kodu gibi düşünerek çalıştırmasıyla ortaya çıkar
- Kullanıcının oturum bilgileri ele geçirilir
- Reflected XSS ,Stored XSS türleri bulunur
- Korunma Yöntemleri arasında, sayfada bulunan girdiler filtrelenmeli ve kontrol edilmeli.Yapılan filtreler encoding yöntemyile atlatılabilir böylece beyazliste kullanılması daha mantıklı olabilir.

**2. IDOR( Insecure Direct Object References)**

Sunucu üzerinde objelerin direkt referansları ile erişim sağlanması
https:/somewebsite/userId=someUser gibi userId değiştirerek başka kullanıcının sayfasına ulaşılabiliyorsa bu zafiyet vardır.

**3. Command Injection**
Uzak sunucuda kod çalıştırmayı içeren zafiyet. İşletim sistemini hedefler. Netcat ile reverse shell açılabilir.
Korunma yöntemleri arasında, kullanıcı girdileri korunmalı, yetkiler kontrol edilmeli, girdi belirli kelimeler alıyorsa onlarla kısıtlandırılabilir.
*Commix* aracı ile tespit edilebilir.

**4. SQL Injection**
Uygulama içerisindeki alınan verinin izinsiz database sorgularının çalıştırılmasıyla olabilir.
- SQLUnion,SQLBlind farklı türleri arasındadır

 **5. File Inclusion**
 Dosya dahil etme, uygulamaya zararlı bir dosyayı uygulama içerisine yüklenmesi ile ortaya çıkar.Reverse
shell oluşturulabilir.
- İki türü bulunmaktadır.Local File ve Remote file inclusion
- Sunucundaki yerel dosyaların uygulama ile erişilmesi veya uygulamaya dahil edilebilmesi local file inclusion
- Genelde include() veya require() metotların yanlış kullanımı sonucunda ortaya çıkar
- Korunma yöntemleri, kullanıcı girdiler kontrol edilmeli, yüklenilen dosyaların uzantıları kısıtlanabilir, beyazliste oluşturarak

# Mobil Güvenlik ve Sızma Teknikleri
*Android* 
çalışan ilk process *zygote* olarak isimlendirilir.Uygulamalar kendi sandboxında çalışır ve her uygulama eşsiz bir id ye sahiptir.
Temel bileşenler
- `ContentProvider`, içerik sağlayıcı veri işlemeden sorumlu bileşen.Veri yazma,okuma gibi veri tabanı işlemleri gerçekleşir. Önemli olan özellik dışarıya açık olup olmadığı kontrol edilmelidir.Manifest içerisinde, <*provider*> tagi içerisinde `android:exported="true"` sayesinde başka uygulamalar tarafından kullanılabilmektedir. exported anahtarı varsayılan olarak true kabul edilmektedir.
* `Activity`, arayüze sahip ekran oluşturan bileşen
* `Service`, arkaplanda çalışan işlemleri yürütür. 
* `BroadReceiver`
* `Intent`, bileşenleri birbirine bağlayan yapı. Implicit intent her uygulama işleyebilir ve explicit intent sadece uygulama içerisinde bileşenleri kullanır. 
Her uygulama ve işlev gerekli izinleri almak zorundadır. İzin seviyeleri normal, signature(sistem tarafından kullanılan izinler) ve dangerous(kişisel izinleri barındırır)

*iOS*
Katmanlı bir yapıya sahip
*CoreOs* çekirdek seviyesi, *Core Services* coreOs soyutlama, *Media* medya kütüphaneleri içerir, *Cocoa Touch* iOS framework(swift)

Secure Enclave - Kritik işlemlerden sorumlu CPU, anahtar yönetimi ve low level kripto işlemleri gereçekleşir
secure element - apple pay çipi
Kernel- XNU kernel( unix değil)
Files system - ilk kurulumda oluşturulur ve slindiğinde kullanıcı verileri erişilemez
Keychain - parola yönetim sistemi

iOS uygulamaları dosya uzantısı IPA, objective-C/swift ile geliştirilir. manifest  özelliği taşıyan dosya `Info.plist` 
Android içerisinde java/kotlin - dex dönüşümü gerçekleşirken iOS uygulamalarında böyle bir dönüşüm mümkün değil uygulama assembly diline çevriliyor.

- Android analiz araçları, apktool,dex2jar,adb
Önemli dizinler **/data/app** uygulamaların olduğu dizin, /system/app sistem uygulamaları

Analiz aşamaları
1. Geliştirici Analizi
2. Statik Analizi - hedef, api çağrılarının tespiti, uygulama entrypoint bulma,kodu anlamlandırma hangi veri hangi fonksiyonu çağrıyor işlevlerini anlama
	> 1. Uygulama indirildikten sonra apktool ile decompile edilir
	> 2. d2j-dex2jar jar formatına çevrilir
	> 3. cfr --outputdir apkdizin apk.jar java koduna çevrilir
	> 4. manifest dosyasından analize başlanır

3. Dinamik Analiz - statik analizde alınan notları görmek

