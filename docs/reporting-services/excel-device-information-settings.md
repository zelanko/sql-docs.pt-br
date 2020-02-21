---
title: Configurações de informações de dispositivo Excel | Microsoft Docs
ms.date: 01/23/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], Excel rendering
- Excel [Reporting Services], rendering
ms.assetid: bb5f3566-f033-4470-be87-1f52fb7a4ab6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7a83bcd79a50400888d5a973ad9a743db19b87b5
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "76761820"
---
# <a name="excel-device-information-settings"></a>Configurações das informações do dispositivo do Excel
  A tabela a seguir lista as configurações de informações de dispositivo para renderização no formato [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] .  
  
|Configuração|Valor|  
|-------------|-----------|  
|**OmitDocumentMap**|Indica se será preciso omitir o mapa do documento para relatórios que dão suporte a ele. O valor padrão é **false**.|  
|**OmitFormulas**|Indica se será preciso omitir fórmulas a partir do relatório renderizado. O valor padrão é **false**.|  
|**SimplePageHeaders**|Indica se o cabeçalho de página do relatório será renderizado para o cabeçalho de página do Excel. Um valor **false** indica que o cabeçalho de página será renderizado para a primeira linha da planilha. O valor padrão é **false**.|  
|**DynamicImageDpi**|A resolução de imagens dinâmicas, como gráficos, medidores e mapas. O valor padrão é **96**. (Disponível no Servidor de Relatórios do Power BI (janeiro de 2020) e mais recente)|  

  
## <a name="see-also"></a>Consulte Também  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Passando configurações de informações de dispositivos para extensões de renderização](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar parâmetros de extensão de renderização em RSReportServer.Config](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referência técnica &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
