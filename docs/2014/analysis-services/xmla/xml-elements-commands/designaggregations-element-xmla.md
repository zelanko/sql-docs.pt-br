---
title: Elemento DesignAggregations (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DesignAggregations Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#DesignAggregations
- microsoft.xml.analysis.designaggregations
- http://schemas.microsoft.com/analysisservices/2003/engine#DesignAggregations
helpviewer_keywords:
- DesignAggregations command
ms.assetid: 4c419dbc-7405-40aa-8ddd-6b46685a297d
caps.latest.revision: 13
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: d448a7cc815dddcc4e9568831f2d652fc7a22680
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122016"
---
# <a name="designaggregations-element-xmla"></a>Elemento DesignAggregations (XMLA)
  Cria agregações para um design de agregação em um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Command>  
   <DesignAggregations>  
      <Object>...</Object>  
      <Time>...</Time>  
      <Steps>...</Steps>  
      <Optimization>...</Optimization>  
      <Storage>...</Storage>  
      <Materialize>...</Materialize>  
      <Queries>...</Queries>  
   </DesignAggregations>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Comando](../xml-elements-properties/command-element-xmla.md)|  
|Elementos filho|[Materializar](../xml-elements-properties/materialize-element-xmla.md), [objeto](../xml-elements-properties/object-element-xmla.md), [otimização](../xml-elements-properties/optimization-element-xmla.md), [consultas](../xml-elements-properties/queries-element-xmla.md), [etapas](../xml-elements-properties/steps-element-xmla.md), [armazenamento](../xml-elements-properties/storage-element-xmla.md) , [Tempo](../xml-elements-properties/time-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 O comando `DesignAggregations` é usado para gerar definições de agregação armazenadas por um design de agregação. Um design de agregação pode ser usado para materializar agregações para uma partição e pode ser reutilizado entre partições.  
  
## <a name="see-also"></a>Consulte também  
 [Comandos &#40;XMLA&#41;](xml-elements-commands.md)  
  
  