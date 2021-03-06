---
title: V4 Driver UI Architecture
author: windows-driver-content
description: A high level design goal for the v4 driver architecture was to provide built-in support for the Windows Store app user interface.
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: 6318E480-C567-4866-8E88-B19904408C59
---

# V4 Driver UI Architecture


A high level design goal for the v4 driver architecture was to provide built-in support for the Windows Store app user interface.

The application-based UI paradigm that is employed is a clear example of this. Windows Store device apps provide users with a full screen experience that is supported in the Windows Store app UI. Windows Store device apps for printing provide extensibility for print preferences, and printer notifications for printers that support the v4 print driver. Windows Store device apps for printing also provide visibility for the print device on the new Start screen.

Printer extension apps support print preferences and printer notifications when users run existing applications on the Windows desktop. While the UIs for these applications are very different, with one tailored for touch and the other optimized for mouse and keyboard users, the business logic and the connection to v4 print drivers can still be similar, regardless of the UI.

The following diagram shows a high level architecture of the Windows Store device apps for printing and printer extension samples that are provided in the [Windows Sample Gallery](http://code.msdn.microsoft.com/).

![overview of custom ui architecture](images/v4custuiarch.png)

As shown in the preceding diagram, the model/view/controller-based architecture enables the apps to share code at the model layer, written in C#.

**Extending PrinterExtensionLibrary**

The PrinterExtensionLibrary project that ships in the various samples can be extended using new classes, or by extending the provided set of classes. Since Microsoft periodically makes updates to the sample code, we recommend that partners should minimize the number of code changes that they make to the provided source files. For partners that are extending the provided set of classes, we recommend that you mark the existing classes as “partial” and add new functions or overrides in a separate source file.

**Sharing compiled binaries between Windows Store apps and Desktop apps**

The PrinterExtensionLibrary project that is shipped in the Windows Store device app and printer extension samples utilizes the same source code, but it may be valuable to build the code so it is portable between the projects without being built separately for each project. To make the code for the PrinterExtensionLibrary project portable, you have to convert the project to a Portable Class Library. Perform the following steps to make the conversion.

1. In Microsoft Visual Studio, click **File** &gt; **New** &gt; **Project**, and then search for "Portable" in the **Search Installed Templates** box.

2. Select Portable Class Library Visual C#, and then provide a name for the project in the **Name** text box and click **OK.**

3. Copy the source code from your existing PrinterExtensionLibrary project into the new project.

4. Right-click your Portable Class Library project and choose **Unload**. Then open the .csproj file and add the following section to your file, just prior to the last tag in the document.

```XML
  <ItemGroup>
    <COMReference Include="PrinterExtensionLib">
      <Guid>{91CE54EE-C67C-4B46-A4FF-99416F27A8BF}</Guid>
      <VersionMajor>1</VersionMajor>
      <VersionMinor>0</VersionMinor>
      <Lcid>0</Lcid>
      <WrapperTool>tlbimp</WrapperTool>
      <Isolated>False</Isolated>
      <EmbedInteropTypes>True</EmbedInteropTypes>
    </COMReference>
  </ItemGroup>
```

5. If you see warnings as a result of COM references, add the following to the &lt;PropertyGroup&gt; tag:

```XML
<ResolveComReferenceSilent>true</ResolveComReferenceSilent>
```

**API for print UI scenarios**

An API has been developed as part of the v4 print driver model to support Printer Extensions and Windows Store device apps for printing. At a high level, the print preferences scenario uses PrintTicket, PrintCapabilities and the new property bags to get and store all of its information. Printer notifications are driven by a new eventing system that is based on the Bidirectional Communication (Bidi) Schema, and this new system uses the AsyncUI protocol between client and server. The data-centric nature of this API means that one application could easily support many devices.

Printer extensions need to be built in such a way that they can gracefully degrade if the requested data is unavailable. For example, if a particular PrintCapabilities feature is unavailable, or if a property in one of the property bags is unavailable, this should not prevent the rest of the app from functioning. When accessing property bags, or specific properties in a property bag, the app should use the try-catch syntax in order to ensure that any exceptions that are thrown do not cause the app to crash. For more information, see [Printer Extension Interfaces](https://msdn.microsoft.com/library/windows/hardware/hh463984).

## Related topics
[Printer Extension Interfaces](https://msdn.microsoft.com/library/windows/hardware/hh463984)  
[Windows Sample Gallery](http://code.msdn.microsoft.com/)  

--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bprint\print%5D:%20V4%20Driver%20UI%20Architecture%20%20RELEASE:%20%289/1/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


