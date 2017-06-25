# English
# Sony-SA-DSDT-Patches
These patches are created for my Sony VPCSA33GX Laptop. In order to use these patches, please follow below steps.

1. [Extracting your DSDT and SSDT files](#extracting-your-dsdt-and-ssdt-files)
2. [EDID data](#edid-data)
3. [MaciASL](#maciasl)
4. [Applying Patches](#applying-patches)

## Extracting your DSDT and SSDT files
Dump your original ACPI tables with Clover by hitting F4 on boot screen. Original tables will be saved to /EFI/CLOVER/origin folder. Create your SSDT.aml by using [ssdtPRGen](https://github.com/Piker-Alpha/ssdtPRGen.sh)
### Disassembling your files
Download [iasl](https://bitbucket.org/RehabMan/acpica/downloads) from RehabMan's repo. If you downloaded iasl.zip to Downloads folder;

```bash
cd ~/Downloads
unzip iasl.zip
sudo cp iasl /usr/bin
```

Create a `refs.txt` with the following content

```
External(_GPE.MMTB, MethodObj, 0)
External(_SB.PCI0.LPCB.H_EC.ECWT, MethodObj, 2)
External(_SB.PCI0.LPCB.H_EC.ECRD, MethodObj, 1)
External(_SB.PCI0.LPCB.H_EC.ECMD, MethodObj, 1)
External(_SB.PCI0.PEG0.PEGP.SGPO, MethodObj, 2)
External(_SB.PCI0.SAT0.SDSM, MethodObj, 4)
External(_GPE.VHOV, MethodObj, 3)
External(_SB.PCI0.XHC.RHUB.TPLD, MethodObj, 2)
```

Put `refs.txt` and all files from /EFI/CLOVER/origin folder to any folder you choose. Go to that directory and

```bash
iasl -da -dl -fe refs.txt *.aml
```

Apply all your patches to .dsl files and save it as .aml file and put them in /EFI/CLOVER/patched folder. SSDT files with x suffix are not needed. If SSDT doesn't nee a patch, you can directly copy that SSDT file without compiling.

## EDID data
You will not able to see installation screen if you don't add the necessary EDID data. Your screen EDID data can be different from mine. Therefore, you must extract your native EDID from Windows. You can use [Monitor Asset Manager](http://www.entechtaiwan.com/util/moninfo.shtm) to extract. Download the software, open it and select your monitor and copy the 128 bytes raw data. You will use this data in your EDID patch.

**10.12.4 Update**

This update requires some changes to EDID data. You must also patch your EDID data with included `edidparser.rb` Run `edidparser.rb` and change your EDID either with DSDT or Clover patch.

## MaciASL
Download RehabMan's [MaciASL](https://bitbucket.org/RehabMan/os-x-maciasl-patchmatic/downloads) Open MaciASL and add my repo by going Preferences/Sources
## Applying Patches
### DSDT Patches
Open your DSDT file with MaciASL and apply patches. EDID data for 1600 x 900 Display patch is a *must*. Actually, without this patch, you will not able to install macOS at all. You can use VM, or previously installed macOS to apply this patch first. HDEF is patched for layout 3. If you are using other AppleHDA, change the layout id. You can also apply other patches to enable brightness control and fix other issues. 

### Disabling Radeon
Patch SSDT-7.aml with SSDT patches from repo(Rename GFX0 to IGPU,AMD Disable, Cleanup SSDT)

---

# Türkçe
# Sony-SA-DSDT-Yamaları

Bu yamalar Sony VPCSA33GX Laptop için üretilmiştir. Bu yamaları kullanabilmek için aşağıdaki işlemlerin yapılması gerekir

1. [DSDT ve SSDT dosyalarının alınması](#dsdt-ve-ssdt-dosyalar%C4%B1n%C4%B1n-al%C4%B1nmas%C4%B1)
2. [EDID bilgisi](#edid-bilgisi)
3. [MaciASL](#maciasl-1)
4. [Yamaların uygulanması](#yamalar%C4%B1n-uygulanmas%C4%B1)

## DSDT ve SSDT dosyalarının alınması
Orjinal ACPI tablolarını en kolay Clover ile alabilirsiniz. Clover ekranında iken F4 tuşuna basın. Böylece orjinal tablolar /EFI/CLOVER/origin klasörüne kaydedilecektir. SSDT.aml dosyanızı [ssdtPRGen](https://github.com/Piker-Alpha/ssdtPRGen.sh) ile oluşturun.

### DSDT ve SSDT dosyalarınınn oluşturulması

RehabMan'in [iasl](https://bitbucket.org/RehabMan/acpica/downloads) programını indirin. Eğer mesela Downloads klasörüne indirdiyseniz,

```bash
cd ~/Downloads
unzip iasl.zip
sudo cp iasl /usr/bin
```

Öncelikle `refs.txt` adında bir dosya oluşturun ve içine şunları yazın

```
External(_GPE.MMTB, MethodObj, 0)
External(_SB.PCI0.LPCB.H_EC.ECWT, MethodObj, 2)
External(_SB.PCI0.LPCB.H_EC.ECRD, MethodObj, 1)
External(_SB.PCI0.LPCB.H_EC.ECMD, MethodObj, 1)
External(_SB.PCI0.PEG0.PEGP.SGPO, MethodObj, 2)
External(_SB.PCI0.SAT0.SDSM, MethodObj, 4)
External(_GPE.VHOV, MethodObj, 3)
External(_SB.PCI0.XHC.RHUB.TPLD, MethodObj, 2)
```

Daha sonra `refs.txt` ve /EFI/CLOVER/origin klasöründeki DSDT ve SSDT-* dosyalarını istediğiniz bir klasöre kopyalayın. O klasöre gidin ve terminale şu komutu girin.

```bash
iasl -da -dl -fe refs.txt *.aml
```

Yamaları .dsl dosyalarına uygulayın ve oluşan dosyaları
/EFI/CLOVER/patched klasörune kopyalayın. Sonunda x olan SSDT dosyaları dinamik olarak oluştulduğundan bunların kopyalanmasına gerek yoktur.

## EDID bilgisi
Eğer EDID bilgisini eklemezseniz kurulum ekranını göremezsiniz. Sizin EDID bilginiz benimkinden farklı olabilir. Bu yüzden EDID bilgisini Windows üzerinden almanız gerekmektedir. [Monitor Asset Manager](http://www.entechtaiwan.com/util/moninfo.shtm) programını kullanarak bu bilgiye sahip olabilirsiniz. Programı indirip çalıştırın ve monitörünüzü seçip daha sonra 128 karakterden oluşan EDID bilgisini kopyalayın. Bu bilgiyi EDID yamasında kullanacaksınız.

**10.12.4 Güncellemesi**

Bu güncelleme ile EDID bilgisinin yamanması gerekmektedir. EDID bilginizi `edidparser.rb` ile yamalayın. Ekteki `edidparser.rb` ile oluşan EDID bilgisini ister Clover ister DSDT ile ekleyin.

## MaciASL
RehabMan'ın [MaciASL](https://bitbucket.org/RehabMan/os-x-maciasl-patchmatic/downloads) yazılımını inidirin ve daha sonra MaciASL i açın ve Preferences/Sources sekmesini seçin. Daha sonra __+__ butonuna tıklayın. **Name** kısmına Sony **URL** kısmına da https://raw.githubusercontent.com/tosbaha/Sony-SA-DSDT-Patches/master/ yazın.
## Yamaların Uygulanması
### DSDT Yamaları
DSDT dosyanızı MaciASL ile açın ve yamaları uygulayın. EDID data for 1600 x 900 Display yaması *zorunlu* bir yamadır. Bu yama olmadan kurulum ekranı açılmayacaktır. Eğer DSDT yaması yapamıyorsanız bu bilgileri Clover ile de ekleyebilirsiniz. ACL275 ses kartı için HDEF yamasının yapılması gerekmektedir. Ekran parlaklığı, batarya ve diğer şeyler için diğer yamaları da uygulayabilirsiniz.

### Radeon kartın kapatılması
SSDT-7.aml dosyasını bu repo da bulunan SSDT yamaları ile yamalayın.(Rename GFX0 to IGPU,AMD Disable, Cleanup SSDT)