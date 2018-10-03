---
title: Elemento ReadWriteMode | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- ReadWriteMode command
ms.assetid: 379bcaca-bb7e-4934-a9e7-21f8ede2fdc7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fa1febe828bf8711ff87f50cfd5a8ce7cbd6eed8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48166646"
---
# <a name="readwritemode-element"></a>Elemento ReadWriteMode
  A propriedade do banco de dados `ReadWriteMode` especifica se o banco de dados está no modo `ReadWrite` ou no modo `ReadOnly`. Estes são os únicos dois possíveis valores da propriedade.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Database>  
...  
   <ddlns_100_0:ReadWriteMode>...</ddlns_100_0:ReadWriteMode>  
...  
</Database>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|ReadWrite|  
|Cardinalidade|0-1: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Banco de dados](database-element-xmla.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 Bancos de dados são criados somente no modo `ReadWrite`. Não podem ser criados Bancos de dados em modo `ReadOnly`.  
  
 O valor do elemento `ReadWriteMode` é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Somente leitura*|Nenhuma alteração nem atualização pode ser aplicada ao banco de dados.|  
|*ReadWrite*|Alterações e atualizações podem ser aplicadas ao banco de dados.|  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Attach](../xml-elements-commands/attach-element.md)   
 [Anexar e desanexar bancos de dados do Analysis Services](../../multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Mover um banco de dados do Analysis Services](../../multidimensional-models/move-an-analysis-services-database.md)   
 [Banco de dados ReadWriteModes](../../multidimensional-models/database-readwritemodes.md)   
 [Alternar um banco de dados do Analysis Services entre os modos ReadOnly e ReadWrite](../../multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
  
