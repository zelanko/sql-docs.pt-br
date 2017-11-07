---
title: Elemento NotifyTableChange (XMLA) | Microsoft Docs
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
- NotifyTableChange Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#NotifyTableChange
- http://schemas.microsoft.com/analysisservices/2003/engine#NotifyTableChange
- microsoft.xml.analysis.notifytablechange
helpviewer_keywords:
- NotifyTableChange command
ms.assetid: b76898eb-20d3-48c8-9eb8-1fd5df638bcc
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 45e156076d7d97164fcb43674e3975daf6944e1e
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="notifytablechange-element-xmla"></a>Elemento NotifyTableChange (XMLA)
  Notifica uma instância de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que ocorreu uma alteração nas tabelas em uma fonte de dados especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Command>  
   <NotifyTableChange>  
      <Object>...</Object>  
      <TableNotifications>...</TableNotifications>  
   </NotifyTableChange>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Comando](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Elementos filho|[Objeto](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md), [TableNotifications](../../../analysis-services/xmla/xml-elements-properties/tablenotifications-element-xmla.md)|  
  
## <a name="remarks"></a>Comentários  
 O **NotifyTableChange** comando permite que um aplicativo cliente notifique explicitamente uma [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] da instância que um ou mais tabelas contidas em uma fonte de dados foram alteradas. Para armazenamento em cache pró-ativo, essa notificação indica que objetos ROLAP (OLAP relacionais) baseados naquelas tabelas devem ser revisados e atualizados.  
  
 Esse método de notificação é melhor utilizado para objetos ROLAP baseados em exibições ou consultas nomeadas, definidas em uma exibição de fonte de dados em que as alterações podem ser difíceis de detectar e rastrear.  
  
 O **objeto** elemento deve se referir a uma fonte de dados a [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] banco de dados. Se o **objeto** elemento se refere a um objeto diferente de uma fonte de dados, ocorrerá um erro.  
  
 Para obter mais informações sobre cache pró-ativo, consulte [Cache pró-ativo &#40;Partições&#41;](../../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
## <a name="see-also"></a>Consulte também  
 [Comandos &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  

