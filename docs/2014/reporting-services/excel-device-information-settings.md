---
title: Configurações de informações de dispositivo Excel | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], Excel rendering
- Excel [Reporting Services], rendering
ms.assetid: bb5f3566-f033-4470-be87-1f52fb7a4ab6
caps.latest.revision: 40
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 8d5da4ae14517e7b2f1ed21d558d4854b664c90f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37170237"
---
# <a name="excel-device-information-settings"></a>Configurações das informações do dispositivo do Excel
  A tabela a seguir lista as configurações de informações de dispositivo para renderização no formato [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] .  
  
|Configuração|Valor|  
|-------------|-----------|  
|**OmitDocumentMap**|Indica se será preciso omitir o mapa do documento para relatórios que dão suporte a ele. O valor padrão é `false`.|  
|**OmitFormulas**|Indica se será preciso omitir fórmulas a partir do relatório renderizado. O valor padrão é `false`.|  
|`SimplePageHeade`RS|Indica se o cabeçalho de página do relatório será renderizado para o cabeçalho de página do Excel. Um valor de `false` indica que o cabeçalho da página será renderizado para a primeira linha da planilha. O valor padrão é `false`.|  
  
## <a name="see-also"></a>Consulte também  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Passando configurações de informações do dispositivo para extensões de renderização](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar parâmetros de extensão de renderização em RSReportServer.Config](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referência técnica &#40;SSRS&#41;](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
