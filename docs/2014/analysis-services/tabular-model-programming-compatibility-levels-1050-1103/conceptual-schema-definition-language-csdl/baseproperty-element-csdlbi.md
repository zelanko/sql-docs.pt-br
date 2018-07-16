---
title: Elemento BaseProperty (CSDLBI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: d0f63e52-7330-4b2c-a929-7a517acc6921
caps.latest.revision: 5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6de9e321e3cd5122a6252663c533be2d536800d2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37320836"
---
# <a name="baseproperty-element-csdlbi"></a>Elemento BaseProperty (CSDLBI)
  O elemento BaseProperty é um tipo complexo que serve como base para outros elementos.  
  
 Seus atributos podem aparecer em colunas e em medidas.  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 A tabela a seguir lista os elementos e atributos que definem o elemento BaseProperty.  
  
|Nome|É obrigatório|Description|  
|----------|-----------------|-----------------|  
|Alinhamento|não|O nome fornecido ao membro (coluna, medida, propriedade de navegação, hierarquia ou nível) que é definido pela implementação do tipo Member|  
|FormatString|não|O nome para exibição do membro.|  
|IsRightToLeft|não|Um valor booliano que indica se o campo contém texto que pode ser lido da direita para a esquerda.<br /><br /> Se esse atributo for omitido, será usada a configuração padrão (do modelo).|  
|SortDirection|não|Um valor que indica como os valores de campo geralmente são classificados. O conteúdo desse atributo é definido pelo tipo simples SortDirection.<br /><br /> Se esse atributo for omitido, será atribuída uma direção de classificação com base no tipo de dados do campo.|  
|Unidades|não|O símbolo que se aplica a valores de campos para expressar unidades.<br /><br /> Se ele for omitido, as unidades serão desconhecidas.|  
  
## <a name="alignment-element"></a>Elemento Alignment  
 Esse tipo simples define o formato de nomenclatura que é usado para resolver a ambiguidade de membros.  
  
|Valor|Description|  
|-----------|-----------------|  
|Nenhum|Use o nome do atributo.|  
|Contexto|Use o nome da relação de entrada.|  
|Mesclagem|Concatene o nome da relação de entrada e o nome da propriedade, de acordo com as regras da gramática atual.|  
  
## <a name="sortdirection-element"></a>Elemento SortDirection  
 Esse tipo simples define o formato de nomenclatura que é usado para resolver a ambiguidade de membros.  
  
|Valor|Description|  
|-----------|-----------------|  
|Nenhum|Use o nome do atributo.|  
|Contexto|Use o nome da relação de entrada.|  
|Mesclagem|Concatene o nome da relação de entrada e o nome da propriedade.|  
  
## <a name="see-also"></a>Consulte também  
 [Compreendendo o modelo de objeto de tabela](../representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  
