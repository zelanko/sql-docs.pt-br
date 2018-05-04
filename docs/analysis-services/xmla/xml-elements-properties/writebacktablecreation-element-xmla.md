---
title: Elemento WritebackTableCreation (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- WritebackTableCreation Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#WritebackTableCreation
- microsoft.xml.analysis.writebacktablecreation
- http://schemas.microsoft.com/analysisservices/2003/engine#WritebackTableCreation
helpviewer_keywords:
- WritebackTableCreation element
ms.assetid: e9579d63-e28c-4d4e-9f4a-21c5da24c276
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 9f0edcc8c195cb97aa388fd8d24f384fbc1231c5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="writebacktablecreation-element-xmla"></a>Elemento WritebackTableCreation (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Determina se uma tabela de write-back é criada durante a [processo](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) operação.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Process>  
...  
   <WritebackTableCreation>...</WritebackTableCreation>  
...  
</Process>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Processar](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 Para obter mais informações sobre opções de processamento disponíveis para objetos em uma instância do Analysis Services, consulte [processando um modelo multidimensional &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 O valor do elemento **WritebackTableCreation** é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Criar*|Crie uma nova tabela de write-back, se não existir uma. Se a tabela de write-back já existir, ocorrerá um erro.|  
|*CreateAlways*|Crie uma nova tabela de write-back, substituindo qualquer tabela de write-back já existente.|  
|*UseExisting*|Use a tabela de write-back já existente, se já existir uma. Se não houver uma tabela, ocorrerá um erro.|  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
