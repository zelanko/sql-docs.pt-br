---
title: Definir um novo atributo automaticamente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- automatic attribute creation
- attributes [Analysis Services], creating
ms.assetid: 208a050a-5e2f-470c-b645-8d835e123db7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5f77148e039e61c080d0eae4e4ab7cad06ef050d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66077312"
---
# <a name="define-a-new-attribute-automatically"></a>Definir um novo atributo automaticamente
  Você pode criar um novo atributo em uma dimensão usando o recurso de edição arrastar-e-soltar no Designer de Dimensão.  
  
### <a name="to-create-a-new-attribute-automatically"></a>Para criar um novo atributo automaticamente  
  
1.  No Designer de Dimensão, abra a dimensão na qual você deseja criar o atributo.  
  
2.  Na guia **Estrutura da Dimensão** , no painel **Exibição da Fonte de Dados** , na tabela onde você quer associar o atributo, selecione a coluna e, depois, arraste a coluna para o painel **Atributos** .  
  
     
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cria o novo atributo que tem o mesmo nome da coluna ao qual está associado. Se houver vários atributos que usam a mesma coluna, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] anexará um número ao nome do atributo.  
  
## <a name="see-also"></a>Consulte Também  
 [Dimensões em modelos multidimensionais](dimensions-in-multidimensional-models.md)   
 [Referência de propriedades de atributo de dimensão](dimension-attribute-properties-reference.md)  
  
  
