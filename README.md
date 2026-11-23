# ELK Log Viewer

Kibana'daki logları Seq tarzında aramak için küçük bir görüntüleyici. Kibana sekmesindeyken yer imlerindeki **Logs** düğmesine tıklarsın, sayfanın üstünde açılır.

*A small Seq-style log viewer for Kibana. It runs as a bookmarklet on top of the Kibana tab you already have open. The interface is in Turkish and English.*

## Kurulum

1. [`elk-log-viewer.html`](elk-log-viewer.html) dosyasını indir ve Chrome'da aç. İstersen [tarayıcıda da açabilirsin](https://milvasoft.github.io/elk-viewer/elk-log-viewer.html).
2. Kibana adresini yaz (ör. `https://kibana.sirket.local/app/discover`). Adres bu bilgisayarda hatırlanır.
3. **Logs** ve **Kibana** düğmelerini yer imleri çubuğuna sürükle. Çubuk görünmüyorsa `Ctrl` + `Shift` + `B`. Sürükleme olmazsa "Yer imi kodunu kopyala" ile elle yer imi oluştur.
4. Kibana'nın herhangi bir sayfasındayken **Logs**'a tıkla. Sağ üstteki × ile Kibana'ya dönersin.

Kibana'da Dev Tools açılabiliyor ve `GET _cat/indices` çalışıyorsa yetkin yeterli. Elasticsearch 8.9 ve 8.15 ile denendi.

## Neler yapabiliyor

- **Seq tarzı sorgular:** `Level = 'Error'`, `StatusCode >= 500`, `RequestPath like '%/orders%'`, `has(Exception)`, `not`, `and`, `or`. Konsoldan kopyaladığın bir log satırını olduğu gibi yapıştırıp arayabilirsin.
- **Zaman:** hazır aralıklar ya da serbest yazım (`15 dk`, `dün`, `10:00 - 11:30`, `18.11 09:00 - 19.11 18:00`), takvim ve histogramda sürükleyerek daraltma.
- **Canlı takip:** yeni loglar akarak gelir.
- **Bu türü hariç tut / Sadece bu tür:** Serilog mesaj şablonuna göre gürültüyü tek tıkla temizler.
- Bir alanın en sık değerleri, değere tıklayınca filtre, bir kaydın ±1 dakika etrafındaki loglar, kayıtlı aramalar, favori kaynaklar, koyu/açık tema.

## Güvenlik

- **Sadece okur.** Yalnızca arama ve alan sorguları yapar, yazma ya da silme isteği yoktur.
- **Kimlik bilgisi saklamaz.** Tarayıcıdaki Kibana oturumunu kullanır, şifre ya da API key istemez. Kibana'daki yetkinin dışına çıkamaz.
- **Dışarıya veri göndermez.** Tek ağ isteği açık olan Kibana adresine gider (Kibana Dev Tools'un kullandığı `/api/console/proxy`). Analitik, telemetri ya da CDN yoktur.
- **Log içeriği düz metin olarak basılır.** Loglara zararlı bir içerik yazılsa bile kod olarak çalışmaz.
- **Kurulum yok.** Sunucu, uzantı ya da yönetici izni gerekmez. Arama geçmişi ve kayıtlı aramalar yalnızca senin tarayıcında durur, Ayarlar'dan kapatılıp silinebilir.

Yer imi Kibana oturumunda kod çalıştırdığı için dosyayı yalnızca bu depodan al.

## Sınırlar

- Elasticsearch metni kelimelere bölerek indexler. Kelimenin ortasından bir parçayı aramak için `message like '%rderId%'` kullan.
- Point-in-time desteklemeyen eski sürümlerde (7.10 öncesi) en fazla 10.000 kayıt kaydırılabilir.
