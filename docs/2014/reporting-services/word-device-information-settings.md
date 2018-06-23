---
title: Configurações de informações de dispositivo do Word | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Word [Reporting Services]
- device information settings [Reporting Services], Word
ms.assetid: 28146498-fae7-4b13-b47f-6ec05aa8e057
caps.latest.revision: 8
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 5b31b3c3ea0cf5b70967ca099e0b979f0c929334
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115351"
---
# <a name="word-device-information-settings"></a>Configurações de informações de dispositivo do Word
  A tabela a seguir lista as configurações de informações de dispositivo para renderização no formato [!INCLUDE[ofprword](../includes/ofprword-md.md)] .  
  
|Configuração|Valor|  
|-------------|-----------|  
|`AutoFit`|`False`. O AutoAjuste é definido como `false` em qualquer tabela do Word.<br /><br /> `True`. O AutoAjuste é definido como `true` em todas as tabelas do Word.<br /><br /> `Never`. Os valores do AutoAjuste não são definidos em qualquer tabela do Word e seu comportamento volta para o padrão do Word.<br /><br /> `Default`. O AutoAjuste é definido em tabelas mais estreitas do que a área de desenho física (largura de página física excluindo as margens) por página lógica.|  
|`ExpandToggles`|Indica se todos os itens que podem ser alternados deve ser renderizados em seu estado totalmente expandido. O valor padrão é `false`.|  
|`FixedPageWidth`|Indica se a Largura de Página escrita para o arquivo DOC crescerá para acomodar a largura da maior página do Corpo do Relatório. O valor padrão é `false`.|  
|**OmitHyperlinks**|Indica se a ação Hiperlink deverá ser omitida em todos os itens onde for definida. O valor padrão é `false`|  
|`OmitDrillthroughs`|Indica se a ação Drillthrough deverá ser omitida em todos os itens onde foi definida. O valor padrão é `false`|  
  
## <a name="see-also"></a>Consulte também  
 [Passando configurações de informações de dispositivos para extensões de renderização](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar parâmetros de extensão de renderização em RSReportServer.Config](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referência técnica &#40;SSRS&#41;](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  