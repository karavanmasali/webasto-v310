# Karavan Webasto V3.11 — 3 Sekmeli Web Arayüzü

Bu sürüm, kullanıcının V3.10 sürümü üzerine hazırlanmıştır. **Bluetooth protokolü, Dizi C START, STOP/CLEAR, hedef sıcaklık, otomatik motor ve termostat hesapları aynen korunmuştur.** Değişen dosyalar yalnızca `index.html`, `style.css`, `app.js` (pasif sekme yönetimi, son işlem göstergesi, sürüm yazısı) ve `manifest.webmanifest` (sürüm adıdır).

## Yeni arayüz

- **Kontrol:** bağlantı, ortam sıcaklığı, otomatik mod, START/STOP dereceleri, manuel START/STOP ve son işlem.
- **Geçmiş:** bugünkü START/STOP sayıları, çalışma süresi, olay listesi, CSV, 24 saat sıcaklık grafiği.
- **Ayarlar:** sessiz bildirim, gece görünümü, termostat gecikmeleri, cihaz bilgileri ve tanı kaydı.
- Alt gezinme sabit kalır. Sekme değiştirmek **sayfayı yenilemez**, BLE bağlantısını kesmez ve otomatik modu kapatmaz.
- Bağlantı ve cihaz verisi başlıkta görünür.

## GitHub Pages kurulumu

1. GitHub üzerinde ayrı bir depo oluştur: ör. `webasto-v311`.
2. ZIP içindeki **14 dosyayı** deponun kök dizinine yükle (`index.html` doğrudan kökte olmalı).
3. Settings → Pages → Deploy from a branch → `main` / `(root)` → Save.
4. GitHub Pages adresinden `Demo` seçeneğiyle üç sekmeyi ve otomatik START/STOP göstergelerini dene.
5. Gerçek Bluetooth testi için Windows 11 Chrome kullan; Web Bluetooth her tarayıcıda desteklenmez. İzin kutusu ve otomatik onay gereklidir.

## Kontrol güvenliği ve sınırlamalar

- Demo işlemleri fiziksel cihazı kontrol etmez. Gerçek cihazda V3.11'i ayrıca test etmeden önceki başarıya güvenme.
- Otomatik modun açık **tercihi** saklanır; sayfa kapanıp yeniden açıldığında Bluetooth tekrar bağlanmalı ve komut izni/onayı verilmelidir.
- Tarayıcı kapalıyken, bilgisayar uykuya geçtiğinde veya bağlantı koptuğunda termostat güvenilir kontrol sunmaz; ısıtıcı açık kalabilir.
- Web bildirimleri cihaz/işletim sisteminin iznine ve politikasına bağlıdır, tamamen sessiz olmayabilir.
- Kullanıcı denetimi olmadan sürekli/gece kullanımına geçmeden önce uzun süreli gerçek cihaz testleri, soğutma döngüsü, CO alarmı, egzoz ve havalandırma güvenliği zorunludur.
