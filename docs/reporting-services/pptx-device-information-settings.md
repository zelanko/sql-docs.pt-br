---
title: "Configurações de informações do dispositivo PPTX | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 09/11/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- render
- powerpoint
- pptx
- export
ms.assetid: 4dc2045f-8025-41a3-8f9d-5635fb24cf4a
caps.latest.revision: 6
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3aa67165e961e76569daadff1fc610c4d16a1e63
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="pptx-device-information-settings"></a>Configurações de informações do dispositivo PPTX
  A tabela a seguir lista as configurações de informações de dispositivo para a renderização de relatórios [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no formato PPTX.  
  
|Configuração|Value|  
|-------------|-----------|  
|**Colunas**|O número de colunas a ser definido para o relatório. Esse valor substitui as configurações originais do relatório.|  
|**ColumnSpacing**|O espaçamento entre colunas a ser definido para o relatório. Esse valor substitui as configurações originais do relatório.|  
|**DpiX**|A resolução horizontal da imagem de saída. O valor padrão é **96**. Aplica-se aos formatos de saída **BMP**, **GIF**, **PNG**e **TIFF** .|  
|**DpiY**|A resolução vertical da imagem de saída. O valor padrão é **96**. Aplica-se aos formatos de saída **BMP**, **GIF**, **PNG**e **TIFF** .|  
|**EndPage**|A última página do relatório a ser renderizado. O valor padrão é o valor de **StartPage**.|  
|**MarginBottom**|O valor da margem inferior, em polegadas, a ser definido para o relatório. Inclua um valor inteiro ou um decimal seguido de "in" (por exemplo, **1in**). Esse valor substitui as configurações originais do relatório.|  
|**MarginLeft**|O valor da margem esquerda, em polegadas, a ser definido para o relatório. Inclua um valor inteiro ou um decimal seguido de "in" (por exemplo, **1in**). Esse valor substitui as configurações originais do relatório.|  
|**MarginRight**|O valor da margem direita, em polegadas, a ser definido para o relatório. Inclua um valor inteiro ou um decimal seguido de "in" (por exemplo, **1in**). Esse valor substitui as configurações originais do relatório.|  
|**MarginTop**|O valor da margem superior, em polegadas, a ser definido para o relatório. Inclua um valor inteiro ou um decimal seguido de "in" (por exemplo, **1in**). Esse valor substitui as configurações originais do relatório.|  
|**PageHeight**|A altura da página, em polegadas, a ser definida para o relatório. Inclua um valor inteiro ou um decimal seguido de "in" (por exemplo, **11in**). Esse valor substitui as configurações originais do relatório.|  
|**PageWidth**|A largura da página, em polegadas, a ser definida para o relatório. Inclua um valor inteiro ou um decimal seguido de "in" (por exemplo, **8,5in**). Esse valor substitui as configurações originais do relatório.|  
|**StartPage**|A primeira página do relatório a ser renderizada. O valor **0** indica que todas as páginas serão renderizadas. O valor padrão é **1**.|  
|**UseReportPageSize**|Se UseReportPageSize =**false** , o tamanho do slide padrão é o padrão do PowerPoint de 13,333” x 7,5” (taxa de proporção de 16:9). Se UseReportPageSize = true, o tamanho do slide padrão é o tamanho da página definido do relatório.<br /><br /> O valor padrão é **false**<br /><br /> Observação: as configurações PageWidth e PageHeight substituem a largura e a altura padrão.|  
  
## <a name="see-also"></a>Consulte também  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Passando configurações de informações de dispositivos para extensões de renderização](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar parâmetros de extensão de renderização em RSReportServer.config](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referência técnica &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  

