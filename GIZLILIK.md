# AstraL — Gizlilik Politikası

**Son güncelleme:** 26 Eylül 2026

AstraL, Discord sunucuları için geliştirilmiş bir kayıt ve moderasyon botudur. Bu belge, botun hangi verileri neden işlediğini, ne kadar sakladığını ve bu veriler üzerinde hangi haklara sahip olduğunuzu açıklar.

Belge, 6698 sayılı Kişisel Verilerin Korunması Kanunu (KVKK) ve Avrupa Birliği Genel Veri Koruma Tüzüğü (GDPR) çerçevesinde hazırlanmıştır.

---

## 1. Veri sorumlusu

AstraL'i işleten geliştiricidir. İletişim: Bu deponun [Issues](../../issues) sekmesinden ulaşabilirsin. Kişisel veri talepleri için destek sunucusu da kullanılabilir *(bağlantı yakında)*.

Botu sunucusuna ekleyen sunucu yöneticileri, kendi sunucularında toplanan veriler bakımından **birlikte veri sorumlusu** konumundadır: hangi özelliklerin açık olacağına, hangi kanalların loglanacağına ve kayıt formunun kullanılıp kullanılmayacağına onlar karar verir.

---

## 2. Toplanan veriler

Bot yalnızca çalışması için gereken veriyi saklar. Aşağıdaki liste **eksiksizdir** ve doğrudan veritabanı şemasından çıkarılmıştır.

### 2.1 Kimlik verileri

| Veri | Nerede | Neden |
|---|---|---|
| Discord kullanıcı kimliği (ID) | Neredeyse tüm kayıtlarda | Kayıtları kişiyle eşleştirmek |
| Discord sunucu ve kanal kimlikleri | Ayarlar, loglar | Ayarları doğru sunucuya uygulamak |
| **Gerçek ad** | Kayıt başvurusu | Yalnızca sunucu yöneticisi kayıt formunu açtıysa toplanır |
| **Yaş** | Kayıt başvurusu ve kayıt kaydı | Yaş sınırı olan sunucularda doğrulama |
| Takma ad (nick) | Kayıt başvurusu ve kayıt kaydı | Sunucudaki görünen ismi ayarlamak |

> **Gerçek ad ve yaş özel önemdedir.** Bu iki alan yalnızca sunucu yöneticisinin kayıt sistemini etkinleştirdiği sunucularda, yalnızca kişinin formu **kendi isteğiyle doldurması** üzerine toplanır. Form doldurulmadan bu veriler hiçbir şekilde elde edilmez.

### 2.2 Moderasyon verileri

- Uyarılar: sebep metni, uyarıyı veren yetkilinin kimliği, tarih, aktif/pasif durumu. Uyarı sağ tık menüsündeki *Sil ve Uyar* ile verildiyse sebep metni **silinen mesajdan kısa bir alıntı** da içerir (bkz. 2.4)
- Moderasyon işlemleri: yasaklama, atma, susturma, susturma kaldırma, kayıt, kayıt silme — işlem türü, sebep, süre, yetkili kimliği, tarih
- AutoMod yakalamaları: Discord'un kendi AutoMod özelliği bir mesajınızı engellediğinde moderasyon geçmişinize **kuralın adı ve uygulanan eylem** yazılır (örnek: `AutoMod: Türkçe küfür · mesaj engellendi`). Engellenen mesajın içeriği ve kurala takılan kelime **saklanmaz** (bkz. 2.4)
- Kayıt başvuruları: başvuru durumu, kararı veren yetkili, red sebebi, karar tarihi

### 2.3 Etkinlik verileri

- Sunucu bazlı mesaj sayısı ve sesli kanalda geçirilen toplam süre (**mesaj içeriği değil, yalnızca sayaç**)
- Son mesaj tarihi
- AFK durumu ve kişinin kendi yazdığı AFK sebebi
- Davet takibi: kimin hangi davet koduyla geldiği ve sunucudan ayrılıp ayrılmadığı
- Hatırlatmalar: `/hatirlat` ile **kendin kurduğun** hatırlatmanın metni, zamanı ve kurulduğu kanal. Hatırlatma zamanı gelip **gönderildiği anda silinir**. Hatırlatma yalnızca özel mesajla gönderilir; özel mesajların kapalıysa kurduğun kanalda yalnızca etiketlenirsin, **metin kanala yazılmaz**

### 2.4 Mesaj içeriği

Bot, mesaj içeriğini **okur** ama kural olarak **saklamaz**. İçerik yalnızca şu anlarda işlenir:

1. **Komut çalıştırmak için** — mesaj bir komutla başlıyorsa ya da bir mesaja sağ tık menüsünden bir komut uygulandıysa (örneğin *Emoji ve Çıkartma Ekle*, mesajdaki emojileri bulmak için içeriği okur). İşlem bitince içerik atılır.
2. **Küfür ve bağlantı filtresi için** — yalnızca sunucu yöneticisi filtreyi açtıysa. Kontrol bellekte yapılır, sonuç veritabanına yazılmaz.
3. **Spam koruması için** — yalnızca sunucu yöneticisi açtıysa. Mesaj selini ve aynı mesajın tekrarını yakalamak için kişinin son mesajlarının **içeriği, gönderim zamanı ve etiket sayısı yalnızca bellekte, en fazla 2 dakika** tutulur. Spam tespit edildiğinde bu kayıtlar hemen atılır; hiçbir zaman diske yazılmaz. Spam sonucu uygulanan susturma, diğer moderasyon işlemleri gibi kaydedilir (bkz. 2.2) — mesaj içeriği bu kayda girmez.
4. **Silinen mesajı geri gösterme (`snipe`) için** — silinen son mesajlar **yalnızca bellekte, en fazla 2 saat** tutulur ve yalnızca "Mesajları Yönet" yetkisi olanlar görebilir. Bot yeniden başladığında bu veri tamamen kaybolur, hiçbir zaman diske yazılmaz.
5. **Denetim kaydı için** — yalnızca sunucu yöneticisi denetim kanalını ayarladıysa, silinen ve düzenlenen mesajlar o sunucunun **kendi Discord kanalına** yazılır. Bu kayıt botun veritabanında değil, sunucunun kendi kanalında durur ve sunucu yöneticisinin denetimindedir.
6. **"Sil ve Uyar" için — kalıcı saklamanın tek istisnası.** Bir yetkili bir mesajı sağ tık menüsünden silip yazarını uyardığında, neden uyarıldığının sonradan anlaşılabilmesi için silinen mesajdan **kısa bir alıntı uyarı sebebine eklenir** ve uyarı kaydıyla birlikte saklanır. Alıntıyı kişinin kendisi ve o sunucunun yetkilileri görebilir; uyarı silme talebiyle birlikte silinir.
7. **Discord AutoMod yakalamaları için** — yalnızca sunucuda AutoMod kuralı kuruluysa. Kuralı **Discord uygular**, mesajı Discord engeller; bot yalnızca "engellendi" bildirimini alır. Bu bildirim engellenen mesajın tam metnini ve kurala takılan kelimeyi içerir, ancak bot bunların **hiçbirini saklamaz** — moderasyon geçmişine yalnızca kuralın adı ve uygulanan eylem yazılır (bkz. 2.2). Aynı kişi aynı kurala arka arkaya takılırsa **60 saniye içindeki tekrarlar kaydedilmez**.

### 2.5 Toplanmayan veriler

Bot şunları **hiçbir koşulda** toplamaz, saklamaz veya talep etmez: e-posta adresi, telefon numarası, şifre, ödeme bilgisi, IP adresi, konum, Discord hesabınıza ait erişim anahtarları ve özel mesajlarınızın (DM) içeriği.

---

## 3. İşleme amacı ve hukuki dayanak

| Amaç | Dayanak |
|---|---|
| Komutları çalıştırmak, botun temel işlevini sunmak | Sözleşmenin ifası (KVKK m.5/2-c, GDPR m.6/1-b) |
| Kayıt sistemi: ad, yaş, takma ad | **Açık rıza** — kişi formu kendi isteğiyle doldurur (KVKK m.5/1, GDPR m.6/1-a) |
| Moderasyon kaydı, uyarılar, baskın koruması, AutoMod yakalamaları | Meşru menfaat — sunucu güvenliğinin sağlanması (KVKK m.5/2-f, GDPR m.6/1-f) |
| Etkinlik sayaçları, davet takibi | Meşru menfaat — sunucu yönetimi. Sunucu yöneticisi kapatabilir |
| Hatırlatmalar | Sözleşmenin ifası — kişi kendisi kurar ve istediği an iptal edebilir |

---

## 4. Saklama süresi ve silme

| Veri | Süre |
|---|---|
| Spam koruması için son mesajlar | **En fazla 2 dakika**, yalnızca bellekte |
| Silinen mesaj içeriği (`snipe`) | **2 saat**, yalnızca bellekte |
| Kayıt, uyarı, moderasyon ve başvuru kayıtları | Bot sunucudan çıkarılana veya silme talebi gelene kadar |
| Etkinlik sayaçları, davet kayıtları | Aynı |
| Hatırlatmalar | **Gönderildiği anda silinir**; en uzun 1 yıl ileriye kurulabilir. `/hatirlat sil` ile istediğin an iptal edebilirsin |
| Sunucu ayarları | Bot sunucudan çıkarıldığında geçerliliğini yitirir |
| Veritabanı yedekleri | Son 14 günün günlük yedekleri, öncesinde haftada bir yedek olmak üzere **en fazla 10 hafta** |

**Uyarı silindiğinde kayıt tablodan düşürülmez, "pasif" olarak işaretlenir.** Bu, moderasyon kararlarının sonradan denetlenebilmesi içindir; talep üzerine tamamen silinir.

**Yedekler hakkında.** Veri kaybını önlemek için veritabanının günlük yedeği alınır. Bir kayıt silindiğinde canlı veritabanından hemen kaldırılır, ancak silinmeden önce alınmış yedeklerde **yukarıdaki süre dolana kadar** kalır ve süre dolunca yedekle birlikte kendiliğinden yok edilir. Yedekler yalnızca bir arıza sonrası veriyi geri getirmek için kullanılır, başka hiçbir amaçla okunmaz. Bir yedekten geri yükleme yapılırsa, önceden gelmiş silme talepleri yeniden uygulanır.

---

## 5. Verilerin paylaşımı

**Veriler hiçbir üçüncü tarafa satılmaz, kiralanmaz veya pazarlama amacıyla aktarılmaz.** Bot dış analiz, reklam veya izleme servisi kullanmaz.

Veriler yalnızca şu şekilde görünür hale gelir:

- **Sunucu yetkilileri**, kendi sunucularındaki kayıtları bot komutlarıyla görebilir (örneğin `sicil`, `uyarilar`). Kendi geçmişini herkes görebilir; başkasınınkini görmek yetki gerektirir.
- **Discord**, botun çalışması için zorunlu altyapı sağlayıcısıdır ve kendi gizlilik politikasına tabidir.

Veriler, botun çalıştığı sunucu üzerinde tutulur ve sunucular arasında paylaşılmaz: bir sunucudaki uyarı veya kayıt geçmişi başka bir sunucudan görülemez.

---

## 6. Haklarınız

KVKK m.11 ve GDPR m.15–22 uyarınca:

- Hakkınızda veri işlenip işlenmediğini **öğrenme** ve bir **kopyasını isteme**
- Yanlış veya eksik verinin **düzeltilmesini** isteme
- Verilerinizin **silinmesini** isteme
- İşlemeye **itiraz etme** ve verdiğiniz **rızayı geri çekme**

Bu haklarınızı kullanmak için yukarıdaki iletişim adresinden ulaşabilirsiniz. Talepler **en geç 30 gün** içinde sonuçlandırılır. Kimlik doğrulaması için Discord kullanıcı kimliğinizi belirtmeniz istenir.

**Rızanızı geri çekmenin en hızlı yolu:** sunucu yetkilisinden kaydınızın silinmesini istemek. Bu, kayıt kaydınızı ve başvurunuzu veritabanından kaldırır.

---

## 7. Çocukların verileri

Discord'un kendi kullanım şartları **13 yaşın altındaki** kişilerin platformu kullanmasını yasaklar. AstraL bilerek 13 yaşın altındaki kişilerden veri toplamaz.

Kayıt formu yaş sorar. 13 yaşın altında olduğu anlaşılan bir kişiye ait veri tespit edilirse **derhal silinir** ve durum sunucu yöneticisine bildirilir. Böyle bir durumu fark ederseniz lütfen iletişime geçin.

---

## 8. Güvenlik

Veriler ve yedekleri botun çalıştığı sunucuda tutulur ve yalnızca botun kendisi tarafından erişilir. Her yedek alındığında bütünlüğü doğrulanır. Bot, kurulumda **Yönetici yetkisi istemez**; yalnızca çalışması için gereken izinleri talep eder.

Yine de hiçbir sistem mutlak güvenlik sunmaz. Bir güvenlik açığı fark ederseniz kamuya açık şekilde paylaşmadan önce iletişime geçmenizi rica ederiz.

---

## 9. Değişiklikler

Bu politika değiştiğinde üstteki tarih güncellenir. Önemli bir değişiklik olması hâlinde duyuru yapılır. Bu belgenin tüm değişiklik geçmişi bu deponun commit geçmişinde açıkça izlenebilir.
