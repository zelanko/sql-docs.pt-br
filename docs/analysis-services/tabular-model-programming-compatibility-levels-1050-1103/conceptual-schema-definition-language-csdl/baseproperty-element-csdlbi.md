---
title: Elemento BaseProperty (CSDLBI) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f1e14b3bcfe862083aa78d634ca20ecaa0f4dd5c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="baseproperty-element-csdlbi"></a>Elemento BaseProperty (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  O elemento BaseProperty é um tipo complexo que serve como base para outros elementos.  
  
 Seus atributos podem aparecer em colunas e em medidas.  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 A tabela a seguir lista os elementos e atributos que definem o elemento BaseProperty.  
  
|Nome|É obrigatório|Descrição|  
|----------|-----------------|-----------------|  
|Alinhamento|Não|O nome fornecido ao membro (coluna, medida, propriedade de navegação, hierarquia ou nível) que é definido pela implementação do tipo Member|  
|FormatString|Não|O nome para exibição do membro.|  
|IsRightToLeft|Não|Um valor booliano que indica se o campo contém texto que pode ser lido da direita para a esquerda.<br /><br /> Se esse atributo for omitido, será usada a configuração padrão (do modelo).|  
|SortDirection|Não|Um valor que indica como os valores de campo geralmente são classificados. O conteúdo desse atributo é definido pelo tipo simples SortDirection.<br /><br /> Se esse atributo for omitido, será atribuída uma direção de classificação com base no tipo de dados do campo.|  
|Unidades|Não|O símbolo que se aplica a valores de campos para expressar unidades.<br /><br /> Se ele for omitido, as unidades serão desconhecidas.|  
  
## <a name="alignment-element"></a>Elemento Alignment  
 Esse tipo simples define o formato de nomenclatura que é usado para resolver a ambiguidade de membros.  
  
|Valor|Description|  
|-----------|-----------------|  
|Nenhuma|Use o nome do atributo.|  
|Contexto|Use o nome da relação de entrada.|  
|Mesclagem|Concatene o nome da relação de entrada e o nome da propriedade, de acordo com as regras da gramática atual.|  
  
## <a name="sortdirection-element"></a>Elemento SortDirection  
 Esse tipo simples define o formato de nomenclatura que é usado para resolver a ambiguidade de membros.  
  
|Valor|Description|  
|-----------|-----------------|  
|Nenhuma|Use o nome do atributo.|  
|Contexto|Use o nome da relação de entrada.|  
|Mesclagem|Concatene o nome da relação de entrada e o nome da propriedade.|  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre o modelo de objeto de tabela em compatibilidade 1050 1103 por meio de níveis](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  
