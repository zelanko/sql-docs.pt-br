---
title: Configurações de informações de dispositivo MHTML | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- device information settings [Reporting Services], MHTML rendering
- MHTML [Reporting Services]
ms.assetid: 60b85dd8-b4fb-4ad9-be6a-e7c89ac076fe
caps.latest.revision: 39
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 7eb07733e9db0a1002658cd1e29de02d95d8ad08
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36005458"
---
# <a name="mhtml-device-information-settings"></a>Configurações das informações do dispositivo MHTML
  A tabela a seguir lista as configurações de informações de dispositivo para a renderização de relatórios no arquivo da Web (MHTML).  
  
|Configuração|Valor|  
|-------------|-----------|  
|**JavaScript**|Indica se JavaScript é compatível com o relatório renderizado.|  
|**OutlookCompat**|Indica se ocorrerá renderização com metadados extras que melhoram a aparência do relatório no Outlook. O valor padrão é `true`.|  
|**Fragmento de MHTML**|Indica se um fragmento de MHTML é criado no lugar de um documento MHTML completo. Um fragmento de MHTML inclui o conteúdo do relatório em um elemento TABLE e omite os elementos HTML e BODY. O valor padrão é `false`.|  
|**DataVisualizationFitSizing**|Indica comportamento de ajuste de visualização de dados quando dentro de um tablix. Isso inclui gráfico, medidor e mapa.<br /><br /> Os valores possíveis são **Aproximado** e **Exato**.<br /><br /> O valor padrão é **Aproximado**. Se a configuração for removida do arquivo **rsreportserver.config** , o comportamento padrão será **Exato**.<br /><br /> Habilitar **Exato** pode ter impacto de desempenho porque o processamento para determinar o tamanho exato pode levar mais tempo.|  
  
## <a name="see-also"></a>Consulte também  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Passando configurações de informações de dispositivos para extensões de renderização](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar parâmetros de extensão de renderização em RSReportServer.Config](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referência técnica &#40;SSRS&#41;](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  