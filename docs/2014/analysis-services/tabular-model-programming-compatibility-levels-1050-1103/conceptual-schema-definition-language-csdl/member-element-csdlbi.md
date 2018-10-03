---
title: Elemento Member (CSDLBI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 1ba225f5-3867-4aae-a519-e3c277688d1e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f193cb746b8df43c33aa65ea3d69d87ab7c36655
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48218826"
---
# <a name="member-element-csdlbi"></a>Elemento Member (CSDLBI)
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
|None|Use o nome do atributo.|  
|Contexto|Use o nome da relação de entrada.|  
|Mesclagem|Concatene o nome da relação de entrada e o nome da propriedade.|  
  
## <a name="see-also"></a>Consulte também  
 [Compreendendo o modelo de objeto de tabela](../representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  
