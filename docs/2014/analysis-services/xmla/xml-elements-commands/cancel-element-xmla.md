---
title: Elemento Cancel (XMLA) | Microsoft Docs
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
- Cancel Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.cancel
- http://schemas.microsoft.com/analysisservices/2003/engine#Cancel
- urn:schemas-microsoft-com:xml-analysis#Cancel
helpviewer_keywords:
- Cancel command
ms.assetid: de4062c1-7434-44dc-9f01-29fcf78963bd
caps.latest.revision: 15
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: cd0fdd50a1dcddb51d167ab76cd5408b631bb3ef
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118433"
---
# <a name="cancel-element-xmla"></a>Elemento Cancel (XMLA)
  Cancela um comando em execução no momento uma [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Command>  
   <Cancel>  
      <ConnectionID>...</ConnectionID>  
      <SessionID>...</SessionID>  
      <SPID>...</SPID>  
      <CancelAssociated>...</CancelAssociated>  
   </Cancel>  
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
|Elementos filho|[CancelAssociated](../xml-elements-properties/cancelassociated-element-xmla.md), [ConnectionID](../xml-elements-properties/id-element-xmla.md), [SessionID](../xml-elements-properties/sessionid-element-xmla.md), [SPID](../xml-elements-properties/spid-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 O comando `Cancel` cancela os comandos que estiverem sendo executados neste momento dentro do contexto de uma sessão. Se o aplicativo cliente não solicitou uma sessão, um comando não poderá ser cancelado.  
  
 Se o comando `Cancel` for executado durante a execução de um comando `Batch`, todo o comando `Batch` será cancelado. Se o comando `Batch` era transacional, todos os comandos contidos no comando `Batch` serão revertidos. Se o comando `Batch` era transacional, todos os comandos contidos no comando `Batch` que estiverem sendo executados no momento em que o comando `Cancel` foi executado serão revertidos. Os comandos não transacionais em um comando `Batch` que foram executados antes, não serão revertidos.  
  
 Normalmente, o comando `Cancel` é usado para cancelar os comandos que estiverem sendo executados no momento em que a sessão estiver ativa. Neste caso, nenhum dos elementos filho do comando `Cancel` deverão ser especificados. O comando `Cancel` também só pode ser usado pelos administradores para cancelar os comandos que estiverem sendo executados em conexões ou sessões que não estejam na sessão ativa naquele momento. Os membros de uma função com permissões de Administrador de um determinado banco de dados podem cancelar os comandos de conexões e sessões aplicáveis a esse banco de dados, enquanto que os administradores de servidor podem cancelar os comandos de conexões e sessões de uma determinada instância do Analysis Services.  
  
 Para recuperar as informações sobre as conexões e as sessões atuais de uma instância [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], o método `Discover` pode ser executado para solicitar, respectivamente, os conjuntos de linhas de esquema DISCOVER_CONNECTIONS e DISCOVER_SESSIONS. Os membros de uma função com permissões de Administrador de um determinado banco de dados só poderão retornar sessões do banco de dados se especificarem o banco de dados na coluna de restrição SESSION_CURRENT_DATABASE do conjunto de linhas de esquema DISCOVER_SESSIONS. Para obter mais informações sobre o `Discover` método, consulte [método descobrir &#40;XMLA&#41;](../xml-elements-methods-discover.md).  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de lote &#40;XMLA&#41;](batch-element-xmla.md)   
 [Comandos &#40;XMLA&#41;](xml-elements-commands.md)  
  
  