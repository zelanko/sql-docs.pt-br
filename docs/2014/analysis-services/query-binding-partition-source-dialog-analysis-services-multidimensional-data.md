---
title: Consulta (caixa de diálogo de origem de partição) de detalhes de associação (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitions.partitionfilterexpression.f1
ms.assetid: 697874d4-3f7a-4126-96f5-37cc8e2ee306
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 604a42cc0b3519f1034733e12f72dc1a7c969ce6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070571"
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
  
  
