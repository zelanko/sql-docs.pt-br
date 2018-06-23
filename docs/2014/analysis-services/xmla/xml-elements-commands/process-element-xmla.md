---
title: Processar Element (XMLA) | Microsoft Docs
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
- Process Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Process
- http://schemas.microsoft.com/analysisservices/2003/engine#Process
- microsoft.xml.analysis.process
helpviewer_keywords:
- Process command
ms.assetid: 886fd480-c0e6-4c9b-b65e-da47f874d938
caps.latest.revision: 13
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 4e90cbb8d18cdba034019e74b7b9d0b00966ee7f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119195"
---
# <a name="process-element-xmla"></a>Elemento Process (XMLA)
  Processa objetos em um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Command>  
   <Process>  
      <Type>...</Type>  
      <Object>...</Object>  
      <Bindings>...</Bindings>  
      <DataSource>...</DataSource>  
      <DataSourceView>...</DataSourceView>  
      <ErrorConfiguration>...</ErrorConfiguration>  
      <WriteBackTableCreation>...</WriteBackTableCreation>  
   </Process>  
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
|Elementos filho|[Associações](../xml-elements-properties/bindings-element-xmla.md), [DataSource](../xml-elements-properties/source-element-xmla.md), [DataSourceView](../xml-elements-properties/datasourceview-element-xmla.md), [ErrorConfiguration](../xml-elements-properties/errorconfiguration-element-xmla.md), [objeto](../xml-elements-properties/object-element-xmla.md), [tipo Elemento &#40;XMLA&#41;](../xml-elements-properties/type-element-xmla.md), [WriteBackTableCreation](../xml-elements-properties/writebacktablecreation-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 Para obter mais informações sobre o processamento de objetos, consulte [processar objetos &#40;XMLA&#41;](../xml-elements-objects.md).  
  
## <a name="see-also"></a>Consulte também  
 [Comandos &#40;XMLA&#41;](xml-elements-commands.md)  
  
  