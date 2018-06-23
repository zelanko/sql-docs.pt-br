---
title: Elemento Subscribe (XMLA) | Microsoft Docs
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
- Subscribe Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Subscribe
- microsoft.xml.analysis.subscribe
- http://schemas.microsoft.com/analysisservices/2003/engine#Subscribe
helpviewer_keywords:
- Subscribe command
ms.assetid: aad50dd7-44d4-4d83-a973-187f9aed35ec
caps.latest.revision: 14
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 94caa1327febf0c7fd5a489c7558ea793977d027
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012765"
---
# <a name="subscribe-element-xmla"></a>Elemento Subscribe (XMLA)
  Assina um rastreamento e retorna um conjunto de linhas que contém os eventos de rastreamento de um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Command>  
   <Subscribe>  
      <Object>...</Object>  
   </Subscribe>  
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
|Elementos filho|[Objeto](../xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 O `Subscribe` comando assina e devolve um conjunto de linhas de um rastreamento especificado em um [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância. Se um objeto que não seja um rastreamento é especificado no `Object` elemento, um erro ocorre.  
  
 Se o elemento `Object` não for especificado, um rastreamento de sessão será definido e assinado na instância [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. O rastreamento de sessão retorna um conjunto fixo de eventos de rastreamento da sessão atual.  
  
 O fluxo do conjunto de linhas retornado por este comando será finalizado se o aplicativo cliente fecha a conexão para o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância, ou se a sessão na qual o `Subscribe` comando é executado é encerrada.  
  
## <a name="see-also"></a>Consulte também  
 [Comandos &#40;XMLA&#41;](xml-elements-commands.md)  
  
  