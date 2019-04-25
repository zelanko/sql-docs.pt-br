---
title: Caixa de diálogo de configurações de armazenamento (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitiondesigner.partitionstoragesettings.f1
- sql12.asvs.cubeeditor.cubebuilder.measuregroupstoragesettings.f1
ms.assetid: 80c41c71-226c-45fe-b9cf-af824b592fe1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8e93c341a73d55094624f3930934076f10674bce
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62758486"
---
# <a name="storage-settings-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Configurações de Armazenamento (Analysis Services - Dados Multidimensionais)
  Use a caixa de diálogo **Configurações de Armazenamento** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para definir configurações de cache pró-ativo, armazenamento e notificação para uma dimensão, cubo, grupo de medidas ou partição. É possível exibir a caixa de diálogo **Configurações de Armazenamento** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] da seguinte maneira:  
  
-   Clicar no botão de reticências (**...** ) para o `ProactiveCaching` valor da propriedade de uma dimensão, cubo, grupo de medidas ou partição no **Properties** janela de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
-   Expandindo um grupo de medidas na guia **Partições** do **Designer de Cubo** e clicando em **Configurações de Armazenamento**.  
  
-   Expandindo um grupo de medidas e selecionando uma partição na grade daquele grupo de medidas na guia **Partições** do **Designer de Cubo** e clicando em **Configurações de Armazenamento**.  
  
-   Expandindo um grupo de medidas e selecionando uma partição na grade daquele grupo de medidas na guia **Partições** do **Designer de Cubo** e clicando em **Configurações de armazenamento** no painel **Barra de Ferramentas** da guia **Partições** do **Designer de Cubo**.  
  
## <a name="options"></a>Opções  
  
|Termo|Definição|Valores|  
|----------|----------------|------------|  
|**Configuração padrão**|Selecione para habilitar o **controle deslizante Configuração padrão** e usar configurações predefinidas para modo de armazenamento e recursos de cache pró-ativos.||  
|**Controle deslizante configuração padrão**|Defina como uma das seguintes configurações predefinidas:<br /><br /> **ROLAP em tempo real**<br /><br /> Selecione para usar as seguintes configurações de armazenamento e cache pró-ativo:|Modo de armazenamento ROLAP<br /><br /> Habilita o cache pró-ativo<br /><br /> Descarta o cache desatualizado com um período de latência de 0 segundos<br /><br /> Coloca o objeto online imediatamente|  
||**HOLAP em tempo real**<br /><br /> Selecione para usar as seguintes configurações de armazenamento e cache pró-ativo:|Modo de armazenamento HOLAP<br /><br /> Habilita o cache pró-ativo<br /><br /> Descarta o cache desatualizado com um período de latência de 0 segundos<br /><br /> Atualiza o cache quando os dados são alterados, com um intervalo de silêncio de 0 segundos e um intervalo de substituição de não silêncio<br /><br /> Coloca o objeto online imediatamente|  
||**MOLAP de baixa latência**<br /><br /> Selecione para usar as seguintes configurações de armazenamento e cache pró-ativo:|Modo de armazenamento MOLAP<br /><br /> Habilita o cache pró-ativo<br /><br /> Descarta o cache desatualizado com um período de latência de 30 minutos<br /><br /> Atualiza o cache quando os dados são alterados com um intervalo de silêncio de 10 segundos e um intervalo de substituição de silêncio de 10 minutos<br /><br /> Coloca o objeto online imediatamente|  
||**MOLAP de latência média**<br /><br /> Selecione para usar as seguintes configurações de armazenamento e cache pró-ativo:|Modo de armazenamento MOLAP<br /><br /> Habilita o cache pró-ativo<br /><br /> Descarta o cache desatualizado com um período de latência de 4 horas<br /><br /> Atualiza o cache quando os dados são alterados com um intervalo de silêncio de 10 segundos e um intervalo de substituição de silêncio de 10 minutos<br /><br /> Coloca o objeto online imediatamente|  
||**MOLAP automático**<br /><br /> Selecione para usar as seguintes configurações de armazenamento e cache pró-ativo:|Modo de armazenamento MOLAP<br /><br /> Habilita o cache pró-ativo<br /><br /> Atualiza o cache quando os dados são alterados, com um intervalo de silêncio de 0 segundos e um intervalo de substituição de não silêncio|  
||**MOLAP agendado**<br /><br /> Selecione para usar as seguintes configurações de armazenamento e cache pró-ativo:|Modo de armazenamento MOLAP<br /><br /> Habilitar cache pró-ativo<br /><br /> Atualiza o cache periodicamente com um intervalo de reconstrução de 1 dia|  
||**MOLAP**<br /><br /> Selecione para usar as seguintes configurações de armazenamento e cache pró-ativo:|Modo de armazenamento MOLAP|  
|**Configuração personalizada**|Selecione para definir explicitamente as opções de modo de armazenamento, cache pró-ativo e notificação.||  
|**Opções**|Clique para exibir a caixa de diálogo **Opções de Armazenamento** para definir explicitamente as opções de modo de armazenamento, cache pró-ativo e notificação. Para obter mais informações sobre a caixa de diálogo **Opções de Armazenamento**, consulte [Caixa de diálogo Opções de Armazenamento &#40;Analysis Services – Dados Multidimensionais&#41;](storage-options-dialog-box-analysis-services-multidimensional-data.md).||  
  
## <a name="see-also"></a>Consulte também  
 [Designers e caixas de diálogo do Analysis Services &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Cache pró-ativo &#40;partições&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)   
 [Armazenamento de cubo &#40;Analysis Services - dados multidimensionais&#41;](multidimensional-models-olap-logical-cube-objects/cube-storage-analysis-services-multidimensional-data.md)  
  
  
