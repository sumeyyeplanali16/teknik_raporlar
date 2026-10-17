İşletim Sistemi Temelleri (OS Basics)

    Yazılım dünyasında geliştirilen uygulamaların ve yazılan kodların donanım kaynaklarıyla nasıl etkileşime girdiğini anlamak için işletim sisteminin (OS) temel bileşenlerini bilmek kritik önem taşır. Bu rapor; çekirdek (kernel), süreç ve iş parçacığı kavramları, bellek yönetimi ve CPU zamanlayıcıları konularını kapsayarak yazılımın "nerede çalıştığını" derinlemesine ele almaktadır.

1. Kernel (Çekirdek) Nedir?
    Çekirdek, işletim sisteminin kalbidir ve donanım ile yazılım arasındaki köprü görevi görür. Donanım kaynaklarına (CPU, bellek, disk, çevre birimleri) doğrudan erişim yetkisine sahip olan en temel yazılım katmanıdır.
    Yetki Seviyeleri (Modlar):
    Kernel Mode (Yetkili Mod / Supervisor Mode): Tüm donanım kaynaklarına ve bellek bölgelerine sınırsız erişim sağlar. İşletim sistemi çekirdeği burada çalışır.
    User Mode (Kullanıcı Modu): Kullanıcı uygulamalarının çalıştığı kısıtlı moddur. Donanıma doğrudan erişemezler; sistem çağrıları (system call) aracılığıyla çekirdekten yardım isterler.
    Çekirdek Mimarileri:
    Monolitik Çekirdek (Monolithic Kernel): Dosya sistemi, sürücüler ve ağ yönetimi gibi tüm temel servisler çekirdek alanında (kernel space) tek bir büyük parça olarak çalışır (örn. Linux). Performansları yüksektir ancak bir hata tüm sistemi çökertebilir.
    Mikroçekirdek (Microkernel): Çekirdek olabildiğince küçük tutulur (sadece süreç ve bellek yönetimi). Sürücüler ve servisler kullanıcı alanında (user space) ayrı süreçler olarak çalışır (örn. Minix, seL4). Daha güvenlidir ancak servisler arası iletişim maliyeti (IPC) nedeniyle biraz daha yavaş olabilir.


2. Süreç (Process) ve İş Parçacığı (Thread) Farkı
    Süreç (Process): Kendi bağımsız bellek alanına sahip, yürütülmekte olan bir program örneğidir. Süreçler arası geçiş ve iletişim maliyetlidir, ancak birinin çökmesi diğerlerini etkilemez (güçlü izolasyon).
    İş Parçacığı (Thread): Bir sürecin içinde çalışan alt yürütme birimidir ("hafif süreç"). Aynı sürece ait thread'ler bellek alanını (kod ve veriyi) ortaklaşa paylaşır; bu sayede iletişim çok hızlıdır ancak birinin yapacağı bellek hatası tüm sürecin sonlanmasına yol açabilir.

3. Bellek Yönetimi Nasıl Yapılır?
    İşletim sistemi, fiziksel RAM'i birden fazla uygulama arasında güvenli, verimli ve adil bir şekilde paylaştırmakla sorumludur.
    Sanal Bellek (Virtual Memory): Fiziksel RAM ile disk alanı (swap alanı) birleştirilerek uygulamalara olduğundan çok daha büyük, sürekli bir adres alanı sunulur. Her sürecin kendine ait sanal adres uzayı vardır.
    Sayfalama (Paging): Bellek sabit boyutlu küçük bloklara (sayfalar / pages, örn. 4KB) bölünür. Fiziksel bellek de aynı boyutta çerçevelere (frames) ayrılır. Sayfa tablosu (Page Table) yardımıyla sanal adresler fiziksel adreslere dönüştürülür.
    TLB (Translation Lookaside Buffer): Sayfa tablosu aramalarını hızlandırmak için CPU içinde bulunan yüksek hızlı özel bir önbellektir.
    SWAP Alanı: Fiziksel RAM dolduğunda, aktif olarak kullanılmayan bellek sayfalarının geçici olarak diske taşındığı alandır.

4. CPU Zamanlayıcıları (CPU Schedulers) Nedir?
    Tek veya çok çekirdekli bir işlemcide, aynı anda çalışmak isteyen onlarca süreç/iş parçacığı vardır. CPU zamanlayıcı, hangi sürecin ne kadar süreyle işlemciyi kullanacağını belirleyen algoritmalardır.
    Zamanlayıcı Türleri:
    Long-term Scheduler (Job Scheduler): Yeni başlayan programları diskten alarak hazır kuyruğuna (ready queue) yerleştirir.
    Short-term Scheduler (CPU Scheduler): Hazır kuyruğundaki süreçlerden birini seçerek CPU'ya atar (çok sık çalışır, milisaniyeler düzeyinde).
    Medium-term Scheduler: Bellek yönetimi amacıyla bazı süreçleri geçici olarak diske (swap out) taşır ve gerektiğinde geri getirir (swap in).
    Temel Algoritmalar:
    FCFS (First-Come, First-Served): Gelen ilk süreç önce çalışır. (Convoy etkisi görülebilir).
    SJF (Shortest Job First): CPU süresi en kısa olan süreç önce çalıştırılır.
    Round Robin (RR): Her sürece eşit zaman dilimi (quantum, örn. 10ms) verilir; süre bitince sıradakine geçilir. Modern işletim sistemlerinde yaygındır.
    Priority Scheduling: Önceliği yüksek olan süreçler önce çalıştırılır.