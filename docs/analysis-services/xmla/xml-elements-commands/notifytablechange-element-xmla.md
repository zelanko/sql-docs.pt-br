---
title: Elemento NotifyTableChange (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 125cea75f5c892cd30e3f346c0b755ab8de55ae5
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="notifytablechange-element-xmla"></a>Elemento NotifyTableChange (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
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
  
## <a name="remarks"></a>Remarks  
 O **NotifyTableChange** comando permite que um aplicativo cliente notifique explicitamente uma [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] da instância que um ou mais tabelas contidas em uma fonte de dados foram alteradas. Para armazenamento em cache pró-ativo, essa notificação indica que objetos ROLAP (OLAP relacionais) baseados naquelas tabelas devem ser revisados e atualizados.  
  
 Esse método de notificação é melhor utilizado para objetos ROLAP baseados em exibições ou consultas nomeadas, definidas em uma exibição de fonte de dados em que as alterações podem ser difíceis de detectar e rastrear.  
  
 O **objeto** elemento deve se referir a uma fonte de dados a [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] banco de dados. Se o **objeto** elemento se refere a um objeto diferente de uma fonte de dados, ocorrerá um erro.  
  
 Para obter mais informações sobre cache pró-ativo, consulte [Cache pró-ativo &#40;Partições&#41;](../../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
## <a name="see-also"></a>Consulte também  
 [Comandos & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
