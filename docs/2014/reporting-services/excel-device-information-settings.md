---
title: Configurações de informações de dispositivo Excel | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], Excel rendering
- Excel [Reporting Services], rendering
ms.assetid: bb5f3566-f033-4470-be87-1f52fb7a4ab6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5d1ec9b650592be41c8ae2f7043649c91ea78442
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63164570"
---
# <a name="excel-device-information-settings"></a>Configurações das informações do dispositivo do Excel
  A tabela a seguir lista as configurações de informações de dispositivo para renderização no formato [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] .  
  
|Configuração|Valor|  
|-------------|-----------|  
|**OmitDocumentMap**|Indica se será preciso omitir o mapa do documento para relatórios que dão suporte a ele. O valor padrão é `false`.|  
|**OmitFormulas**|Indica se será preciso omitir fórmulas a partir do relatório renderizado. O valor padrão é `false`.|  
|`SimplePageHeade`rs|Indica se o cabeçalho de página do relatório será renderizado para o cabeçalho de página do Excel. Um valor `false` indica que o cabeçalho de página será renderizado para a primeira linha da planilha. O valor padrão é `false`.|  
  
## <a name="see-also"></a>Consulte também  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Passando configurações de informações de dispositivos para extensões de renderização](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar parâmetros de extensão de renderização em RSReportServer.config](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referência técnica &#40;SSRS&#41;](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
