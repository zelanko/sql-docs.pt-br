---
title: resultados Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: results Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.results
- urn:schemas-microsoft-com:xml-analysis#results
- http://schemas.microsoft.com/analysisservices/2003/engine#results
helpviewer_keywords: results element
ms.assetid: 3249a17a-7bfa-4753-b605-8f611ba7ae2b
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 06fc0651d4475d612bf2821bcca97c93c17d8633
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="results-element-xmla"></a>Elemento Results (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Contém uma coleção de [raiz](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) elementos retornados pelo [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) usando o método de [lote](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) comando.  
  
 **Namespace**`http://schemas.microsoft.com/analysisservices/2003/xmla-multipleresults`  
  
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
  
## <a name="remarks"></a>Comentários  
 Se um comando **Batch** for executado pelo método **Execute** , o elemento **return** conterá um único elemento **results** em vez de um único elemento **root** . O conteúdo do elemento **results** depende das configurações utilizadas para executar o comando **Batch** .  
  
 Para comandos **Batch** não transacionais, o elemento **results** contém um elemento **root** para cada comando executado pelo comando **Batch** , independentemente de o comando ser concluído com sucesso ou não. Para comandos **Batch** transacionais, o elemento **results** contém apenas um elemento **root** , que contém informações de erro para o comando que falhou no comando **Batch** .  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
