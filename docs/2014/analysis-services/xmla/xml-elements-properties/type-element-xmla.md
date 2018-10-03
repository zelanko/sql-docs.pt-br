---
title: Tipo de elemento (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Type Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.type
- http://schemas.microsoft.com/analysisservices/2003/engine#Type
- urn:schemas-microsoft-com:xml-analysis#Type
helpviewer_keywords:
- Type element
ms.assetid: 5d898123-a635-402a-be86-8249d7304fa4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 71f7745a3f3ea39309d871d5fafef737176d3a45
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48054386"
---
# <a name="type-element-xmla"></a>Elemento Type (XMLA)
  Determina o tipo de processamento a ser executado o [processo](../xml-elements-commands/process-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Process>  
...  
   <Type>...</Type>  
...  
</Process>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|None|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Processar](../xml-elements-commands/process-element-xmla.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre como processar opções disponíveis para objetos em uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], consulte [processamento de objeto de modelo Multidimensional](../../multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 O valor do elemento `Type` é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*ProcessFull*|Descarta todos os dados do objeto afetado e processa o objeto afetado.|  
|*ProcessAdd*|Adiciona novos dados ao objeto afetado.|  
|*ProcessUpdate*|Atualiza os dados no objeto afetado.|  
|*ProcessIndexes*|Cria ou recria índices e agregações no objeto afetado.|  
|*ProcessScriptCache*|Se o cubo for processado, o servidor recriará o cache de scripts MDX. Em caso negativo, um erro será gerada.<br /><br /> **Observação** aplica-se apenas ao cubo.|  
|*ProcessData*|Processa dados somente no objeto afetado.|  
|*ProcessDefault*|Detecta o estado do objeto afetado e executa a opção de processamento adequada no objeto afetado para otimizá-lo completamente e retorná-lo para um estado completamente processado.|  
|*ProcessClear*|Descarta os dados do objeto afetado e todos os objetos relacionados.|  
|*ProcessStructure*|Processa a estrutura somente do objeto afetado.|  
|*ProcessClearStructureOnly*|Exclui os dados somente do objeto afetado.|  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
