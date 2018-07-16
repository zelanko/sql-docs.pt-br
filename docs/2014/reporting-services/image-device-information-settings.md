---
title: Configurações de informações de dispositivo de imagem | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- images [Reporting Services], rendering
- device information settings [Reporting Services], IMAGE rendering
ms.assetid: edad9498-69f7-4726-8699-fa615f704dff
caps.latest.revision: 40
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 17c7a8f084db4c252da7f235762a60078ef39214
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37315466"
---
# <a name="image-device-information-settings"></a>Configurações das informações do dispositivo do Image
  A tabela a seguir lista as configurações de informações de dispositivo para renderização no formato do IMAGE.  
  
|Configuração|Valor|  
|-------------|-----------|  
|**Colunas**|O número de colunas a ser definido para o relatório. Esse valor substitui as configurações originais do relatório.|  
|**ColumnSpacing**|O espaçamento entre colunas a ser definido para o relatório. Esse valor substitui as configurações originais do relatório.|  
|`DpiX`|A resolução horizontal da imagem de saída. O valor padrão é **96**. Aplica-se ao `BMP`, `GIF`, `PNG`, e `TIFF` formatos de saída.|  
|`DpiY`|A resolução vertical da imagem de saída. O valor padrão é **96**. Aplica-se ao `BMP`, `GIF`, `PNG`, e `TIFF` formatos de saída.|  
|**EndPage**|A última página do relatório a ser renderizado. O valor padrão é o valor de `StartPage`.|  
|**MarginBottom**|O valor da margem inferior, em polegadas, a ser definido para o relatório. Você deve incluir um valor inteiro ou decimal seguido de "in" (por exemplo, `1in`). Esse valor substitui as configurações originais do relatório.|  
|**MarginLeft**|O valor da margem esquerda, em polegadas, a ser definido para o relatório. Você deve incluir um valor inteiro ou decimal seguido de "in" (por exemplo, `1in`). Esse valor substitui as configurações originais do relatório.|  
|**MarginRight**|O valor da margem direita, em polegadas, a ser definido para o relatório. Você deve incluir um valor inteiro ou decimal seguido de "in" (por exemplo, `1in`). Esse valor substitui as configurações originais do relatório.|  
|**MarginTop**|O valor da margem superior, em polegadas, a ser definido para o relatório. Você deve incluir um valor inteiro ou decimal seguido de "in" (por exemplo, `1in`). Esse valor substitui as configurações originais do relatório.|  
|**OutputFormat**|Um dos [!INCLUDE[ndptecgdiexpanded](../includes/ndptecgdiexpanded-md.md)] ([!INCLUDE[ndptecgdi](../includes/ndptecgdi-md.md)]) com suporte a formatos de saída: `BMP`, `EMF`, `GIF`, `JPEG`, `PNG`, ou `TIFF`.|  
|**PageHeight**|A altura da página, em polegadas, a ser definida para o relatório. Você deve incluir um valor inteiro ou decimal seguido de "in" (por exemplo, `11in`). Esse valor substitui as configurações originais do relatório.|  
|**PageWidth**|A largura da página, em polegadas, a ser definida para o relatório. Você deve incluir um valor inteiro ou decimal seguido de "in" (por exemplo, `8.5in`). Esse valor substitui as configurações originais do relatório.|  
|**PrintDpiX**|A resolução horizontal da imagem de saída. O valor padrão é `300`. Aplica-se a metarquivo avançado (`EMF`) formato de saída.|  
|**PrintDpiY**|A resolução vertical da imagem de saída. O valor padrão é `300`. Aplica-se a metarquivo avançado (`EMF`) formato de saída.|  
|`StartPage`|A primeira página do relatório a ser renderizada. O valor `0` indica que todas as páginas serão renderizadas. O valor padrão é `1`.|  
  
## <a name="see-also"></a>Consulte também  
 [Passando configurações de informações do dispositivo para extensões de renderização](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar parâmetros de extensão de renderização em RSReportServer.Config](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referência técnica &#40;SSRS&#41;](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
