---
title: Elemento Mode (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Mode Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Mode
- microsoft.xml.analysis.mode
- http://schemas.microsoft.com/analysisservices/2003/engine#Mode
helpviewer_keywords:
- Mode element
ms.assetid: 43a54181-6494-48c3-b14b-376d8939fa9f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e768d9ef176a05d4fe7622a520c9ac98f1d71d81
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48072406"
---
# <a name="mode-element-xmla"></a>Elemento Mode (XMLA)
  Identifica o modo a ser usado pelo pai [bloqueio](../xml-elements-commands/lock-element-xmla.md) elemento durante a criação de um bloqueio em um objeto especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Lock>  
   ...  
   <Mode>...</Mode>  
   ...  
</Lock>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|None|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Bloqueio](../xml-elements-commands/lock-element-xmla.md), [desbloquear](../xml-elements-commands/unlock-element-xmla.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O elemento pai `Lock` usa o elemento `Mode` para determinar o tipo de bloqueio a ser criado em um objeto. O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*CommitShared*|Um bloqueio compartilhado é estabelecido no objeto especificado. Outros bloqueios compartilhados podem ser criados para o mesmo objeto.<br /><br /> Um bloqueio compartilhado impede que as transações que contenham operações de gravação, como um [Execute](../xml-elements-methods-execute.md) chamada de método em execução um [Alter](../xml-elements-commands/alter-element-xmla.md) comando em um objeto especificado, sejam confirmadas até que o bloqueio compartilhado é removido. Um bloqueio compartilhado não impede que as transações que contenham operações de leitura, como um [Discover](../xml-elements-methods-discover.md) chamada de método ou uma `Execute` chamada de método em execução um [instrução](../xml-elements-commands/statement-element-xmla.md) comando sejam confirmadas.|  
|*CommitExclusive*|Um bloqueio exclusivo é estabelecido no objeto especificado. Outros bloqueios compartilhados ou exclusivos não podem ser criados para o mesmo objeto.<br /><br /> Um bloqueio exclusivo impede que as transações que contenham operações de leitura ou gravação em um objeto especificado sejam confirmadas até a remoção do bloqueio exclusivo.|  
  
## <a name="see-also"></a>Consulte também  
 [ID do elemento &#40;XMLA&#41;](id-element-xmla.md)   
 [Elemento do objeto &#40;XMLA&#41;](object-element-xmla.md)   
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
