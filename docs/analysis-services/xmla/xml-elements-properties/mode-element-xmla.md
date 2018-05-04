---
title: Elemento Mode (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
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
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: e5f6f3e46a86d8db07d2ce13a84007f2c36af267
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="mode-element-xmla"></a>Elemento Mode (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
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
  
## <a name="remarks"></a>Remarks  
 O pai **bloqueio** elemento usa o **modo** elemento para determinar o tipo de bloqueio para criar um objeto. O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*CommitShared*|Um bloqueio compartilhado é estabelecido no objeto especificado. Outros bloqueios compartilhados podem ser criados para o mesmo objeto.<br /><br /> Um bloqueio compartilhado impede que as transações que contenham operações de gravação, como um [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) chamada do método que executa um [Alter](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md) comando, em um objeto especificado, sejam confirmadas até que o bloqueio compartilhado é removido. Um bloqueio compartilhado não impede que as transações que contenham operações de leitura, como um [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) chamada de método ou um **Execute** chamada do método que executa um [instrução](../../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md) de comando Confirmar.|  
|*CommitExclusive*|Um bloqueio exclusivo é estabelecido no objeto especificado. Outros bloqueios compartilhados ou exclusivos não podem ser criados para o mesmo objeto.<br /><br /> Um bloqueio exclusivo impede que as transações que contenham operações de leitura ou gravação em um objeto especificado sejam confirmadas até a remoção do bloqueio exclusivo.|  
  
## <a name="see-also"></a>Consulte também  
 [ID do elemento & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/id-element-xmla.md)   
 [Elemento de objeto & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)   
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
