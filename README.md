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
## Your EDID data
You will not able to see installation screen, if you don't add the necessary EDID data. Your screen EDID data can be different than mine. Therefore you must extract your native EDID from Windows. You can use Monitor Asset Manager from http://www.entechtaiwan.com/util/moninfo.shtm to extract. Download the software, open it and select your monitor and copy the 128 bytes raw data. You will use this data in your EDID patch.
## MaciASL
Download RehabMan's MaciASL from https://bitbucket.org/RehabMan/os-x-maciasl-patchmatic/downloads Open MaciASL and add my repo by going Preferences/Sources
## Applying Patches
### DSDT Patches
Open your DSDT file with MaciASL and apply patches. EDID data for 1600 x 900 Display patch is a *must* Actually without this patch you will not able to install OSX at all. You can use VM, or previously installed OSX to apply this patch first. I use patched AppleHDA from http://www.insanelymac.com/forum/topic/298663-applehda-for-yosemite/ for Realtek ACL275 sound card. That is why HDEF is patched for layout 3. If you are using other AppleHDA change the layout id. You can also apply other patches to enable brightness control and several fixes. 
### SSDT Patch
In order to disable AMD card, SSDT must also be patched. I assume that you created your SSDT with https://github.com/Piker-Alpha/ssdtPRGen.sh Now open terminal and go to the folder which has all DSDT and SSDT files we extracted before. Issue following command.
```
iasl -da -dl *.aml
```
After this you will get bunch of dsl files in the same directory. Open ssdt5.dsl and apply Disable AMD patch. Then save as SSDT-1.aml and file type as ACPI Machine Language Battery. Copy SSDT-1.aml file to your Extra folder(if you are using Chimera)
