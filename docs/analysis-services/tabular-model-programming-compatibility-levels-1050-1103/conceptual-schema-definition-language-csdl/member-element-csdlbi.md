---
title: Elemento Member (CSDLBI) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 39c8271c188d22cf6246e6c6c969b4a3d224b3e8
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38041664"
---
# <a name="member-element-csdlbi"></a>Elemento Member (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  O elemento Member é um tipo complexo que serve como base para outros elementos.  
  
 Seu atributos podem aparecer em colunas, medidas, propriedades de navegação, hierarquias e níveis.  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 A tabela a seguir lista os elementos e atributos que definem o elemento Member.  
  
|Nome|É obrigatório|Description|  
|----------|-----------------|-----------------|  
|Nome||O nome fornecido ao membro (coluna, medida, propriedade de navegação, hierarquia ou nível) que é definido pela implementação do tipo TMember|  
|Caption|Sim|O nome para exibição do membro.|  
|ContextualNameRule|Sim|O formato de nomenclatura que é usado para resolver a ambiguidade de membros. O conteúdo desse atributo é definido pelo tipo simples ContextualNameRule.|  
|Hidden||Um valor booliano que indica se o membro será ocultado do cliente.<br /><br /> O padrão é false, o que significa que as colunas ficam visíveis no cliente.|  
|ReferenceName||O identificador usado para fazer referência ao membro em uma consulta DAX. Se esse atributo for omitido, será usado o nome do campo|  
  
## <a name="contextualnamerule-element"></a>Elemento ContextualNameRule  
 Esse tipo simples define o formato de nomenclatura que é usado para resolver a ambiguidade de membros.  
  
|Valor|Description|  
|-----------|-----------------|  
|Nenhum|Use o nome do atributo.|  
|Contexto|Use o nome da relação de entrada.|  
|Mesclagem|Concatene o nome da relação de entrada e o nome da propriedade.|  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre o modelo de objeto Tabular em compatibilidade níveis 1050 até 1103](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  
