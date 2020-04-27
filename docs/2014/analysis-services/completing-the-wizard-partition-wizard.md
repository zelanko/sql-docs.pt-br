---
title: Concluindo o assistente (Assistente para partições) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitionwizard.finish.f1
ms.assetid: 68a4dd5d-94d9-4a02-be31-949a6da0ef51
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f7ab4ad7a819c18056ab5901f95caf1b74b23a25
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66087533"
---
# <a name="completing-the-wizard-partition-wizard"></a>Concluindo o Assistente (Assistente para Partições)
  Use a página **Concluindo o Assistente** para nomear a partição, definir o design de agregação da partição e, opcionalmente, implantar e processar a partição após concluir o Assistente para Partições.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Digite o nome da nova partição. Se estiver trabalhando com várias tabelas, digite o prefixo que será combinado com o nome da tabela para criar cada nome de partição.  
  
 **Opções de agregação**  
 Especifica a opção de agregação da partição.  
  
 A tabela a seguir lista as opções de agregação disponíveis.  
  
|Opção|Descrição|  
|------------|-----------------|  
|**Criar agregações para a partição agora**|Cria agregações para a nova partição depois que o Assistente para Partições cria a nova partição. A seleção dessa opção inicia o Assistente de Design de Agregação depois que você clica **em Concluir** no Assistente para Partições. Para obter mais informações sobre o Assistente de Design de Agregação, consulte a [Ajuda de F1 do Assistente de Design de Agregação](aggregation-design-wizard-f1-help.md).|  
|**Criar as agregações mais tarde**|Cria a partição sem criar agregações neste momento.|  
|**Copiar o design de agregação de uma partição existente**|Copia o design de agregação de uma partição existente no grupo de medidas para a nova partição. Um clique nesta opção disponibiliza a opção **Copiar de** . Use a opção **Copiar de** para selecionar a partição da qual copiar o design de agregação.<br /><br /> Observe que as partições que podem ser mescladas no futuro devem ter a mesma estrutura de tabela e design de agregação. Se você mesclar a nova partição com uma partição existente no grupo de medidas, deverá copiar o design de agregação da partição existente na nova partição.|  
  
 **Implantar e Processar Agora**  
 Implanta e processa a partição para a instância do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] especificada na página **Locais de Processamento e Armazenamento** . O assistente implanta e processa a partição depois que você clica em **Concluir** nessa página.  
  
## <a name="see-also"></a>Consulte Também  
 [Partições &#40;Analysis Services – Dados Multidimensionais&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  
