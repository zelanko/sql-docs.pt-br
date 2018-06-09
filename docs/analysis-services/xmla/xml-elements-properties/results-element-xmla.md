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
ms.openlocfilehash: 7fc64d6b31f1b05d8bf5b4d1c80d75dff0583e86
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34576158"
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[retornar](../../../analysis-services/xmla/xml-elements-properties/return-element-xmla.md)|  
|Elementos filho|[root](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 Se um comando **Batch** for executado pelo método **Execute** , o elemento **return** conterá um único elemento **results** em vez de um único elemento **root** . O conteúdo do elemento **results** depende das configurações utilizadas para executar o comando **Batch** .  
  
 Para comandos **Batch** não transacionais, o elemento **results** contém um elemento **root** para cada comando executado pelo comando **Batch** , independentemente de o comando ser concluído com sucesso ou não. Para comandos **Batch** transacionais, o elemento **results** contém apenas um elemento **root** , que contém informações de erro para o comando que falhou no comando **Batch** .  
  
## <a name="see-also"></a>Confira também
 [Propriedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
