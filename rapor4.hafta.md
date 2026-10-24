1. NTFS vs ext4 vs APFS Farkları

   Her işletim sistemi, verileri disk üzerinde düzenlemek için kendine özgü bir dosya sistemi (File System) kullanır.
   NTFS (New Technology File System - Windows):
   Kullanım Alanı: Windows işletim sistemlerinin standart dosya sistemidir.
   Özellikleri: Günlükleme (journaling) özelliği sayesinde ani elektrik kesintilerinde veri bütünlüğünü korur. Gelişmiş güvenlik izinleri (ACL) ve büyük dosya/bölüm desteği sunar.
   Dezavantajı: macOS üzerinde varsayılan olarak salt okunurdur (ek yazılımlar olmadan yazma yapılamaz).
   ext4 (Fourth Extended Filesystem - Linux):
   Kullanım Alanı: Linux tabanlı sistemlerin varsayılan ve en popüler dosya sistemidir.
   Özellikleri: "Extent" adı verilen yapıları kullanarak büyük dosyaları ardışık bloklar halinde saklar, bu da dosya bölünmesini (fragmentation) azaltır. Çok yüksek performans ve kararlılık sunar.
   Dezavantajı: Windows tarafından doğrudan okunamaz (özel sürücüler gerekir).
   APFS (Apple File System - macOS / iOS):
   Kullanım Alanı: Apple cihazlarının modern, flash depolama odaklı dosya sistemidir.
   Özellikleri: Özellikle SSD'ler için tasarlanmıştır. "Copy-on-Write" (Yazma anında kopyalama) mantığıyla çalışır; bu sayede anlık kopyalama (cloning) ve anlık yedekleme (snapshot) işlemleri anında gerçekleşir. Güçlü yerleşik şifreleme desteği vardır.

2. Blok Yapısı Nedir?

   Dosya sistemleri, sabit diskin ham alanını yönetebilmek için onu mantıksal parçalara ayırır. Bu en küçük mantıksal birime blok (Windows terminolojisinde küme/cluster) denir.
   Nasıl Çalışır? Diskler bayt bayt veri yazmak yerine bloklar halinde yazar. Örneğin, bir blok boyutu 4 KB ise, 1 KB'lık bir dosya kaydettiğinizde bile o bloğun tamamı (4 KB) o dosyaya tahsis edilir (geri kalan alan boş kalır ama başka dosya yazayamaz).
   Parçalanma (Fragmentation): Dosyalar büyüdükçe veya silindikçe bloklar diske dağılabilir. HDD'lerde kafanın hareket etmesine neden olarak yavaşlamaya yol açar; ancak modern dosya sistemleri (ext4 ve APFS gibi) bunu minimize eder.

3. HDD vs SSD Çalışma Prensipleri

   Depolama dünyasının iki ana donanım mimarisi, veriyi saklama ve okuma biçimleriyle birbirlerinden ayrılır:
   HDD (Hard Disk Drive - Sabit Disk):
   Çalışma Prensibi: Mekanik bir yapıya sahiptir. İçinde hızla dönen manyetik disk plakaları ve bu plakalar üzerinde hareket eden bir okuma/yazma kafası bulunur (eski gramofonlara benzer).
   Hız Sınırı: Veriye erişmek için kafanın doğru sektöre gitmesi (seek time) ve plakanın dönmesi (rotational latency) gerekir. Bu mekanik hareket fiziksel bir zaman maliyeti yaratır.
   SSD (Solid State Drive - Katı Hal Sürücüsü):
   Çalışma Prensibi: Tamamen elektronik, hareketli parça içermeyen bir yapıya sahiptir. NAND Flash bellek hücreleri ve bir kontrolcü (controller) barındırır. Elektrik sinyalleriyle doğrudan veriye anında erişir.
   Hız Sınırı: Mekanik gecikme olmadığı için rastgele okuma/yazma hızları HDD'lere göre yüzlerce kat daha fazladır.

4. Kazanç: Veri Okuma/Yazma Hızları Nereden Geliyor?

   Bu mekanizmaları bildiğinizde, bir bilgisayarın neden yavaş veya hızlı çalıştığını doğrudan anlamış olursunuz:
   Fiziksel vs. Elektronik: HDD'lerde hız, motorun devir hızına (örn. 7200 RPM) ve kafanın mekanik çevikliğine bağlıdır. SSD'lerde ise hız, bellek yongalarının mimarisine ve veri yollarının (SATA yerine NVMe/PCIe gibi) bant genişliğine bağlıdır.
   Dosya Sistemi Optimizasyonu: APFS ve ext4 gibi modern dosya sistemleri, SSD'lerin paralel çalışma yapısına ve flash bellek özelliklerine uyum sağlayarak veriyi en az gecikmeyle kontrolcüye iletir.
   Rastgele Erişim (Random Access): Dağınık haldeki binlerce küçük dosyayı okurken (örneğin işletim sistemi açılırken), mekanik HDD kafası disk üstünde sürekli gezinmek zorunda kalırken, SSD tüm bu noktalara aynı anda, milisaniyeden kısa sürede ulaşır. Hız farkının temel kaynağı budur.