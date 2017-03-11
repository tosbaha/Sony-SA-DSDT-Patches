# English
# Sony-SA-DSDT-Patches
DSDT and SSDT Patches for Sony SA
This patches are created for my Sony VPCSA33GX Laptop. In order to use these patches you must have following

1. Clean DSDT and SSDT(s)
2. Your EDID data
3. MaciASL
4. Applying Patches


## Extracting your DSDT and SSDT files
You can extract your ACPI tables either within Windows or Linux.
### Extracting using Windows
Although I only used this to extract my DSDT, you can extract DSDT and SSDT files using Windows. If you are using Windows, download RW Everything from http://rweverything.phpnet.us/index.htm Run RW-Everything, select ACPI Tables. From ACPI Tables save DSDT and *all* SSDT files.

### Extracting using Linux
We will need all DSDT and SSDT tables. Boot with any Live Linux USB(Ubuntu, Parted Magic.....) and issue following commands in Terminal

```
sudo cat /sys/firmware/acpi/tables/DSDT >dsdt.aml
sudo cat /sys/firmware/acpi/tables/SSDT1 >ssdt1.aml
sudo cat /sys/firmware/acpi/tables/SSDT2 >ssdt2.aml
sudo cat /sys/firmware/acpi/tables/SSDT3 >ssdt3.aml
sudo cat /sys/firmware/acpi/tables/SSDT4 >ssdt4.aml
sudo cat /sys/firmware/acpi/tables/SSDT5 >ssdt5.aml
sudo cat /sys/firmware/acpi/tables/SSDT6 >ssdt6.aml
```

### Extracting using Clover
Dump your original ACPI tables with Clover by hitting F4 on boot screen. Original tables will be saved to /EFI/CLOVER/origin folder.

## Your EDID data
You will not able to see installation screen, if you don't add the necessary EDID data. Your screen EDID data can be different than mine. Therefore you must extract your native EDID from Windows. You can use [Monitor Asset Manager](http://www.entechtaiwan.com/util/moninfo.shtm) to extract. Download the software, open it and select your monitor and copy the 128 bytes raw data. You will use this data in your EDID patch.
## MaciASL
Download RehabMan's [MaciASL](https://bitbucket.org/RehabMan/os-x-maciasl-patchmatic/downloads) Open MaciASL and add my repo by going Preferences/Sources
## Applying Patches
### DSDT Patches
Open your DSDT file with MaciASL and apply patches. EDID data for 1600 x 900 Display patch is a *must* Actually without this patch you will not able to install OSX at all. You can use VM, or previously installed OSX to apply this patch first. HDEF is patched for layout 3. If you are using other AppleHDA, change the layout id. You can also apply other patches to enable brightness control and fix other issues. 
##Disabling Radeon
Patch SSDT-7.aml with SSDT patches from repo(Rename GFX0 to IGPU,AMD Disable, Cleanup SSDT)


---

# Türkçe
# Sony-SA-DSDT-Yamaları

Bu yamalar Sony VPCSA33GX Laptop için üretilmiştir. Bu yamaları kullanabilmek için aşağıdaki işlemlerin yapılması gerekir

1. Temiz DSDT ve SSDT dosyaları
2. EDID bilgisi
3. MaciASL
4. Yamaların uygulanması


## DSDT ve SSDT dosyalarının alınması
ACPI tablosu Windows veya Linux üzerinden alınabilir.
### Windows
Ben bu methodu sadece DSDT mi almak için kullanmış olsamda bu method ile DSDT ve SSDT dosyaları da alınabilir. Öncelikle [RW-Everything](http://rweverything.phpnet.us/index.htm) uygulamasını indirin. RW-Everything i çalıştırın ve ACPI Tables'ı seçin. Daha sonrada DSDT ve *tüm* SSDT dosyalarını kaydedin.

### Linux
Bütün DSDT ve SSDT dosyalarına ihtiyacımız olacak. Herhangi bir Linux(Ubuntu, Parted Magic.....) ile bilgisayarınızı boot edin aşağıdaki komutları  Terminal ekranına yapıştırın.

```
sudo cat /sys/firmware/acpi/tables/DSDT >dsdt.aml
sudo cat /sys/firmware/acpi/tables/SSDT1 >ssdt1.aml
sudo cat /sys/firmware/acpi/tables/SSDT2 >ssdt2.aml
sudo cat /sys/firmware/acpi/tables/SSDT3 >ssdt3.aml
sudo cat /sys/firmware/acpi/tables/SSDT4 >ssdt4.aml
sudo cat /sys/firmware/acpi/tables/SSDT5 >ssdt5.aml
sudo cat /sys/firmware/acpi/tables/SSDT6 >ssdt6.aml
```
Bu komutu çalıştırdığınız yerde oluşan *.aml dosyalarını kopyalayın.

### Extracting using Clover
Orjinal ACPI tablolarını en kolay Clover ile alabilirsiniz. Clover ekranında iken F4 tuşuna basınç Böylecek orjinal tablolar /EFI/CLOVER/origin klasörüne kaydedilecektir.

## EDID bilgisi
Eğer EDID bilgisini eklemezseniz kurulum ekranını göremezsiniz. Sizin EDID bilginiz benimkinden farklı olabilir. Bu yüzden EDID bilgisini Windows üzerinden almanız gerekmektedir. [Monitor Asset Manager](http://www.entechtaiwan.com/util/moninfo.shtm) programını kullanarak bu bilgiye sahip olabilirsiniz. Programı indirip çalıştırın ve monitörünüzü seçip daha sonra 128 karakterden oluşan EDID bilgisini kopyalayın. Bu bilgiyi EDID yamasında kullanacaksınız.
## MaciASL
RehabMan'ın [MaciASL](https://bitbucket.org/RehabMan/os-x-maciasl-patchmatic/downloads) yazılımını kısmından inidirin ve daha sonra MaciASL i açın ve Preferences/Sources sekmesini seçin. Daha sonra __+__ butonuna tıklayaın. **Name** kısmına Sony **URL** kısmına da https://raw.githubusercontent.com/tosbaha/Sony-SA-DSDT-Patches/master/ yazın.
## Yamaların Uygulanması
### DSDT Patches
DSDT dosyanızı MaciASL ile açın ve yamaları uygulayın. EDID data for 1600 x 900 Display yaması *zorunlu* bir yamadır. Bu yama olmadan kurulum ekranı açılmyacaktır. Eğer DSDT yaması yapamıyorsanız bu bilgileri Clover ile de ekleyebilirsiniz. ACL275 ses kartı için HDEF yamasının yapılması gerekmektedir. Ekran parlaklığı, batarya ve diğer şeyler için diğer yamaları da uygulayabilirsiniz.
##Disabling Radeon
SSDT-7.aml dosyasını bu repo da bulunan SSDT yamaları ile yamalayın.(Rename GFX0 to IGPU,AMD Disable, Cleanup SSDT)