# AstraL

**Discord sunucuları için Türkçe kayıt ve moderasyon botu.**

Kayıt başvurularını butonlu forma bağlar, başvuranın geçmişini yetkilinin önüne koyar, uyarıları sunucu bazlı numaralandırır, spamı bellekte yakalar ve baskınları davet koduyla hesap yaşını birleştirerek durdurur. Komutlar `/komut` olarak çalışır, çoğu `.komut` olarak da.

[**➕ Sunucuna ekle**](https://discord.com/oauth2/authorize?client_id=1457131021194625239&permissions=9896024468726&scope=bot+applications.commands) · [Gizlilik Politikası](GIZLILIK.md) · [Kullanım Şartları](SARTLAR.md)

---

## Ne yapar

### Kayıt sistemi

Üye karşılama mesajındaki butona basıyor, açılan formda nick / isim / yaş giriyor. Başvuru yetkili kanalına bir karar kartı olarak düşüyor ve kart başvuranın **tüm geçmişini** özetliyor: aktif uyarıları, yasaklamaları, susturmaları, daha önce reddedilmiş başvuruları. Sicili lekeliyse kart renk değiştiriyor.

Onay ve red tek tıkla. Red sebebi kullanıcıya özelden iletiliyor — neyi düzelteceğini bilmeden aynı başvuruyu tekrarlamasın diye.

24 saatten uzun bekleyen başvurular yetkilileri etiketleyerek kendini hatırlatıyor.

### Otomatik rol

Kayıt sistemi istemeyen sunucular için: katılan üyeye rolü bot veriyor. Üyelere ve botlara ayrı, birden fazla rol tanımlanabiliyor. Baskın kilidi aktifken rol dağıtımı kendiliğinden duruyor; hesap yaşı filtresi ve gecikme ile saldırganların rol toplaması zorlaşıyor. `otorol uygula` rolü mevcut üyelere de veriyor.

### Uyarı ve otomatik ceza

Uyarılar her sunucuda 1'den başlıyor. Eşik tanımlayıp ceza bağlayabilirsin — örneğin 3. uyarıda bir saat susturma. Uyarı silmek kaydı tablodan düşürmüyor, pasife alıyor: moderasyon geçmişi denetlenebilir kalıyor.

### Baskın koruması

Yalnızca "şu sürede şu kadar katılım" saymıyor. Davet kodunu ve hesap yaşını birleştirip sunucu paylaşımından gelen organik kalabalıkla tek koddan gelen taze hesapları ayırıyor.

Varsayılan tepki sunucuyu kilitlemek — doğrulama seviyesini yükseltip davetleri durdurmak. Atma ve yasaklama bilerek varsayılan değil: yanlış alarmda gerçek üyeler gider. Kilit kalıcı yazılıyor, yani bot yeniden başlasa bile sunucu yüksek doğrulamada unutulmuyor.

### Anti-spam

Mesaj seli, aynı mesajın tekrarı, toplu etiket ve büyük harf yağmuru. Spam mesajları toplu siliniyor, gönderen süreli susturuluyor; büyük harfte yalnızca mesaj siliniyor. Eşiklerin hepsi `/koruma spam` ile ayarlanıyor, yetkililer ve muaf rol etkilenmiyor. Tespit tamamen bellekte — mesaj başına veritabanı sorgusu yok, yoğun sunucuda botu yavaşlatmıyor.

### İçerik filtresi

Küfür ve bağlantı filtresi, alan adı beyaz listesi ve muaf rol desteğiyle. Düzenlenen mesajlar da denetleniyor: temiz mesaj atıp sonradan link eklemek filtreyi delmiyor.

### Discord AutoMod

`/automod kur` Discord'un yerleşik AutoMod kurallarını tek menüden kuruyor: küfür ve argo, Türkçe küfür, sunucu davetleri, dolandırıcılık kalıpları, şüpheli spam, toplu etiket ve küfürlü profil adları. AutoMod mesajı **gönderilmeden önce** engelliyor ve bot kapalıyken de çalışıyor; AstraL'in kendi filtresiyle birlikte katmanlı koruma oluyor. Kurallar AstraL ayarlarını izliyor (etiket sınırı, susturma süresi, muaf rol, uyarı kanalı), sunucuda başka botların ya da elle kurulmuş kurallara dokunulmuyor.

### Denetim kaydı

Mesaj silme ve düzenleme, takma ad ve rol değişimi, kanal ve rol işlemleri, ses hareketleri, yasaklamalar. Silinen mesajın görseli kayda gömülüyor, dosya adı ve boyutu ayrıca yazılıyor — Discord eki CDN'den kaldırdığında bile ne olduğu kayıtta kalıyor.

Denetim kaydı moderasyon logundan **ayrı kanalda** tutuluyor. Çok daha yoğun akıyor; karışırsa moderasyon logu okunamaz hale geliyor.

### Sicil

`sicil` komutu kişinin uyarılarını, moderasyon işlemlerini ve kayıt geçmişini tek kartta zaman sırasıyla birleştiriyor. Kim ne zaman ne yaptı, tek yerde.

### Sağ tık menüsü

Bir kullanıcıya sağ tıkla → **Uygulamalar** → *Sicili Göster* veya *Uyar*. Bir mesaja sağ tıkla → *Sil ve Uyar*: mesaj siliniyor, yazarı uyarılıyor ve silinen mesaj uyarı sebebine alıntılanıyor. Komut yazmaya, kimlik kopyalamaya gerek yok.

### Emoji ve çıkartma ekleme

Başka bir sunucunun emojisini beğendin mi? Emojinin geçtiği mesaja sağ tıkla → *Emoji ve Çıkartma Ekle*. Mesajda birden çok emoji varsa hangilerini alacağını seçersin; çıkartmalar da gelir. **Nitro gerekmez.** `/emoji ekle` emojinin bağlantısını ya da kimliğini de kabul eder, `/emoji yukle` kendi görselinden emoji yapar.

### Ayrıca

Hatırlatıcı (`/hatirlat 30dk toplantı` — özelden gelir) · ses kanalı taşıma (`/tasi`: bir kişiyi ya da kanaldaki herkesi) · rol butonları · süreli rol · davet takibi · mesaj ve ses istatistikleri · AFK · yetkili performans tablosu · snipe · toplu rol · kanal kilitleme ve yenileme

---

## Başlarken

**1. Botu ekle.** [Davet bağlantısı](https://discord.com/oauth2/authorize?client_id=1457131021194625239&permissions=9896024468726&scope=bot+applications.commands)

AstraL kurulumda **Yönetici yetkisi istemez** — yalnızca komutların gerçekten kullandığı izinleri talep eder.

**2. Botun rolünü yukarı taşı.** Sunucu Ayarları → Roller. Discord bir botun kendi rolünden yüksek bir role dokunmasına izin vermez; bildirilen sorunların çoğu bundan kaynaklanıyor.

**3. Kurulumu çalıştır.**

    /kurulum

Yetkili rolü, üye rolü, kayıtsız rolü ve kanalları tanımlar. Kayıt sistemi bunlar olmadan çalışmaz.

**4. İstediğin sistemleri aç.**

    /log ayarla          moderasyon ve denetim kanalları
    /kayitpanel gonder   butonlu kayıt paneli
    /antiraid ayarla     baskın koruması
    /koruma ayarla       küfür ve bağlantı filtresi

**5. Komutları keşfet.**

    /yardim              kategorilere ayrılmış liste
    /yardim uyar         tek bir komutun ayrıntısı

Liste senin yetkine göre süzülür: kullanamayacağın komutu görmezsin.

---

## Sık sorulanlar

**Bot rol veremiyor / isim değiştiremiyor.**
Botun rolü, yöneteceği rollerin üstünde olmalı. Sunucu Ayarları → Roller bölümünden AstraL'i yukarı taşı.

**Slash komutları görünmüyor.**
Yeni komutların Discord'a yayılması bir saati bulabilir. `CTRL+R` ile yenile. Prefix komutları (`.yardim`) hemen çalışır.

**Prefix nasıl değişir?**
`/prefix` — sunucuya özeldir, varsayılan nokta.

**Kayıt formu hangi bilgileri topluyor?**
Nick, isim ve yaş. Bunları yalnızca senin sunucunun kayıt yetkilileri görür. Kayıt sistemini açmak zorunda değilsin. Ayrıntı: [Gizlilik Politikası](GIZLILIK.md).

**Verilerimi sildirebilir miyim?**
Evet. Sunucundaki bir yetkiliden kaydını silmesini iste, ya da bize ulaş. Haklarının tamamı gizlilik politikasında yazılı.

**Bot çevrimdışı.**
Destek sunucusundaki duyurulara bak. Bilinen bir kesinti yoksa bildir.

---

## Destek ve bildirim

- **Hata bildirimi ve özellik önerisi** → bu deponun [Issues](../../issues) sekmesi
- **Soru ve yardım** → destek sunucusu *(bağlantı yakında)*
- **Güvenlik açığı** → public issue **açma**, doğrudan iletişime geç

Hata bildirirken hangi komutu çalıştırdığını, ne beklediğini ve ne olduğunu yaz. Sunucu kimliği ve yaklaşık saat de yardımcı olur.

---

## Kaynak kod

AstraL **kapalı kaynaktır**. Bu depo botun belgelerini, politikalarını ve hata takibini barındırır; kod ayrı ve özel bir depoda geliştirilir.

© 2026 ArdayraL. Tüm hakları saklıdır.
