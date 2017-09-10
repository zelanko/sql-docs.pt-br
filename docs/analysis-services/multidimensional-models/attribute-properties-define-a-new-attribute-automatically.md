---
title: Definir um novo atributo automaticamente | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- automatic attribute creation
- attributes [Analysis Services], creating
ms.assetid: 208a050a-5e2f-470c-b645-8d835e123db7
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 56bb141f18d96c1a598b83a14d3f301764df5ecf
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="attribute-properties---define-a-new-attribute-automatically"></a>Propriedades de atributo - definir um novo atributo automaticamente
  Você pode criar um novo atributo em uma dimensão usando o recurso de edição arrastar-e-soltar no Designer de Dimensão.  
  
### <a name="to-create-a-new-attribute-automatically"></a>Para criar um novo atributo automaticamente  
  
1.  No Designer de Dimensão, abra a dimensão na qual você deseja criar o atributo.  
  
2.  Na guia **Estrutura da Dimensão** , no painel **Exibição da Fonte de Dados** , na tabela onde você quer associar o atributo, selecione a coluna e, depois, arraste a coluna para o painel **Atributos** .  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cria o novo atributo que tem o mesmo nome da coluna ao qual está associado. Se houver vários atributos que usam a mesma coluna, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] anexará um número ao nome do atributo.  
  
## <a name="see-also"></a>Consulte também  
 [Dimensões em modelos multidimensionais](../../analysis-services/multidimensional-models/dimensions-in-multidimensional-models.md)   
 [Referência de propriedades de atributo de dimensão](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
