---
title: Detalhes de associação de consulta (caixa de diálogo origem da partição) (Analysis Services-dados multidimensionais) | Microsoft Docs
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
ms.openlocfilehash: 59d2ae1fed9d22366786e21a287a621f08418a5d
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84539748"
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
  
 **Verificação**  
 Clique para verificar se a instrução em **Consulta** é uma instrução SQL válida.  
  
## <a name="see-also"></a>Consulte Também  
 [Caixa de diálogo origem da partição &#40;Analysis Services-dados multidimensionais&#41;](partition-source-dialog-box-analysis-services-multidimensional-data.md)  
  
  
