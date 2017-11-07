---
title: Elemento Schema (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Schema Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Schema
helpviewer_keywords:
- Schema element
ms.assetid: 4b6375fb-7ad8-4d5f-88b1-abd3da2654db
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 51fd142bad60a7c8e64d27952509dfa5b2b6c28f
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="schema-element-assl"></a>Elemento Schema (ASSL)
  Contém o esquema da exibição da fonte de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DataSourceView>  
   ...  
   <Schema>...</Schema>  
   ...  
</DataSourceView>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|esquema|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O **esquema** é representada usando o formato de linguagem de definição de esquema XML (XSD) de conjuntos de dados de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] do .NET Framework, com algumas extensões para DataSets e outras específicas para esse uso na definição de dados Language (DDL). DataSets define um mapeamento flexível de XSD em um esquema relacional, mas retorna XSD em uma forma mais canônica. Somente essa forma canônica é válida nas fontes de dados.  
  
 O elemento que corresponde ao pai do **esquema** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.DataSourceView>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

