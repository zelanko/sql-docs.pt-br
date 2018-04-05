---
title: Tipo de elemento (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Type Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.type
- http://schemas.microsoft.com/analysisservices/2003/engine#Type
- urn:schemas-microsoft-com:xml-analysis#Type
helpviewer_keywords:
- Type element
ms.assetid: 5d898123-a635-402a-be86-8249d7304fa4
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 363b89eddf7794174689c0d6df7805328c88eb70
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="type-element-xmla"></a>Elemento Type (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Determina o tipo de processamento a ser executada pelo [processo](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) elemento.  
  
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
|Valor padrão|Nenhum|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Processar](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Para obter mais informações sobre como processar opções disponíveis para objetos em uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], consulte [processando um modelo multidimensional &#40; Analysis Services &#41; ](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 O valor de **tipo** elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*ProcessFull*|Descarta todos os dados do objeto afetado e processa o objeto afetado.|  
|*ProcessAdd*|Adiciona novos dados ao objeto afetado.|  
|*ProcessUpdate*|Atualiza os dados no objeto afetado.|  
|*ProcessIndexes*|Cria ou recria índices e agregações no objeto afetado.|  
|*ProcessScriptCache*|Se o cubo for processado, o servidor recriará o cache de scripts MDX. Em caso negativo, um erro será gerada.<br /><br /> **Observação** aplica-se somente ao cubo.|  
|*ProcessData*|Processa dados somente no objeto afetado.|  
|*ProcessDefault*|Detecta o estado do objeto afetado e executa a opção de processamento adequada no objeto afetado para otimizá-lo completamente e retorná-lo para um estado completamente processado.|  
|*ProcessClear*|Descarta os dados do objeto afetado e todos os objetos relacionados.|  
|*ProcessStructure*|Processa a estrutura somente do objeto afetado.|  
|*ProcessClearStructureOnly*|Exclui os dados somente do objeto afetado.|  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
