---
title: (Caixa de diálogo de propriedades de partição) de cache pró-ativo (SSMS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.partitionproperties.proactivecaching.f1
ms.assetid: ecba72a3-703f-4ede-9d85-9a3318a749e5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cb486ec383ab6fa1684bd9d0e9b8f6bc67631eee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070709"
---
# <a name="proactive-caching-partition-properties-dialog-box-ssms"></a>Cache Pró-ativo (caixa de diálogo Propriedades da Partição) (SSMS)
  Use a página **Cache Pró-ativo** da caixa de diálogo **Propriedades da Partição** no SQL Server Management Studio para definir as propriedades de armazenamento e cache pró-ativo de uma partição em um grupo de medidas para um cubo em um banco de dados do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
## <a name="options"></a>Opções  
 **Configuração padrão**  
 Selecione para habilitar o **controle deslizante Configuração padrão** e usar configurações predefinidas para modo de armazenamento e recursos de cache pró-ativos.  
  
 **Controle deslizante configuração padrão**  
 Defina como uma das configurações predefinidas listadas na tabela a seguir.  
  
|Configuração|Descrição|  
|-------------|-----------------|  
|**ROLAP em tempo real**|Selecione para usar as seguintes configurações de armazenamento e cache pró-ativo:<br /><br /> Modo de armazenamento ROLAP.<br /><br /> Habilita o cache pró-ativo.<br /><br /> Descarta o cache desatualizado com um período de latência de 0 segundos.<br /><br /> Coloca o objeto online imediatamente.|  
|**HOLAP em tempo real**|Selecione para usar as seguintes configurações de armazenamento e cache pró-ativo:<br /><br /> Modo de armazenamento HOLAP.<br /><br /> Habilita o cache pró-ativo.<br /><br /> Descarta o cache desatualizado com um período de latência de 0 segundos.<br /><br /> Atualiza o cache quando os dados são alterados, com um intervalo de silêncio de 0 segundos e sem intervalo de anulação de silêncio.<br /><br /> Coloca o objeto online imediatamente.|  
|**MOLAP de baixa latência**|Selecione para usar as seguintes configurações de armazenamento e cache pró-ativo:<br /><br /> Modo de armazenamento MOLAP.<br /><br /> Habilita o cache pró-ativo.<br /><br /> Descarta o cache desatualizado, com um período de latência de 30 minutos.<br /><br /> Atualiza o cache quando os dados são alterados, com um intervalo de silêncio de 10 segundos e um intervalo de substituição de silêncio de 10 minutos.<br /><br /> Atualiza o cache quando os dados são alterados, com um intervalo de silêncio de 10 segundos e um intervalo de substituição de silêncio de 10 minutos.<br /><br /> Coloca o objeto online imediatamente.|  
|**MOLAP de latência média**|Selecione para useBrings objeto online imediatamente.<br /><br /> as configurações de cache pró-ativo e armazenamento a seguir:<br /><br /> Modo de armazenamento MOLAP.<br /><br /> Habilita o cache pró-ativo.<br /><br /> Descarta o cache desatualizado, com um período de latência de 4 horas.<br /><br /> Atualiza o cache quando os dados são alterados, com um intervalo de silêncio de 10 segundos e um intervalo de substituição de silêncio de 10 minutos.<br /><br /> Coloca o objeto online imediatamente.|  
|**MOLAP automático**|Selecione para usar as seguintes configurações de armazenamento e cache pró-ativo:<br /><br /> Modo de armazenamento MOLAP.<br /><br /> Habilita o cache pró-ativo.<br /><br /> Atualiza o cache quando os dados são alterados, com um intervalo de silêncio de 0 segundos e sem intervalo de anulação de silêncio.|  
|**MOLAP agendado**|Selecione para usar as seguintes configurações de armazenamento e cache pró-ativo:<br /><br /> Modo de armazenamento MOLAP<br /><br /> Habilitar cache pró-ativo<br /><br /> Atualiza o cache periodicamente com um intervalo de reconstrução de 1 dia|  
|**MOLAP**|Selecione para usar as seguintes configurações de armazenamento e cache pró-ativo:<br /><br /> Modo de armazenamento MOLAP.|  
  
 **Configuração personalizada**  
 Selecione para definir explicitamente as opções de modo de armazenamento, cache pró-ativo e notificação.  
  
 **Opções**  
 Clique para exibir a caixa de diálogo **Opções de Armazenamento** para definir explicitamente as opções de modo de armazenamento, cache pró-ativo e notificação. Para obter mais informações sobre a caixa de diálogo **Opções de Armazenamento**, consulte [Caixa de diálogo Opções de Armazenamento &#40;Analysis Services – Dados Multidimensionais&#41;](storage-options-dialog-box-analysis-services-multidimensional-data.md).  
  
## <a name="see-also"></a>Consulte também  
 [Cache pró-ativo &#40;partições&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)   
 [Caixa de diálogo Propriedades de partição &#40;SSMS&#41;](partition-properties-dialog-box-ssms.md)   
 [Seleção de &#40;caixa de diálogo Propriedades de partição&#41; &#40;SSMS&#41;](selection-partition-properties-dialog-box-ssms.md)   
 [Geral &#40;caixa de diálogo Propriedades de partição&#41; &#40;SSMS&#41;](general-partition-properties-dialog-box-ssms.md)   
 [Configuração de erros para cubo, partição e processamento da dimensão &#40;SSAS - Multidimensional&#41;](multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md)  
  
  
