---
title: os resultados Element (XMLA) | Microsoft Docs
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
api_name:
- results Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.results
- urn:schemas-microsoft-com:xml-analysis#results
- http://schemas.microsoft.com/analysisservices/2003/engine#results
helpviewer_keywords:
- results element
ms.assetid: 3249a17a-7bfa-4753-b605-8f611ba7ae2b
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1e42f6aa620b57630df690ee92bdbbd849ab100b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37165227"
---
# <a name="results-element-xmla"></a>Elemento Results (XMLA)
  Contém uma coleção de elementos [root](root-element-xmla.md) retornada pelo método [Execute](../xml-elements-methods-execute.md) que usa o comando [Batch](../xml-elements-commands/batch-element-xmla.md) .  
  
 **Namespace** http://schemas.microsoft.com/analysisservices/2003/xmla-multipleresults  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<return>  
   <results>  
      <root>...</root>  
   </results>  
</return>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[retornar](return-element-xmla.md)|  
|Elementos filho|[root](root-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 Se um comando `Batch` for executado pelo método `Execute`, o elemento `return` conterá um único elemento `results` em vez de um único elemento `root`. O conteúdo do elemento `results` depende das configurações utilizadas para executar o comando `Batch`.  
  
 Para comandos `Batch` não transacionais, o elemento `results` contém um elemento `root` para cada comando executado pelo comando `Batch`, independentemente de o comando ser concluído com sucesso ou não. Para comandos `Batch` transacionais, o elemento `results` contém apenas um elemento `root`, que contém informações de erro para o comando que falhou no comando `Batch`.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
