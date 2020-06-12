---
title: Geral (caixa de diálogo opções de armazenamento) (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitiondesigner.partitionstoragesettings.setstorageoptions.storage.f1
ms.assetid: ee1fac79-ae15-4c3c-9a98-33db04388817
author: minewiskan
ms.author: owend
ms.openlocfilehash: f67e3f7a3c9d84c8095286707c3dd6ce2c22c3bd
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544388"
---
# <a name="general-storage-options-dialog-box-analysis-services---multidimensional-data"></a>Geral (caixa de diálogo Opções de Armazenamento) (Analysis Services - Dados Multidimensionais)
  Use a caixa de diálogo **Geral** da caixa de diálogo **Opções de Armazenamento** do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para definir configurações de modo de armazenamento e cache pró-ativo para uma dimensão, cubo, grupo de medidas ou partição.  
  
> [!NOTE]  
>  Você deve estar familiarizado com a funcionalidade de modo de armazenamento e de cache pró-ativo para modificar essas configurações. Para obter mais informações, consulte [Cache pró-ativo &#40;Partições&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
## <a name="options"></a>Opções  
  
|Termo|Definição|  
|----------|----------------|  
|**Modo de armazenamento**|Seleciona o modo de armazenamento a ser usado para o objeto.<br /><br /> **MOLAP**<br /> O objeto usa armazenamento MOLAP (OLAP multidimensional).<br /><br /> **HOLAP**<br /> O objeto usa armazenamento HOLAP (OLAP híbrido).<br /><br /> **ROLAP**<br /> O objeto usa armazenamento ROLAP (OLAP relacional).|  
|**Habilitar cache pró-ativo**|Habilita o cache pró-ativo.<br /><br /> Observação: se essa opção não estiver selecionada, todas as opções, exceto **Modo de armazenamento** , estarão desabilitadas.|  
|**Atualizar o cache quando os dados forem alterados**|Usa o método de notificação selecionado na guia **Notificações** para atualizar a imagem MOLAP do objeto sempre que uma notificação for recebida. Para obter mais informações sobre a guia **notificações** , consulte [caixa de diálogo notificações &#40;opções de armazenamento&#41; &#40;Analysis Services de dados multidimensionais&#41;](notifications-storage-options-dialog-analysis-services-multidimensional-data.md).<br /><br /> Observação: essa opção estará desabilitada a menos que a opção **Habilitar cache pró-ativo** esteja selecionada.|  
|**Intervalo de silêncio**|Define o intervalo mínimo e unidades de tempo no qual o objeto não tem atividades antes do cache pró-ativo começar a criar a nova imagem MOLAP para o objeto.<br /><br /> Observação: essa opção estará desabilitada a menos que **Atualizar o cache quando os dados forem alterados** esteja selecionada.|  
|**Intervalo de substituição de silêncio**|Define o intervalo máximo e unidades de tempo no qual, após uma notificação ser recebida para o objeto, o cache pró-ativo começa a criar a nova imagem MOLAP para o objeto, independentemente da atividade atual do objeto. Notificações recebidas depois que esse intervalo foi atingido não cancelam o processo de imagem MOLAP disparado por esse intervalo.<br /><br /> Observação: essa opção estará desabilitada a menos que **Atualizar o cache quando os dados forem alterados** esteja selecionada. Observe também que essa opção não deve ser definida se o **modo de armazenamento** estiver definido como **HOLAP**.|  
|**Descartar cache desatualizado**|Especifica o período entre o início da criação de um novo cache MOLAP e a remoção do cache MOLAP existente.<br /><br /> Observação: essa opção estará desabilitada a menos que a opção **Habilitar cache pró-ativo** esteja selecionada. Observe também que essa opção não deve ser definida se o **modo de armazenamento** estiver definido como HOLAP.|  
|**Latency**|Seleciona o intervalo e as unidades de tempo do período entre o início da criação de um novo cache MOLAP e a remoção do cache MOLAP existente.<br /><br /> Observação: essa opção estará desabilitada a menos que a opção **Descartar cache desatualizado** esteja selecionada. Observe também que essa opção não deve ser definida se o **modo de armazenamento** estiver definido como **HOLAP**.|  
|**Atualizar o cache periodicamente**|Atualiza a imagem MOLAP regularmente, independentemente da notificação.<br /><br /> Observação: essa opção estará desabilitada a menos que a opção **Habilitar cache pró-ativo** esteja selecionada. Observe também que essa opção não deve ser definida se o **modo de armazenamento** estiver definido como **HOLAP**.|  
|**Intervalo de recriação**|Seleciona o intervalo e as unidades de tempo para o período que, depois que uma nova imagem MOLAP é criada, [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] inicia o processo de imagem MOLAP novamente para o objeto, independentemente da notificação. Notificações recebidas depois que esse intervalo foi atingido não cancelam o processo de imagem MOLAP disparado por esse intervalo.<br /><br /> Observação: essa opção estará desabilitada a menos que a opção **Atualizar o cache periodicamente** esteja selecionada. Observe também que essa opção não deve ser definida se o **modo de armazenamento** estiver definido como **HOLAP**.|  
|**Colocar online imediatamente**|Coloca os objetos online imediatamente. Se essa opção estiver definida, os objetos usarão o armazenamento ROLAP subjacente para resolver consultas enquanto o cache MOLAP estiver sendo recriado. Se essa opção não estiver definida, os objetos serão colocados online apenas após o cache MOLAP ser concluído.|  
|**Habilitar agregações ROLAP**|Usa exibições materializadas na fonte de dados subjacente para armazenar agregações.<br /><br /> Observação: se a fonte de dados subjacente não der suporte a exibições materializadas, ocorrerá um erro quando o objeto for processado.|  
|**Aplicar configurações a dimensões**|Aplica configurações de modo de armazenamento e de cache pró-ativo a dimensões associadas.|  
  
## <a name="see-also"></a>Consulte Também  
 [Caixa de diálogo opções de armazenamento &#40;Analysis Services de dados multidimensionais&#41;](storage-options-dialog-box-analysis-services-multidimensional-data.md)   
 [Caixa de diálogo notificações &#40;opções de armazenamento&#41; &#40;Analysis Services de dados multidimensionais&#41;](notifications-storage-options-dialog-analysis-services-multidimensional-data.md)  
  
  
