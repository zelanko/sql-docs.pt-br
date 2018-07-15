---
title: Concluindo o Assistente (Assistente para partições) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitionwizard.finish.f1
ms.assetid: 68a4dd5d-94d9-4a02-be31-949a6da0ef51
caps.latest.revision: 23
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 063863ec6ac25fcc698bbaa5514cf4c578235c66
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37167657"
---
# <a name="completing-the-wizard-partition-wizard"></a>Concluindo o Assistente (Assistente para Partições)
  Use a página **Concluindo o Assistente** para nomear a partição, definir o design de agregação da partição e, opcionalmente, implantar e processar a partição após concluir o Assistente para Partições.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Digite o nome da nova partição. Se estiver trabalhando com várias tabelas, digite o prefixo que será combinado com o nome da tabela para criar cada nome de partição.  
  
 **Opções de agregação**  
 Especifica a opção de agregação da partição.  
  
 A tabela a seguir lista as opções de agregação disponíveis.  
  
|Opção|Description|  
|------------|-----------------|  
|**Criar agregações para a partição agora**|Cria agregações para a nova partição depois que o Assistente para Partições cria a nova partição. A seleção dessa opção inicia o Assistente de Design de Agregação depois que você clica **em Concluir** no Assistente para Partições. Para obter mais informações sobre o Assistente de Design de Agregação, consulte a [Ajuda de F1 do Assistente de Design de Agregação](aggregation-design-wizard-f1-help.md).|  
|**Criar as agregações mais tarde**|Cria a partição sem criar agregações neste momento.|  
|**Copiar o design de agregação de uma partição existente**|Copia o design de agregação de uma partição existente no grupo de medidas para a nova partição. Um clique nesta opção disponibiliza a opção **Copiar de** . Use a opção **Copiar de** para selecionar a partição da qual copiar o design de agregação.<br /><br /> Observe que as partições que podem ser mescladas no futuro devem ter o mesmo design de agregação e a estrutura de tabela. Se você mesclar a nova partição com uma partição existente no grupo de medidas, deverá copiar o design de agregação da partição existente na nova partição.|  
  
 **Implantar e processar agora**  
 Implanta e processa a partição para a instância do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] especificada na página **Locais de Processamento e Armazenamento**. O assistente implanta e processa a partição depois que você clica em **Concluir** nessa página.  
  
## <a name="see-also"></a>Consulte também  
 [Partições &#40;Analysis Services - dados multidimensionais&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  
