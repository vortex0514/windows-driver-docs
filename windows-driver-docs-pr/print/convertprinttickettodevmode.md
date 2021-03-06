---
title: ConvertPrintTicketToDevMode
author: windows-driver-content
description: ConvertPrintTicketToDevMode
MS-HAID:
- 'drvarch\_41a9430f-d630-4158-9cb9-97afc671b868.xml'
- 'print.convertprinttickettodevmode'
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: dd77d79e-e274-47c3-9bfd-95054bc9f23d
keywords: ["ConvertPrintTicketToDevMode"]
---

# ConvertPrintTicketToDevMode


Unidrv and PScript5 print drivers fill in the public and private parts of the [**DEVMODEW**](https://msdn.microsoft.com/library/windows/hardware/ff552837) structure that they support by using the information from the Print Ticket that was passed in the application's call to ConvertPrintTicketToDevMode. The [**IPrintOemPrintTicketProvider::ConvertPrintTicketToDevMode**](https://msdn.microsoft.com/library/windows/hardware/ff553167) method is called for each print driver plug-in that was installed.

The following illustration shows the order of the calls to IPrintOemPrintTicketProvider::ConvertPrintTicketToDevMode when the driver callsConvertPrintTicketToDevMode.

![diagram illustrating the convertprinttickettodevmode calling sequence](images/ptpcpt2dm-uml.gif)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bprint\print%5D:%20ConvertPrintTicketToDevMode%20%20RELEASE:%20%289/1/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


