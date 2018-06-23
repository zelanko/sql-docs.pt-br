---
title: Elemento Unlock (XMLA) | Microsoft Docs
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
- Unlock Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Unlock
- urn:schemas-microsoft-com:xml-analysis#Unlock
- microsoft.xml.analysis.unlock
helpviewer_keywords:
- Unlock command
ms.assetid: 46425b33-baa2-41ad-803a-34d2fb4b2cab
caps.latest.revision: 14
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: ce0b1512c32ddffd029e9a4704e9afcd5ad7a388
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120204"
---
# <a name="unlock-element-xmla"></a>Elemento Unlock (XMLA)
  Desbloqueia um bloqueio especificado em uma [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Command>  
   <Unlock>  
      <ID>...</ID>  
   </Unlock>  
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
|Elementos filho|[ID](../xml-elements-properties/id-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 O comando `Unlock` remove um bloqueio estabelecido dentro do contexto da transação ativa no momento. Apenas administradores de banco de dados ou servidor podem emitir explicitamente um `Unlock` comando.  
  
 Todos os bloqueios são mantidos no contexto da transação atual. Quando a transação atual é confirmada ou revertida, todos os bloqueios definidos dentro da transação são liberados automaticamente.  
  
## <a name="see-also"></a>Consulte também  
 [Bloquear elemento &#40;XMLA&#41;](lock-element-xmla.md)   
 [Comandos &#40;XMLA&#41;](xml-elements-commands.md)  
  
  