---
title: Elemento Mode (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Mode Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Mode
- microsoft.xml.analysis.mode
- http://schemas.microsoft.com/analysisservices/2003/engine#Mode
helpviewer_keywords:
- Mode element
ms.assetid: 43a54181-6494-48c3-b14b-376d8939fa9f
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 57c3450e8928b24dc03e2d5915983f39330d0b0c
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="mode-element-xmla"></a>Elemento Mode (XMLA)
  Identifica o modo a ser usado pelo pai [bloqueio](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md) elemento durante a criação de um bloqueio em um objeto especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Lock>  
   ...  
   <Mode>...</Mode>  
   ...  
</Lock>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Bloqueio](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md), [desbloquear](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O pai **bloqueio** elemento usa o **modo** elemento para determinar o tipo de bloqueio para criar um objeto. O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*CommitShared*|Um bloqueio compartilhado é estabelecido no objeto especificado. Outros bloqueios compartilhados podem ser criados para o mesmo objeto.<br /><br /> Um bloqueio compartilhado impede que as transações que contenham operações de gravação, como um [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) chamada do método que executa um [Alter](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md) comando, em um objeto especificado, sejam confirmadas até que o bloqueio compartilhado é removido. Um bloqueio compartilhado não impede que as transações que contenham operações de leitura, como um [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) chamada de método ou um **Execute** chamada do método que executa um [instrução](../../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md) de comando Confirmar.|  
|*CommitExclusive*|Um bloqueio exclusivo é estabelecido no objeto especificado. Outros bloqueios compartilhados ou exclusivos não podem ser criados para o mesmo objeto.<br /><br /> Um bloqueio exclusivo impede que as transações que contenham operações de leitura ou gravação em um objeto especificado sejam confirmadas até a remoção do bloqueio exclusivo.|  
  
## <a name="see-also"></a>Consulte também  
 [ID do elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/id-element-xmla.md)   
 [Elemento de objeto &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)   
 [Propriedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
