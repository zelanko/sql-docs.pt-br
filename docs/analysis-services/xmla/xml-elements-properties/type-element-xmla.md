---
title: Tipo de elemento (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ca05cb4bc5ea8951db028ed4da53ee3bfd7131dc
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="type-element-xmla"></a>Elemento Type (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Determina o tipo de processamento a ser executada pelo [processo](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Process>  
...  
   <Type>...</Type>  
...  
</Process>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Processar](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 Para obter mais informações sobre como processar opções disponíveis para objetos em uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], consulte [processando um modelo multidimensional &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 O valor de **tipo** elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Value|Descrição|  
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
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
