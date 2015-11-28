# Pasif Bilgi Toplama

Kısaca hedef sisteme dogrudan bir erisim yada tarama olamaz peki pasif olarak nasıl bilgi toplarıza bakalım

- 1.Kali Linux komut satırında whois komutunu kullarak guvenlik testi yapabiliriz whois ile hedef sistem hakkında gerekli bilgilere erisebiliriz. ornegin whois google.com deyip enter tusuna basıldıgında sonuclari gozlemleyebiliriz.

- 2.Hedef sistemin sunucusunun IP sini ogrenmek icin en basit kullanılabilecek komut "ping" komutudur. Ornegin ping google.com deyip entera basarsak sonuclari gozlemleriz ctrl+c tusu islemi keser.

- 3.Hedef sistem hakkında bilgi edinmek icin sitelerde vardır. google arama motoruna https://www.robtex.com/ den hedef domaini yazayarak arama yapabiliriz. Ayrıca IP adresini isaret eden domainleride https://www.robtex.com/ip/().html#graph parantezler olmadan icinde IP adresi yazıp sonuc alabiliriz.

- 4.Bing arama motorunu kullanarak da bazı bilgiler elde edebiliriz. Arama yerine IP adresini yazıp aratınca bu alan adına ait web siteleri burdan goruntuleyebilirz. OrneGin ip 173.194.112.228 deyip aratInca sonucları gozlemleriz.

- 5.Kali Linux da komut satırında thehorvester komutunu kullanılarak hedef domaine ait emaillerin public olmuslarını buluruz. ornegin thehorvester -d google.com -l 100 -b all bu alana ait  email adreslerini, virtual hostları, alan adi kayitlarini gosterir bu sayı degeri limitini arttirabilirsiniz.

- 6.Kali Linux da metasploit aracini kullanarakda hedef domaine sahip olan emailleri bulabiliriz. Bunun icin kali ye metasploiti cagiracagiz.

> msfconsole komutu ile cagiriyoruz

> use auxiliary/gather/search_email_collector yazip enter deyip bu module gectikten sonra 

> show options diyoruz ve kullanabilecegimiz parametreler gozukur biz domaine ait arama yapacagımızdan set DOMAIN google.com deyip enter diyoruz exploit komutunu kullaniyoruz bizim yerimize bu alan adina ait emailleri bulmaya calışır.

- 7.archieve.org/web adresini de kullanarak hedef domainin ile ilgili bilgileri ulabiliriz snapshot durumunu goruntuleyebiliriz.

- 8.netcraft.com hedef domaine ait acıga cıkmıs yani herkes tarafından bilinen e-posta adresleri bulunabilir.

- 9.pipl.com istedigimiz herhangi bir kisiye ait bilgileri burdan bulabiliriz.

- 10.foundstone sitedigger google hacking programini kullanabiliriz. http://www.mcafee.com/us/dowloads/free-l/tools/vitedigger.aspx indirerek hedef domain ile ilgili acıkları bulmaya calısırız.


Peki buraya kadar hep bir arac kullandik simdi manuel olarak google hacking nasil yapilir buna bakalim

## MANUEL HACKING

site:*.google.com bu sekilde google un gecmisinde arayabiliriz.

link:linux.com icerisinde linux.com barından sitelerini bulabilirz.

site:google.com inurl:page.php?intPageID= gibi sayfalar bulunursa bunlar sql injection acıgı bulunabilecek sayfaları gosterir.

site:google.com inurl:?id= daha genel aramadır cunku ingilizce ve turkce olmasına gore degisebilir.

intext:kullanici sifre site: google.com hedef sistemin text kısmında arama yapılır.

allintext:sifre site:*google.com

inurl:admin site:google.com

filetype:xls"sifre" site:edu.tr icinde sifre gecen exel dosyalarını gosterir.

filetype:xls"kullanici|sifre" site:google.com

intitle:index.of site:google.com dizin listelemeye izin veren yerleri goruntuler

intitle:index.of ws_ftp.log site:.edu.tr daha ayrintili bicimde hem indexde acik ve bu indexde acik olan yerleri vsftpd loglari acik olan siteleri buluruz.

intitle:index.of inurl:"/admin/" admin dizini listelenebilir olan siteleri gosterir.

powered by phpBB "inurl: "index.php?s" OR inurl: "index.php?style" phpBB kullanan ve acik bulunan siteleri aratabilirz.

intitle:index.of "Microsoft-IIS/5.0 server at"

Bunlari google arama motorunda yazip taratabilirsiniz.

## SUBDOMAINLOOKUP SCRPITI

Kulaniminda hedef domaine ait sub domain aratabiliriz. Bunun icin su adimlari takip edebilirz.
-Kali Linux komut satirini aciyoruz icine vim komutunu kullarak subdomainlookup.py sayfasini olusturuyoruz 
vim subdomainlookup.py yazip enter tusuna basiyoruz ve bu dosyanin icine https://dl.dropboxusercontent.com/u/3364236/tools/subdomainlookup.py yazip aratiyoruz google da e cikan icerigi kopyalayip kali linux da actigimiz sayfanin icine yapistiriyoruz simdi vim den biraz bahsedeyim icerige birsey yazmak icin insert anlamina gelen i tusuna basiyoruz insert ten cikmak icin esc tusuna basiyoruz burdan cikmak icin :q! yazip cikiyoruz icerigi kaydedip cikmak icin :wq yazip cikiyoruz simdi adimlara donelim
-2.adim olan icerigi yapistiriyoruz ve esc tusuna basiyoruz
-:wq deiyoruz kaydedip cikiyoruz
-chmod u+x subdomainlookup.py deyip enter bu dosya ve domainlerin izin bilgilerini degistirmek icin kullanilir aktif ettik x->calisitir anlaminda u-> user anlaminda
ve simdi 
-python subdomainlookup.py google.com enter bu isme ait domainleri vs goroyoruz.

## SHODAN

Tarayicisi kullanmadan bahsediyim kendinize ait bir hesap acabilirsiniz bu tarayiciya google uzerinde arattigimizda ulasabilirsiniz. arama yerine 
apache country:TR
nginx country:TR
iis country :TR  yazip arattiginizda tek tek bu sunuculara ait domainleri bulunur. Ornegin apache hostname:.google.com gibi..

kendi belirledigimiz bir network de aratabiliriz nasil yapilir bakalim adim adim
-ilk once ping atip sistenin IP sini ogrenelim
-net:192.168.10.0 yazip sonuc bulabiliriz tabi bu aramayi genisletebiliriz 
--net:192.168.10.0/24 yazip bu o networkteki tum bilgileri gosteririr.
