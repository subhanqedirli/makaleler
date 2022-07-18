# Bottles kullanarak Linux'ta Windows Uygulamaları ve oyunları çalıştırın
![Bottles](https://i.imgur.com/PBWcNum.png)
##   
Linux'ta Wine/Windows ortamlarını yönetmenin kolay ve yeni bir yolunu mu arıyorsunuz? Artık Windows yazılımlarını ve oyunlarını Bottles ile Linux'ta çalıştırabilirsiniz. Windows ortamları, bir Windows uygulamasının çalıştırıcılarla çalıştırılabileceği ortamlar olarak tanımlanır. Wine, birinin Windows uygulamalarını Linux tabanlı bir sistemde çalıştırmasını sağlayan uyumluluk katmanlarıdır.
######             
Bootles 2017 yılında kişisel tüketim için geliştirildi. Birkaç iyileştirmeden sonra, Bottles artık çevre tabanlı şişeler(ortamlar) oluşturmak ve yönetmek için en basit yöntemi sağlıyor. Bu şişeler ile istenilen Windows uygulaması çalıştırılabilmektedir.
#### Bottles'ın en önemli özellikleri şunlardır:
###  
- Ayrıca topluluk tarafından yönlendirilen bir depoya dayanan tam entegre bir yükleyici yöneticisi
- En yaygın bağımlılıklar önceden yüklenmiş ve birçok yazılımı hemen çalıştırmak için özel bir yapılandırma ile Oyun veya Yazılım için hazır, önceden yapılandırılmış ortamlar aracılığıyla yönetimi kolay, ayrıca ortamınızı sıfırdan yapılandırabilirsiniz.
- Yüklü programları otomatik olarak algılar, bunları program listesine manuel olarak eklemenize gerek yoktur.
- Basitleştirilmiş DLL geçersiz kılmaları
- Dosya yöneticinizdeki bağlam menüsünü kullanarak şişelerinizdeki her yürütülebilir dosyayı (.exe/.msi/.bat) çalıştırmanıza izin verir.
- Yürütülebilir dosya argümanları için entegre yönetim ve depolama
- Yapılandırması kolay veya tam yedekleme dışa aktarma ve içe aktarma, ayrıca klonlamayı da destekler.
- Özel ortam değişkenleri için destek
- Wine süreçleri için Entegre Görev Yöneticisi
- Destek için ProtonDB ve WineHQ'ya kolay erişim
- Daha iyi oyun performansı için esync, fsync, dxvk, önbellek, gölgelendirici derleyici, boşaltma e.t.c gibi çeşitli optimizasyonlar
- Şişelerden çıkmadan farklı wine önek ayarlarının değiştirilmesine izin verir.
- Şişe için ortam güncellemelerini kontrol etme ve kırılma durumunda otomatik onarım sistemi
##  
Bu rehber, Linux'ta Windows uygulamalarını ve oyunlarını çalıştırmak için Bottles'ın nasıl kurulacağı ve kullanılacağı hakkında gerekli adımları sağlar.
## Linux'ta Bottles Nasıl Kurulur
###    
 Bottles'ı istediğiniz yerden kurabilirsiniz. Appimage, Debain, Fedora, AUR, Snap ve Flatpak olarak edinebilirsiniz.
- Flatpak
- AUR
- Fedora
- Kaynaktan derleme
### Flatpak (Önerilir)
Flatpak, tam korumalı sürümü sağlar. Burada gerekli tüm bağımlılıklar tek bir pakette toplanmıştır.
###   
Flatpak'ı kurduktan sonra Bottles indirmek için Flathub deposunu bu komutla aktif edin:
```
sudo flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```
Şimdi depodan Bottles'ı aratalımş
``` 
$ sudo flatpak search Bottles
Name     Description                                              Application ID                           Version            Branch Remotes
Bottles  Run Windows software                                     com.usebottles.bottles                   2022.4.14-trento-1 stable flathub
GxPlugi… GxPlugins LV2                                            …reedesktop.LinuxAudio.Plugins.GxPlugins 0.9.0              21.08  flathub
GxPlugi… GxPlugins LV2                                            …reedesktop.LinuxAudio.Plugins.GxPlugins 0.9.0              20.08  flathub
AAAAXY   A nonlinear puzzle platformer taking place in impossibl… io.github.divverent.aaaaxy               v1.2.15            stable flathub
```
Şimdiyse Bottles'ı kuralım.
``` 
sudo flatpak install flathub com.usebottles.bottles
```
Her şey yolundaysa böyle bir çıktı alacaksınız:
```
Looking for matches…
Required runtime for com.usebottles.bottles/x86_64/stable (runtime/org.gnome.Platform/x86_64/42) found in remote flathub
Do you want to install it? [Y/n]: y

com.usebottles.bottles permissions:
    ipc            network        pulseaudio        wayland                x11
    devices        devel          multiarch         dbus access [1]        system dbus access [2]

    [1] org.freedesktop.Notifications
    [2] org.freedesktop.UDisks2


        ID                                                   Branch                  Op            Remote             Download
 1.     com.usebottles.bottles.Locale                        stable                  i             flathub            < 491.8 kB (partial)
 2.     org.freedesktop.Platform.GL.default                  21.08                   i             flathub            < 131.3 MB
 3.     org.freedesktop.Platform.GL32.default                21.08                   i             flathub            < 138.6 MB
 4.     org.freedesktop.Platform.ffmpeg-full                 21.08                   i             flathub              < 4.2 MB
 5.     org.freedesktop.Platform.ffmpeg_full.i386            21.08                   i             flathub              < 4.3 MB
 6.     org.freedesktop.Platform.openh264                    2.0                     i             flathub              < 1.5 MB
 7.     org.gnome.Platform.Compat.i386                       42                      i             flathub            < 153.7 MB
 8.     org.gnome.Platform.Locale                            42                      i             flathub            < 335.9 MB (partial)
 9.     org.gnome.Platform                                   42                      i             flathub            < 275.5 MB
10.     org.winehq.Wine.DLLs.dxvk                            stable-21.08            i             flathub             < 21.4 MB
11.     org.winehq.Wine.gecko                                stable-21.08            i             flathub            < 114.0 MB
12.     org.winehq.Wine.mono                                 stable-21.08            i             flathub             < 85.1 MB
13.     com.usebottles.bottles                               stable                  i             flathub            < 138.6 MB

Proceed with these changes to the system installation? [Y/n]: y
```
### AUR
Bottles için AUR'da 2 paket mevcuttur:
- bottles - (resmi) - en son stabil paket
- bottles-git - (resmi olmayan) - githubdaki en son sürümü kurar


Paketi indirmek için herhangi bir AUR yardımmcısı(genellikle yay veya paru) kullanmalıyız.
```
## Bottles için
yay -S bottles
paru -S bottles

## Bottles-git için
yay -S bottles-git
paru -S bottles-git
```
### DNF
 En kolay yolun bu olduğunu söyleyebilirim. Bu komutu kullanrak kurabiliriz:
 ```
 sudo dnf install bottles
 ```
### Kaynaktan derleme
Bazı Linux dağıtımlarında, Bottles'ı kaynaktan derleyerek kurmanız gerekir. Ancak devam etmeden önce aşağıdaki paketlerin kurulu olması gerekir:
- ninja
- python3
- Git
- meson
- glib
    - glib2-devel - Fedora için
    - libglib2.0-dev - Debian/Ubuntu için

Gereksinimler karşılandıktan sonra devam edin ve Bottles'ı Git'ten kopyalayın.
```
git clone https://github.com/bottlesdevs/Bottles.git
cd Bottles
```
Şişeleri aşağıdaki komutlarla oluşturun ve kurun:
```
mkdir build
meson build && cd build
ninja -j$(nproc)
ninja install
```
## Linux'ta Bottles Uygulamasını Çalıştırmak
Bottles kurulduğuna göre, Windows uygulamalarını ve oyunlarını Linux üzerinde kolayca çalıştırabilirsiniz. Bottles uygulamalar menüsünden başlatılabilir.
###  
![](https://i.imgur.com/K6aVHMm.png)
###  
Bottles açıldı. Bir şişe oluşturalım.
###  
![](https://i.imgur.com/CA6OiTT.png)
###   
Devam edin ve bileşenlerin en son sürümlerini indirin; Bottles genel deposundan DXVK, Caffe runner, LatencyFleX, Runtime, NVAPI ve VKD3D.
###  
![](https://i.imgur.com/9Wa6ykt.png)
###    
İşlem tamamlandığında şu mesajı göreceksiniz:
###  
![](https://i.imgur.com/JLqEyXZ.png)
###  
## Bottles kullanarak Windows uygulamasını/oyunlarını Linux üzerinde çalıştırın.
Şimdi sol üstteki "+"" simgesine basarak yeni bir şişe oluşturarak başlayın.
###  
![](https://i.imgur.com/wi7eGqU.png)
###  
Gerekli ayrıntıları sağlayarak şişeyi oluşturun.
###  
![](https://i.imgur.com/VEMBUDN.png)
###  
Ortamı şu şekilde seçin:
- DXVK etkin, VKD3D devre dışı, Esync etkin, Ayrık Grafik Kartı etkin, oyun içinde daha iyi ses kalitesi için PulseAudio gecikmesi 60 ms'ye zorlanan oyunlar için oyun, Arial, Times ve Courier yazı tipleri
- Multimedya uygulamaları için destek sağlamak için DXVK ve VKD3D etkinleştirilmiş uygulamalar için uygulama.
- Deneyler yapmaya başlayabileceğiniz net bir çalışma alanı özelleştirin

Uygulama ortamını ayarlayalım.
###  
![](https://i.imgur.com/EdJOorE.png)
###  
Aşağıdaki gibi ortam oluşturulacaktır.
###  
![](https://i.imgur.com/LNWCIha.png)
###  
Tamamlandığında, bunu göreceksiniz.
###  
![](https://i.imgur.com/9U4a4ku.png)
###   
Şimdi ortamda .exe veya .msi uygulamasını çalıştıralım.
###   
![](https://i.imgur.com/8sbsL7c.png)
###  
Yürütülebilir dosyayı dosya sisteminden seçin ve çalıştır'a tıklayın.
###   
![](https://i.imgur.com/80zQcOg.png)
###  
Uygulama kurulumu aşağıdaki gibi başlayacaktır. Tıpkı bir Windows sisteminde olduğu gibi uygulama kurulumunu sonuna kadar takip edin.
###  
![](https://i.imgur.com/ejMMiqU.png)
###   
Tamamlandığında, uygulama programlar sekmesinde görünmelidir.
###   
![](https://i.imgur.com/jQSZBpf.png)
###   
Uygulamayı çalıştırın. Uygulamayı çalıştırmak için de birkaç seçenek vardır.
![](https://i.imgur.com/yzbiPQi.png)
###   
Uygulama gösterildiği gibi çalışmalıdır.
![](https://i.imgur.com/1HYtcrX.png)
###   

## Bitiş
Umarım bu yazıyla sizlere temel Linux kavramlarını anlatmış, size bir şeyler katabilmişimdir. Aşağıdaki bağlantılardan bana ulaşa bilirsiniz.

Email: subhanqedirli@protonmail.com                 [Youtube](https://www.youtube.com/channel/UCCyrdKjOWMQFu4MpAuD9ajg) [Discord](https://discord.gg/jwR4sAYQ5n)  [Telegram](https://t.me/LinuxisnotUNIXchannel) [Mastodon](https://mastodon.social/web/accounts/106607411263382617) 
## Kaynakça 
[Bottles](https://usebottles.com/)
###  
[Computing for Geeks](https://computingforgeeks.com/run-windows-apps-and-games-on-linux-using-bottles/)
