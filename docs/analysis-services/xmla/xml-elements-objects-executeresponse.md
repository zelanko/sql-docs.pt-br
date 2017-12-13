---
title: Elemento ExecuteResponse (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
apiname: ExecuteResponse Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#ExecuteResponse
- http://schemas.microsoft.com/analysisservices/2003/engine#ExecuteResponse
- microsoft.xml.analysis.executeresponse
helpviewer_keywords: ExecuteResponse element
ms.assetid: 6edb1b82-da4c-4cd9-9385-bea04032f0eb
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 097003992837088f15d6bae461220efb10c1a162
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="xml-elements---objects---executeresponse"></a>XML elementos - objetos - ExecuteResponse
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Contém as informações retornadas por uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em resposta a um [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md) chamada de método.  
  
 **Namespace** urn:schemas-microsoft-com:xml-analysis  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ExecuteResponse>  
   <return>  
</ExecuteResponse>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|[retornar](../../analysis-services/xmla/xml-elements-properties/return-element-xmla.md)|  
  
## <a name="remarks"></a>Comentários  
 O **ExecuteResponse** é o elemento superior dentro do corpo de uma resposta SOAP para o **Execute** método.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento DiscoverResponse &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-objects-discoverresponse.md)   
 [Objetos de &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-objects.md)  
  
  
