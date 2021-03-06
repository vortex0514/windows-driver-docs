---
title: Patching a DMA Buffer
description: Patching a DMA Buffer
ms.assetid: 4d8a8a89-0617-4ab8-8609-37bbdb8999f0
keywords: ["DMA buffers WDK display , patching", "patching DMA buffers WDK display"]
---

# Patching a DMA Buffer


## <span id="ddk_patching_a_dma_buffer_gg"></span><span id="DDK_PATCHING_A_DMA_BUFFER_GG"></span>


After the video memory manager is informed where every memory resource for the DMA buffer is located, the GPU scheduler calls the display miniport driver's [**DxgkDdiPatch**](https://msdn.microsoft.com/library/windows/hardware/ff559737) function to patch the resource with a physical address (that is, assign a physical address to the resource).

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[display\display]:%20Patching%20a%20DMA%20Buffer%20%20RELEASE:%20%282/10/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




