---
title: Tipo de dados EmptyResult (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- EmptyResult Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#EmptyResult
- olapxmla_EmptyResult
- urn:schemas-microsoft-com:xml-analysis#EmptyResult
helpviewer_keywords:
- EmptyResult data type
ms.assetid: 63818123-acbb-4220-9d60-1aa20a7326a1
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3854d63c59cd8b5132358d51e084e39232b79d52
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="emptyresult-data-type-xmla"></a>Tipo de dados EmptyResult (XMLA)
  Define um tipo de dados derivado que representa um [raiz](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) elemento que não retorna dados de um [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) ou [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) chamada de método.  
  
 **Namespace** urn:schemas-microsoft-com:xml-analysis:empty  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:empty">  
   <!-- All elements are inherited from Resultset -->  
</root>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|[Conjunto de resultados](../../../analysis-services/xmla/xml-data-types/resultset-data-type-xmla.md)|  
|Tipos de dados derivados|Nenhuma|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|Nenhuma|  
|Elementos derivados|[raiz](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
  
## <a name="remarks"></a>Comentários  
 Não se espera que alguns comandos do XMLA (XML for Analysis) retornem um resultado ou  não poderiam retornar um resultado devido a um erro. Os comandos XMLA que não retornam um resultado retornam o tipo de dados **EmptyResult** , um namespace no elemento **root** .  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir representa um elemento **root** retornado para um resultado vazio.  
  
```  
<return>  
   <root xmlns="urn:schemas-microsoft-com:xml-analysis:empty"/>  
</return>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML &#40; XMLA &#41;](../../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)  
  
  

