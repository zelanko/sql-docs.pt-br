---
title: Consulta (caixa de diálogo de origem de partição) de detalhes de associação (Analysis Services - dados multidimensionais) | Microsoft Docs
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
- sql12.asvs.cubeeditor.partitions.partitionfilterexpression.f1
ms.assetid: 697874d4-3f7a-4126-96f5-37cc8e2ee306
caps.latest.revision: 20
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7789e99c47f2219d8155eb929a081c5f734a75d9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37194336"
---
# <a name="query-binding-detail-partition-source-dialog-box-analysis-services---multidimensional-data"></a>Detalhes de Associação de Consulta (caixa de diálogo Origem da Partição) (Analysis Services - Dados Multidimensionais)
  Use a opção **Associação de Consulta** na caixa de diálogo **Origem da Partição** para especificar a consulta que fornece os dados para a partição. É possível exibir este painel selecionando **Associação de Consulta** da opção **Tipo de associação** na caixa de diálogo **Origem da Partição** .  
  
## <a name="options"></a>Opções  
 **Fonte de dados**  
 Selecione a fonte de dados na qual a consulta é executada para fornecer dados de fato para a partição.  
  
 **Consulta**  
 Digite ou modifique a instrução SQL usada ao recuperar dados de fato quando a partição é processada.  
  
> [!IMPORTANT]  
>  Ao especificar uma cláusula WHERE, um subconjunto de registros pode ser usado para esta partição. Isso é essencial para evitar duplicação de dados quando várias partições estiverem baseadas em uma única tabela de fatos. Para obter mais informações, consulte a [Partition Source Dialog Box &#40;Analysis Services - Multidimensional Data&#41;](partition-source-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Verificar**  
 Clique para verificar se a instrução em **Consulta** é uma instrução SQL válida.  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo fonte de partição &#40;Analysis Services - dados multidimensionais&#41;](partition-source-dialog-box-analysis-services-multidimensional-data.md)  
  
  
