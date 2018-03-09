---
title: Definir um novo atributo automaticamente | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- automatic attribute creation
- attributes [Analysis Services], creating
ms.assetid: 208a050a-5e2f-470c-b645-8d835e123db7
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f56c70ce3d75de8f7be924941df227d1213902c0
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
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
  
  
