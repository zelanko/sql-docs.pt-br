---
title: Elemento Mode (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 12e792c51b2f6feb3edb4e01c12dcf4809e2d4d4
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34575748"
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|Nenhum|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Bloqueio](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md), [desbloquear](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O pai **bloqueio** elemento usa o **modo** elemento para determinar o tipo de bloqueio para criar um objeto. O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*CommitShared*|Um bloqueio compartilhado é estabelecido no objeto especificado. Outros bloqueios compartilhados podem ser criados para o mesmo objeto.<br /><br /> Um bloqueio compartilhado impede que as transações que contenham operações de gravação, como um [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) chamada do método que executa um [Alter](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md) comando, em um objeto especificado, sejam confirmadas até que o bloqueio compartilhado é removido. Um bloqueio compartilhado não impede que as transações que contenham operações de leitura, como um [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) chamada de método ou um **Execute** chamada do método que executa um [instrução](../../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md) de comando Confirmar.|  
|*CommitExclusive*|Um bloqueio exclusivo é estabelecido no objeto especificado. Outros bloqueios compartilhados ou exclusivos não podem ser criados para o mesmo objeto.<br /><br /> Um bloqueio exclusivo impede que as transações que contenham operações de leitura ou gravação em um objeto especificado sejam confirmadas até a remoção do bloqueio exclusivo.|  
  
## <a name="see-also"></a>Confira também
 [Elemento ID &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/id-element-xmla.md)   
 [Elemento do objeto &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)   
 [Propriedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
