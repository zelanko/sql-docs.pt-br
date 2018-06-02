---
title: Elemento Attach | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fa13ada270ffe7c7d7a1290dd3645efae5f4c6a1
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34574058"
---
# <a name="attach-element"></a>Elemento Attach
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Anexa um banco de dados do Analysis Services que foi anteriormente desanexado da instância do servidor atual ou de outra instância, a instância do servidor atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Command>  
   <Attach>  
      <Folder>...</Folder>  
            <ReadWriteMode>...</ReadWriteMode>  
            <Password>...</Password>  
   </Attach>  
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
|Elementos pai|[Comando](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Elementos filho|[Pasta](../../../analysis-services/xmla/xml-elements-properties/folder-element-xmla.md)<br /><br /> [readWriteMode](../../../analysis-services/xmla/xml-elements-properties/readwritemode-element.md)<br /><br /> [Senha](../../../analysis-services/xmla/xml-elements-properties/password-element-xmla.md)|  
  
## <a name="see-also"></a>Confira também
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Elemento Detach](../../../analysis-services/xmla/xml-elements-commands/detach-element.md)   
 [Anexar e desanexar bancos de dados do Analysis Services](../../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Mover um banco de dados do Analysis Services](../../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)   
 [Banco de dados ReadWriteModes](../../../analysis-services/multidimensional-models/database-readwritemodes.md)   
 [Alternar um banco de dados do Analysis Services entre os modos ReadOnly e ReadWrite](../../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
  
