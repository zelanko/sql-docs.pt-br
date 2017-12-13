---
title: Bancos de dados do elemento (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Databases Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Databases
helpviewer_keywords: Databases element
ms.assetid: 2806a074-d47e-4434-9599-04888783770f
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 103d82ca6627a4d29eacd9271c1965ee53449ef5
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="databases-element-assl"></a>Elemento Databases (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém a coleção de [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) elementos associados a um [Server](../../../analysis-services/scripting/objects/server-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Server>  
      ...  
   <Databases>  
      <Database>...</Database>  
      </Databases>  
   ...  
</Server>  
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
|Elementos pai|[Servidor](../../../analysis-services/scripting/objects/server-element-assl.md)|  
|Elementos filho|[Banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.DatabaseCollection>.  
  
## <a name="see-also"></a>Consulte também  
 [Coleções de &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
