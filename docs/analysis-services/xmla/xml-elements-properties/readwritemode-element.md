---
title: Elemento ReadWriteMode | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a109db366c2b165ccf466bdeab8b7d3bb9c4d69f
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="readwritemode-element"></a>Elemento ReadWriteMode
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  A propriedade do banco de dados **ReadWriteMode** especifica se o banco de dados está no modo **ReadWrite** ou no modo **ReadOnly** . Estes são os únicos dois possíveis valores da propriedade.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Database>  
...  
   <ddlns_100_0:ReadWriteMode>...</ddlns_100_0:ReadWriteMode>  
...  
</Database>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|ReadWrite|  
|Cardinalidade|0-1: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Banco de dados](../../../analysis-services/xmla/xml-elements-properties/database-element-xmla.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 Bancos de dados são criados somente no modo **ReadWrite** . Não podem ser criados Bancos de dados em modo **ReadOnly** .  
  
 O valor do elemento **ReadWriteMode** é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|*Somente leitura*|Nenhuma alteração nem atualização pode ser aplicada ao banco de dados.|  
|*ReadWrite*|Alterações e atualizações podem ser aplicadas ao banco de dados.|  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Attach](../../../analysis-services/xmla/xml-elements-commands/attach-element.md)   
 [Anexar e desanexar bancos de dados do Analysis Services](../../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Mover um banco de dados do Analysis Services](../../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)   
 [Banco de dados ReadWriteModes](../../../analysis-services/multidimensional-models/database-readwritemodes.md)   
 [Alternar um banco de dados do Analysis Services entre os modos ReadOnly e ReadWrite](../../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
  
