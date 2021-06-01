## What is a SDD?
==SSD== (solid state drive) is a storage device that uses ==integrated circuit assemblies to store data persistently==, typically using ==flash memory==.

Compared with electromechanical dirves, SSDs are more typically resistant to physical shock, run silently, and have ==quicker access time and lower latency==. SSDs store data in semiconductor cells. SSD storage devices ==vary== in their properties ==according to the number of bits stored in each cell==, with single-bit cells ("SLC") being generally the most reliable, durable, fast, and expensive type, compared with 2- and 3-bit cells ("MLC" and "TLC"), and finally quad-bit cells ("QLC") being used for consumer devices that do not require such extreme properties and are the cheapest of the four.

==Hybrid drives== or solid-state hybrid drives (SSHDs), such as *Apple's Fusion Drive*, ==combine== features of SSDs and HDDs in the same unit using ==both flash memory and a HDD== in order to ==improve the performance of frequently-accessed data==.

They are used instead of (or alongside) a hard drive.
## Sizes (form factors) of different SSDs
#### _2.5 inch SSD_
They are the ==most common== type. They are typically ==used in desktops, servers and storage systems built== around hard disk drives (HDD). They have the same size and shape as a 2.5 inch mechanical hard drive.
![[Pasted image 20201129140739.png]]
**How to install a 2.5" SATA SSD in a desktop PC?**
1. Turn off your PC
2. Locate the SATA port
3. If you are using a 2.5" drive bay, detach the mounting bracket, attach the SSD by aligning the mounting screw holes on the bracket with the holes on the SSD and mount the SSD in the drive bay
4. If you are using a 3.5" drive bay, detach the mounting bracket, attach the SSD by aligning the mounting screw holes on the bracket with the holes on the SSD. Locate an available 3.5" drive bay inside the desktop and install the SSD
5. Attach one end of the SATA cable to the SSD and the other end to the SATA connector on the motherboard
6. Use the SATA power cable that is connected to the power supply and attach it to the SSD
7. Plug the power cable and boot up the system
8. Use a tool (disk management for Windows) to allocate the new installed storage
#### _M.2 SSD (defined in 2013)_
M.2 is a form factor specification for ==internally mounted== SSDs. Formerly known as **Next Generation Form Factor** (NGFF). They have ==keying notches== on the edge connector to ==designate various interface or PCIe lane configurations== (M.2 SSDs can be "B", "M", or "B&M" keyed). They are all removable, except Type 1620 that's typically mounted on the main system board. They come in a variety of sizes expressed as code.
_Examples_: 
- _2280 M.2 device is 22mm × 80mm_ used in laptop, PC, Server or Hyperscale date, Server boot
- _2260 M.2 device is 22mm × 60mm_
- 1620 used in mobile, tablet and laptop
- 1630
- 2230 used in mobile, tablet, laptop, PC boot, Server boot
- 3030
- 2242
- 3042
- 22110 used in PC boot and Data, Server or Hypersclae data

![[Pasted image 20201129140842.png]]
![[Pasted image 20201129141155.png]]
Note: there are adapters that allow pluging a M.2 SSD into a PCIe slot
#### _3.5 inch SSD_
![[Pasted image 20201129141541.png]]
#### _mSATA SSD_
![[Pasted image 20201129141815.png]]
#### _AIC SSD (add-in card SSD)_
It plugs directly into a PCIe slot on a computer's motherboard. It also comes in different sizes such as HH/HL (half-height half-length) & FH/HL (full-height half-length)
![[Pasted image 20201129141905.png]]
## Interfaces
#### SATA (serial advances technology attachement)
It delivers a maximum speed of around 550 MB/s 
#### NVMe (non-volatile memory express)
A **PCIe (peripheral component interconnect express)** SSD standard (a standard for connecting SSDs via PCIe). It delivers up to 7000 MB/s for the latest drives connected to computers with a PCIe 4.0
_**Note**: SSD's form factor doesn't determine its interface_
_**Note**: Some 2.5 inch SSDs have a SAS (serial attached SCSI) interface that can provide data transfer speed up to 1200 MB/s_
_**Note**: there are motherboards that support only SATA or NVMI_
#### Important note
All M.2 devices have slots (keys) to prevent them being fitted into the wrong king of M.2 slot (M.2 SSDs can be "B", "M", or "B&M" keyed)

| Form Factor | Available Interfaces |
| ------------  | --------------------- |
| 2.5 inch | SATA, U.2 (PCIe NVMe) or SAS |
| M.2 | SATA or PCIe NVMe |
| AIC | PCIe NVMe |
| mSATA | SATA|
## Technologies
