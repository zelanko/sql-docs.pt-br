---
title: Definir um novo atributo automaticamente | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d598ddb86e421309fe6aa7361595d64ddf1f0a24
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="attribute-properties---define-a-new-attribute-automatically"></a>Propriedades de atributo - definir um novo atributo automaticamente
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Você pode criar um novo atributo em uma dimensão usando o recurso de edição arrastar-e-soltar no Designer de Dimensão.  
  
### <a name="to-create-a-new-attribute-automatically"></a>Para criar um novo atributo automaticamente  
  
1.  No Designer de Dimensão, abra a dimensão na qual você deseja criar o atributo.  
  
2.  Na guia **Estrutura da Dimensão** , no painel **Exibição da Fonte de Dados** , na tabela onde você quer associar o atributo, selecione a coluna e, depois, arraste a coluna para o painel **Atributos** .  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cria o novo atributo que tem o mesmo nome da coluna ao qual está associado. Se houver vários atributos que usam a mesma coluna, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] anexará um número ao nome do atributo.  
  
## <a name="see-also"></a>Consulte também  
 [Dimensões em modelos multidimensionais](../../analysis-services/multidimensional-models/dimensions-in-multidimensional-models.md)   
 [Referência de propriedades de atributo de dimensão](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
