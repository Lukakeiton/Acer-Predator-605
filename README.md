# Acer-Predator-605

Español:

Hackintosh para Acer Predator 605

Bienvenidos a mi segundo hackintosh.

Especificaciones:

- Intel Core i7 4790
- Placa base MS-7829 LGA1150
- Sapphire Nitro+ Radeon RX 590 8GB GDDR5 UEFI
- BCM94352HMB 802.11ac WiFi Bluetooth 867Mbps Wireless-AC WiFi + BT 4,0 half Mini PCI-E
- SSD WDC WD10EZEX-21M2NA0 para Windows 10
- SSD TCSUNBOW X3 480GB para Mac OS Catalina

Para hacer un doble inicio de Windows 10 y Mac OS Catalina, tiene que instalarlos de forma independiente. En otras palabras, se puede instalar cada sistema operativo en cualquier orden, simplemente desconecte el disco duro en el que acaba de instalar para evitar problemas de inicio. Instalé Windows 10 primero, tan sencillo como lo es. Luego, instalé Mac os Catalina desenchufando el disco duro de Windows.

Cómo hacer un instalador USB para Mac OS Catalina

Se necesitará:
- 16GB USB o de mayor capacidad
- Mac OS Catalina de App Store (o una actualización de software)
- Instalador de Clover EFI pkg
- Un ordenador con mac o un hackintosh

Encienda su Mac o hackintosh, abra Utilidad de Discos y formatee el USB con el nombre "MacOSInstaller" con el formato HFS+ Journaled (Mac OS extended (Journaled)). Abra la terminal y escriba el siguiente comando:

sudo /Applications/Install\ macOS\ Catalina.app/Contents/Resources/createinstallmedia --volume /Volumes/MacOSInstaller

Mantenga la calma, tardará 30 minutos en terminar.

Una vez terminado, descargue la última versión pkg de Clover EFI desde:

https://github.com/CloverHackyColor/CloverBootloader/releases

Instale Clover en el USB con las siguientes opciones (botón de personalizr), deje el resto como está:

- ApfsDriverLoader
- AptioInputFix
- AudioDxe
- DataHubDxe
- Fat
- FSInject
- OsxAptioFixDrv
- SMCHelper
- VBoxHfs

Una vez haya creado el USB, copie los kexts prorpocionado en EFI/CLOVER/kexts/Other.Primero. la configuración de la BIOS:

Para acceder a la configuración BIOS/UEFI, presione y mantenga la tecla suprimir en un teclado USB mientras el sistema está cargando
- Load Optimized Defaults
- Set AHCI for HDD/SSD
- Disable VT-d
- Disable Secure Boot Mode
- Save and exit.

Ahora, presione F12 or acceda a la configuración de la BIOS/UEFI para dar prioridad al inicio desde USB.

Una vez se ejecute desde el USB, Clover aparecerá. Tiene que seleccionar Mac OS Installer, espere unos minutos, entonces el instalador aparecerá.

Abra Utilidad de Discos y formatee el disco duro en HFS+ Jounaled. Ciérrelo.

Instale Mac OS Catalina en el disco duro. Varios reininicios, sin importancia, se darán, inicie de nuevo desde el USB y eliga Mac OS Installer desde Clover.

Una vez haya instalado el sistema operativo, inicie desde el USB una vez más para entrar en Mac OS Catalina. 

Una vez ejecutado, instale Clover en el disco duro con las siguientes opciones, deje las demás como están:

- ApfsDriverLoader
- AptioInputFix
- AudioDxe
- DataHubDxe
- Fat
- FSInject
- OsxAptioFixDrv
- SMCHelper
- VBoxHfs

NO REINICIE. Despues de que termine la instalación, necesitará instalar algunos kexts (driver en Mac) para hacer que todo funcione. Para hacerlo, descargue la última versión de estos kexts:

- AppleALC
- Lilu
- WhatEverGreen
- FakeSMC
- USBInjectAll
- IntelMausiEthernet
- FakePCIID
- FakePCIID_Intel_HD_Graphics
- FakePCIID_Broadcom_WiFi
- BrcmPatchRAM2
- BrcmFirmwareData
- BrcmBluetoothInjector
- VoodooPS2Controller

También, tiene que descargar Clover Configurator (CC). Monte la partición EFI, descative el SIP y copie los anteriores kexts en Library/Extensions con Clover Configurator (CC). Ahora, seleccione el archivo config.plist desde el inicio de CC.

En la sección de ACPI, añada los parches "change GFX0 to IGPU", "change HECI to IMEI" y "change PEGP to GFX0".

En la sección de Boot, añada "dart=0", "nv-disable=1" y "-cdfon" en la subseción Arguments.

En la sección Device, seleccione "Inject", "Add ClockID", "FixOwnership" y "HighCurrent" en la subsección USB. Además, en la subsección de Audio, escriba "15" donde pone Inject y marque "ResetHDA".

En la sección Rt Variables, escriba en BooterConfig "0x28" y en CsrActiveConfig "0x67".

Ahora, guárdelo y reinicie. Eso es todo.

SI QUIERE AÑADIR LA PARTICIÓN DE WINDOWSA A CLOVER

Monte la EFI.

Vaya a EFI/BOOT, copie BOOTX64.efi y péguelo en EFI/Windows/Boot. Renombre el archivo anterior a bootmgfw.efi.

Ahora, apague el PC, conecte el disco duro con Windows y entre en la configuración de la BIOS. Selecione como primer disco duro de arranque aquel donde Mac OS está instalado, guarde los cambios y reinicie. Eso es todo.

English

Hackintosh for Acer Predator 605

Welcome everyone to my second hackintosh.

Specs:
- Intel Core i7 4790
- MS-7829 motherboard LGA1150
- Sapphire Nitro+ Radeon RX 590 8GB GDDR5 UEFI
- BCM94352HMB 802.11ac WiFi Bluetooth 867Mbps Wireless-AC WiFi + BT 4,0 half Mini PCI-E
- SSD WDC WD10EZEX-21M2NA0 for Windows 10
- SSD TCSUNBOW X3 480GB fow Mac OS Catalina


To do a double boot Windows 10 and Mac OS Catalina you have to install them separately. In other words, you can install each OS in the order you want, but you have to disconnect first the SSD to avoid boot corruptions. I installed first Windows, as an easy task it is. Then, I installed Mac OS Catalina with the SSD but Windows' one disconnected.

Make USB Installer for Mac OS Catalina

You will need:
- 16GB USB or larger
- Mac OS Catalina from App Store (or Software update)
- Clover EFI pkg installer
- Mac computer or hackintosh one

Boot on you Mac or hackintosh, open Disk Utility and format the USB with name "MacOSInstaller" with HFS+ Journaled (Mac OS extended (Journaled)). Open terminal and type the next command:

sudo /Applications/Install\ macOS\ Catalina.app/Contents/Resources/createinstallmedia --volume /Volumes/MacOSInstaller

Keep calm, over 30 minutes until finish job.

Once is done, download the last pkg release from Clover EFI from:

https://github.com/CloverHackyColor/CloverBootloader/releases

Install Clover on the USB with these added options (customize button), rest marked as are:

- ApfsDriverLoader
- AptioInputFix
- AudioDxe
- DataHubDxe
- Fat
- FSInject
- OsxAptioFixDrv
- SMCHelper
- VBoxHfs

Once you have created the USB, copy the kexts I provided to EFI/CLOVER/kexts/Other. First, BIOS specifications:

To access BIOS/UEFI Setup, press and hold Delete on a USB Keyboard while the system is booting up
- Load Optimized Defaults
- Set AHCI for HDD/SSD
- Disable VT-d
- Disable Secure Boot Mode
- Save and exit.

Now, press F12 or access BIOS/UEFI Setup to set boot priority to USB.

Once you have booted from the USB, Clover will appear. You have to select Mac OS Installer, wait a couple of minutes, then the installer will show.

Open Disk Utility and format in HFS+ Jounaled the SSD or HDD. Close it.

Install Mac OS Catalina in the HDD/SSD. Multiple reboots, no matter, boot again from USB and choose Mac OS Installer from Clover.

Once you have installed the OS, boot from USB again to enter Mac OS Catalina. 

Open again and install Clover on the SSD with these added options, rest marked as are:

- ApfsDriverLoader
- AptioInputFix
- AudioDxe
- DataHubDxe
- Fat
- FSInject
- OsxAptioFixDrv
- SMCHelper
- VBoxHfs

DO NOT REBOOT. After installation is complete, you will need to install some kexts (driver in Mac) to make the hardware works. To do so, download the last version of those kexts:

- AppleALC
- Lilu
- WhatEverGreen
- FakeSMC
- USBInjectAll
- IntelMausiEthernet
- FakePCIID
- FakePCIID_Intel_HD_Graphics
- FakePCIID_Broadcom_WiFi
- BrcmPatchRAM2
- BrcmFirmwareData
- BrcmBluetoothInjector
- VoodooPS2Controller

Also, you have to download Clover Configurator (CC). Mount EFI partition, disable SIP and install the kexts in Library/Extensions with Clover Configurator. Now, select the config.plist file from home CC.

In ACPI section, add "change GFX0 to IGPU", "change HECI to IMEI" and "change PEGP to GFX0" patches.

In Boot section, add "dart=0", "nv-disable=1" and "-cdfon" in Arguments subsection.

In Device section, select "Inject", "Add ClockID", "FixOwnership" and "HighCurrent" in USB subsection. Also, in Audio subsection, set to "15" Inject and tick "ResetHDA".

In Rt Variables section, set BooterConfig to "0x28" and CsrActiveConfig to "0x67".

Now, save it and reboot. That's all.

IF YOU WANT TO ADD WINDOWS PARTITION TO CLOVER

Mount EFI.

Go to EFI/BOOT , copy BOOTX64.efi and paste it to EFI/Windows/Boot. Rename it to bootmgfw.efi.

Now, power off the PC, connect the SSD with Windows and enter BIOS configuration. Select First HD Boot to the one where Mac OS is installed, save changes and reboot. That's all.
