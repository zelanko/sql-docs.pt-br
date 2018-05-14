---
title: resultados Element (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 97cebdade566f796ff09bd68e8b292868e37e0a9
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="results-element-xmla"></a>Elemento Results (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contém uma coleção de elementos [root](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) retornada pelo método [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) que usa o comando [Batch](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) .  
  
 **namespace** `http://schemas.microsoft.com/analysisservices/2003/xmla-multipleresults`  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<return>  
   <results>  
      <root>...</root>  
   </results>  
</return>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[retornar](../../../analysis-services/xmla/xml-elements-properties/return-element-xmla.md)|  
|Elementos filho|[raiz](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 Se um comando **Batch** for executado pelo método **Execute** , o elemento **return** conterá um único elemento **results** em vez de um único elemento **root** . O conteúdo do elemento **results** depende das configurações utilizadas para executar o comando **Batch** .  
  
 Para comandos **Batch** não transacionais, o elemento **results** contém um elemento **root** para cada comando executado pelo comando **Batch** , independentemente de o comando ser concluído com sucesso ou não. Para comandos **Batch** transacionais, o elemento **results** contém apenas um elemento **root** , que contém informações de erro para o comando que falhou no comando **Batch** .  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
