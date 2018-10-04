---
title: Elemento Schema (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Schema Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Schema
helpviewer_keywords:
- Schema element
ms.assetid: 4b6375fb-7ad8-4d5f-88b1-abd3da2654db
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5b8f9ab11698c2e0e73436abb3506ca38c45afe6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48218786"
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|esquema|  
|Valor padrão|None|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[DataSourceView](../objects/datasourceview-element-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O elemento `Schema` é representado pelo formato da linguagem XSD (XML Schema Definition) de DataSets no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework, com algumas extensões para DataSets e outras específicas para esse uso na linguagem de definição de dados (DDL). DataSets define um mapeamento flexível de XSD em um esquema relacional, mas retorna XSD em uma forma mais canônica. Somente essa forma canônica é válida nas fontes de dados.  
  
 O elemento que corresponde ao pai de `Schema` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.DataSourceView>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
