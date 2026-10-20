# Karavan Webasto V3.10 — Web Önizleme ve Otomatik Termostat

**Kaynak:** Kullanıcının göndermiş olduğu `Karavan-Webasto-V3-9-OTOMATIK(1).zip` dosyası.

## Çalışan komutlar korunmuştur

`ble.js`, `auto-engine.mjs`, `command-profile.mjs` ve `protocol.mjs` içindeki **RE5011 Dizi C START**, **STOP/CLEAR**, **0x66 hedef** ve doğrulanmış durum okuma mantığı değiştirilmedi; yalnızca JavaScript modül sürüm parametresi güncellendi. Fiziksel cihazda bu sürüm ayrıca test edilmelidir.

## V3.10 yenilikleri

- Yeni, sade, telefon ekranına uyumlu ana panel; gereksiz hedef sıcaklığı +/- ve zorunlu hedef test adımı kaldırıldı. Gerçek komutlar hâlâ açık kullanıcı izni ister.
- START ve STOP sıcaklık eşikleri ayrı; STOP hedefi otomatik aktifken cihaz hedefine gönderilir.
- Otomatik mod **tercihi** tarayıcı depolamasına kaydedilir ve START/STOP döngüsünde görsel olarak değişmez.
- Yeni açılan/yenilenen sekmede **tercih açık kalsa da gerçek otomatik kontrol kendiliğinden devreye girmez**. Bluetooth, kullanıcı komut izni ve “Otomatik kontrolü başlat” onayı gerekir. Ekranda “Beklemede” görünür. Bu hayati güvenlik ayrımıdır.
- Bluetooth geçici koparsa otomatik tercihi açık kalır, kontrol “Bağlantı bekleniyor” gösterir; cihaz kendiliğinden durmaz. Yeniden bağlanma mevcut V3.9 mantığını kullanır. 10 dakika yeniden bağlanılamazsa aktif kontrol beklemeye alınır.
- Manuel START/STOP, otomatik tercihini kullanıcı müdahalesi olarak kapatır.
- Gün/saat ile çalışma geçmişi, bugünkü doğrulanmış START/STOP sayıları, kayıtlı START–STOP çiftlerine dayanan tahmini çalışma süresi, CSV olarak dışa aktarma ve geçmişi temizleme.
- Son 24 saat ortam sıcaklığı grafiği (tarayıcı açıkken gelen ölçümler; demo ve gerçek ölçümler ayrıdır).
- İsteğe bağlı tarayıcı bildirimi (silent özelliği istenir; tarayıcı/işletim sistemi sessizliği garanti etmez), gece görünümü.
- Gelişmiş ayarlar ve BLE tanı kayıtları katlanır bölüme taşındı; tanı TXT olarak indirilebilir.
- İnternetsiz görsel deneme için demo ve sıcaklık +3/-3°C düğmeleri.
- Durum paketleri CRC ile kontrol edilir, hatada yeni otomatik komut gönderilmez. V3.9'da bulunan 4 START/saat sınırı, STOP teyidi ve beklemeler korunur.

## Kurulum (GitHub Pages)

1. Çalışan V3.9 deponu YEDEKLE. En iyisi yeni bir depo ya da yeni bir dal oluştur.
2. ZIP içindeki dosyaları **klasör oluşturmadan**, depo köküne yükle; `index.html` doğrudan kökte olmalı.
3. Settings → Pages → Deploy from a branch → `main` / `(root)` → Save. Yayın bağlantısında `V3.10` yazdığını doğrula; `Ctrl+Shift+R` ile yenile.
4. Önce **Demo** ile görünüm ve termostat davranışını dene. Demo sıcaklığını 20°C altına indir, START bekle; 25°C üstüne çıkar, STOP gecikmesini bekle. Tekrar START için yeniden başlatma beklemesi işler.
5. Gerçek cihazda bağlantı kur; **Gerçek Webasto komutlarına izin veriyorum** kutusunu aç. Önce gözetim altında manuel START/STOP dene.
6. Otomatik modu açınca ek onay istenir. Sayfa yenilendiyse tercih açık ama kontrol `Beklemede` olur; **Otomatik kontrolü başlat** butonuyla tekrar onay ver.
7. En sonunda tam bir otomatik START→STOP→START döngüsünü cihazın yanında test et. Soğutma tamamlanmadan güç kesme.

## Sınırlar

- **Bu bir WEB uygulaması:** Bilgisayar ve tarayıcı açık/çalışır olmalı; sekme uyuyabilir veya işletim sistemi durdurabilir. iOS arka plan kontrolünün çalıştığı anlamına gelmez.
- Web bildirimleri tarayıcı ve işletim sistemi ayarlarına bağlıdır; `silent:true` talebi her durumda sessiz olacağını garanti etmez.
- Cihaz bağlantısı kaybolduğunda otomatik kontrol edemez; ısıtıcı çalışmaya devam edebilir.
- Çalışma geçmişindeki START/STOP sayıları **cihazdan doğrulanan komut geçişlerini** sayar, gerçek yanma süresi veya yakıt miktarını ölçmez. Geçmiş o tarayıcıdaki localStorage'da tutulur; başka cihazda otomatik olarak görünmez.
- Dizel ısıtıcıda sağlam egzoz, doğru havalandırma, çalışan CO alarmı ve üretici güvenlik koşulları şarttır. Gözetimsiz çalışma güvenliği bu yazılım tarafından sertifikalandırılmamıştır.
