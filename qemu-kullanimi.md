# Qemu-KVM kullanımı

Bu belgede **qemu-kvm** kullanımı anlatılmaktadır. İşin teknik detayından çok kullanmak isteyenlerin işini görmesi için basitleştirerek anlatmaya çalışacağız.

Not: Bu belgede **debian sid** üzerinde olduğunuzu varsayarak anlatım yaptım ama diğer dağıtımlarda da benzer şekilde kullanımı var.

Qemu kullanmak için **gui** uygulamalar da vardır. Örneğin *gnome-boxes* ile qemuyu grafik tabanlı olarak kullanabilirsiniz. Bu belgede buna değinmeyeceğiz. terminalden kullanımı üzerine anlatım olacak.

## Qemu kurulumu

Debian için **apt-get install qemu-kvm** komutunu kullanabiliriz. Uefi bios ile kullanmak için **ovmf** paketine gerek duyulmaktadır. onuda debian için **apt-get install ovfm** komutu ile kurabiliriz.

## Disk imajı oluşturma

**qemu-img** komutu ile kolay yoldan imaj açabiliriz. boyutunu **G** **M** gibi harfler ile ifade ediyoruz. Örneğin:

```bash
$ qemu-img create deneme.img 30G
Formatting 'deneme.img', fmt=raw size=32212254720
```

Bu disk imajı **raw** formattadır. yani disk imajını usb belleğe *dd* komutu ile yazıp daha sonra bunu kullanabilirsiniz.

**Raw** yerine **qcow2** formatta oluşturmak isterseniz **-f qcow2** parametresini ekleyebilirsiniz. Örneğin:

```bash
$ qemu-img create -f qcow2 deneme.qcow2 30G
```

**Raw** imajlar çok fantastik şeyler yaparsanız diske zarar verebilir. **Qcow2** imajlar ise daha az zararlıdır ama *dd* komutu ile doğrudan basıp kullanılamaz.

## Sanal makinanın başlatılması

**qemu-system-x86_64** komutu ile başlatılır. **--enable-kvm** parametresi eklenerek **kvm** etkinleştirilmelidir. yoksa çok kasar. Debianda **kvm** komutu bu komutun kısa halidir. eğer **kvm** komutu yoksa **bashrc** içine **alias** ekleyebilirsiniz. Örnek kullanım:

```bash
$ qemu-system-x86_64 --enable-kvm
```

Ardından oluşturduğumuz disk imajını qemuya hard disk olarak bağlamamız gerekli. onun için de **-hda** parametresi kullanılır. Ayrıca **-m** parametresi ile bellek miktarını **G** **M** gibi semboller ile göstererek belirtmemiz gerekli. Örneğin:

```bash
$ qemu-system-x86_64 --enable-kvm -hda deneme.img -m 2G
WARNING: Image format was not specified for 'deneme.img' and probing guessed raw.
       Automatically detecting the format is dangerous for raw images, write operations on block 0 will be restricted.
       Specify the 'raw' format explicitly to remove the restrictions.
```

Örnekteki gibi uyarı vermesinin sebebi raw disk imajı kullanmamızdan dolayı. Çok fantastik şeyler yapmayacaksak çokta önemli değil :D Ayrıca raw imaj yerine usb bellek hard disk gibi şeyleri de kullanabilirsiniz. imaj konumu olarak /dev/sdx vermeniz yeterlidir.

Şimdi sıra geldi sanal makinaya format atmaya. Bunun için iso imajını bağlamak gerekli. bunun için **-cdrom** parametresi kullanılmalıdır. Örneğin:

```bash
$ qemu-system-x86_64 --enable-kvm -hda deneme.img -m 2G -cdrom debian-live-10.4.0-amd64-gnome.iso
```

**Uefi** bios için **ovmf** eklememiz gerekir. onun için **-bios /usr/share/ovmf/OVMF.fd** parametresi eklenebilir. (bu dosyanın konumu dağıtımdan dağıtıma değişebilir.)

```
$ qemu-system-x86_64 --enable-kvm -hda deneme.img -m 2G -cdrom debian-live-10.4.0-amd64-gnome.iso -bios /usr/share/ovmf/OVMF.fd
```

## Bazı parametreler

Doğrudan tablo şeklinde vermeyi düşündüm. Bu belgeyi okumaya üşenip buraya bakabilirsiniz.

| Parametreler                    | Anlamları                                                 |
| ------------------------------- | --------------------------------------------------------- |
| -boot d                         | cdrom ile başlat                                          |
| -boot c                         | hdd ile başlat                                            |
| -m 3G                           | 3gb ram kullan                                            |
| --enable-kvm                    | KVM etkinleştir                                           |
| -cdrom xx                       | iso dosyasını cdrom olarak ayarla                         |
| -hda xx                         | birinci hard disk imajı                                   |
| -hdb xx                         | ikinci hard disk imajı                                    |
| -hdc xx                         | üçüncü hard disk imajı                                    |
| -hdd xx                         | dördüncü disk imajı                                       |
| -cpu host                       | yerel makinanın işlemci ismini sanal makinada kullan      |
| -smp cores=2                    | çift çekirdek kullan                                      |
| -vga cirrus                     | ekran kartı olarak cirrus göster                          |
| -vga vmware                     | ekran kartı olarak vmware göster                          |
| -display vnc:0                  | görüntüyü vnc üzerinden al (5900 portundan)               |
| -soundhw ac97                   | ses kartı olarak ac97 ekle                                |
| -nic user,hostfwd=tcp::2222-:22 | Sanal makinadaki 22 portunu hostun 2222 portuna yönlendir |
| -bios /usr/share/ovmf/OVMF.fd   | UEFI olarak başlat                                        |

## Bitiş

Umarım bu yazıyla size qemu-kvm kullanımını anlata bilmişimdir. Aşağıdaki adreslerden bana ulaşa bilirsiniz.

Email: subhanqedirli@protonmail.com                 [Youtube](https://www.youtube.com/channel/UCCyrdKjOWMQFu4MpAuD9ajg) [Discord](https://discord.gg/jwR4sAYQ5n) [Matrix](https://matrix.to/#/!kSPvsnjXUJDMJszYek:matrix.org?via=matrix.org) [Telegram](https://t.me/LinuxisnotUNIXchannel) [Mastodon](https://mastodon.social/@subhanqedirli)  