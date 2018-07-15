---
title: Elemento NotifyTableChange (XMLA) | Microsoft Docs
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
- NotifyTableChange Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#NotifyTableChange
- http://schemas.microsoft.com/analysisservices/2003/engine#NotifyTableChange
- microsoft.xml.analysis.notifytablechange
helpviewer_keywords:
- NotifyTableChange command
ms.assetid: b76898eb-20d3-48c8-9eb8-1fd5df638bcc
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 612738591115a2e7af964ba4ee5d9950587e45bc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37203896"
---
# <a name="notifytablechange-element-xmla"></a>Elemento NotifyTableChange (XMLA)
  Notifica uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que uma alteração ocorreu nas tabelas em uma fonte de dados especificado.  
  
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Comando](../xml-elements-properties/command-element-xmla.md)|  
|Elementos filho|[Objeto](../xml-elements-properties/object-element-xmla.md), [TableNotifications](../xml-elements-properties/tablenotifications-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 O comando `NotifyTableChange` permite que um aplicativo cliente notifique explicitamente uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] sobre a alteração de uma ou mais tabelas contidas em uma fonte de dados. Para armazenamento em cache pró-ativo, essa notificação indica que objetos ROLAP (OLAP relacionais) baseados naquelas tabelas devem ser revisados e atualizados.  
  
 Esse método de notificação é melhor utilizado para objetos ROLAP baseados em exibições ou consultas nomeadas, definidas em uma exibição de fonte de dados em que as alterações podem ser difíceis de detectar e rastrear.  
  
 O elemento `Object` deve recorrer a uma fonte de dados no banco de dados [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Se o elemento `Object` se referir a um objeto diferente de uma fonte de dados, ocorrerá um erro.  
  
 Para obter mais informações sobre cache pró-ativo, consulte [Cache pró-ativo &#40;Partições&#41;](../../multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
## <a name="see-also"></a>Consulte também  
 [Comandos &#40;XMLA&#41;](xml-elements-commands.md)  
  
  
