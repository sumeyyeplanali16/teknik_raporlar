1. Temel Kavramlar (IP, Port, DNS, TCP, UDP)

  IP (Internet Protocol): Ağ üzerindeki her cihazın (bilgisayar, telefon, sunucu vb.) birbirini bulabilmesini sağlayan benzersiz kimlik numaramızdır (Örn: 192.168.1.1 veya 172.217.169.206).
  Port: Bir bilgisayar üzerindeki farklı uygulamaların veya servislerin dış dünya ile iletişim kurduğu sanal kapılardır (0 - 65535 arası). Örneğin, web trafiği genellikle 80 (HTTP) veya 443 (HTTPS) numaralı portları kullanır.
  DNS (Domain Name System): İnsanların hatırlaması zor olan IP adreslerini (142.250.190.46), tarayıcılara yazdığımız okunabilir alan adlarına (google.com) çeviren internet rehberidir.
  TCP (Transmission Control Protocol): Veri gönderiminden önce taraflar arasında bağlantı kuran (Three-way Handshake), verinin eksiksiz ve sırasıyla iletilmesini garantileyen güvenli ve yavaş protokoldür. (Örn: Web sayfaları, e-postalar, dosya transferleri).
  UDP (User Datagram Protocol): Bağlantı kurmadan doğrudan veri gönderen, paket kaybını umursamayan ancak çok hızlı olan protokoldür. (Örn: Canlı video/ses yayınları, çevrimiçi oyunlar).

2. Paket Yapısı Nasıl Çalışır?
  İnternet üzerinden gönderilen büyük veriler (resimler, mesajlar, videolar) doğrudan bir seferde gönderilmez; paketlere (packet) bölünür.

  Paketin Bileşenleri:
  Başlık (Header): Gönderenin IP adresi, alıcının IP adresi, port numaraları, paket sırası (sequence number) ve hata kontrol (checksum) bilgilerini içerir.
  Gövde (Payload): Taşınan gerçek verinin parçasıdır.
  Çalışma Prensibi:
  Kaynak cihaz veriyi küçük paketlere böler ve her birine başlık bilgisi ekler.
  Paketler ağ üzerindeki yönlendiriciler (routers) aracılığıyla farklı yollardan hedef cihaza doğru hareket eder.
  Hedef cihaza varan paketler, başlıklarındaki sıra numaralarına bakılarak yeniden birleştirilir ve eksik paket varsa TCP ile tekrar istenir.

3. Temel Ağ Araçları (Ping, Traceroute, Nslookup)

  Ağ sorunlarını gidermek ve bağlantıyı test etmek için sıkça kullanılan komut satırı araçlarıdır:
  Ping: Hedef bir sunucuya veya cihaza küçük veri paketleri (ICMP) göndererek erişilebilir olup olmadığını ve paketlerin gidip gelme süresini (latency / ping süresi) milisaniye cinsinden ölçer.
  Traceroute (Tracert): Bir paketin kaynaktan hedefe ulaşana kadar hangi yönlendiricilerden (router/hop) geçtiğini ve her bir adımdaki gecikme sürelerini gösteren haritalama aracıdır. Ağ tıkanıklıklarını bulmak için idealdir.
  Nslookup: DNS sorguları yaparak bir alan adının hangi IP adresine karşılık geldiğini (veya tersini) öğrenmenizi sağlar. DNS sorunlarını çözmek için kullanılır.