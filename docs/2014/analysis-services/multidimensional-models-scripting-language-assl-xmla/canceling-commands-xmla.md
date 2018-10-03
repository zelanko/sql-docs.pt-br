---
title: Cancelando comandos (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- connections [XML for Analysis]
- associated connections [XML for Analysis]
- XML for Analysis, canceling
- associated sessions [XML for Analysis]
- canceling connections
- canceling commands
- canceling sessions
- SPID
- XMLA, canceling
- server process IDs [XML for Analysis]
- sessions [XML for Analysis]
ms.assetid: b59f8197-c33d-4e65-9022-848ccba540f5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d3b622700843e83f3308874d44a4c6af132b4d89
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48171936"
---
# <a name="canceling-commands-xmla"></a>Cancelando comandos (XMLA)
  Dependendo das permissões administrativas do usuário que emite o comando, o [Cancelar](../xmla/xml-elements-commands/cancel-element-xmla.md) comando no XML for Analysis (XMLA) pode cancelar um comando em uma sessão, uma sessão, uma conexão, um processo do servidor ou uma sessão associada ou conexão.  
  
## <a name="canceling-commands"></a>Cancelando comandos  
 Um usuário pode cancelar o comando em execução no contexto da sessão explícita atual ao enviar um comando `Cancel` sem propriedades especificadas.  
  
> [!NOTE]  
>  Um comando em execução em uma sessão implícita não poderá ser cancelado por um usuário.  
  
### <a name="canceling-batch-commands"></a>Cancelando comandos em lote  
 Se um usuário cancelar um comando `Batch`, todos os comandos restantes ainda não executados no comando `Batch` serão cancelados. Se o comando `Batch` for transacional, qualquer comando executado antes do comando `Cancel` será revertido.  
  
## <a name="canceling-sessions"></a>Cancelando sessões  
 Especificando um identificador de sessão para uma sessão explícita na [SessionID](../xmla/xml-elements-properties/id-element-xmla.md) propriedade do `Cancel` de comando, um administrador de banco de dados ou administrador de servidor pode cancelar uma sessão, incluindo o comando atualmente em execução . Um administrador de banco de dados só poderá cancelar sessões para bancos de dados nos quais tiver permissões administrativas.  
  
 Um administrador de banco de dados pode recuperar as sessões ativas para um banco de dados especificado recuperando o conjunto de linhas do esquema DISCOVER_SESSIONS. Para recuperar o conjunto de linhas de esquema DISCOVER_SESSIONS, o administrador de banco de dados usa o XMLA `Discover` método e especifica o identificador do banco de dados apropriado para a coluna de restrição SESSION_CURRENT_DATABASE o [restrições](../xmla/xml-elements-properties/restrictions-element-xmla.md) propriedade do `Discover` método.  
  
## <a name="canceling-connections"></a>Cancelando conexões  
 Especificando um identificador de conexão na [ConnectionID](../xmla/xml-elements-properties/connectionid-element-xmla.md) propriedade do `Cancel` de comando, um administrador de servidor pode cancelar todas as sessões associadas a uma determinada conexão, incluindo todos os comandos em execução, e Cancele a conexão.  
  
> [!NOTE]  
>  Se a instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não é possível localizar e cancelar as sessões associadas a uma conexão, como quando a bomba de dados abre várias sessões enquanto fornece conectividade HTTP, a instância não é possível cancelar a conexão. Se esse for o caso durante a execução de um comando `Cancel`, ocorrerá um erro.  
  
 Um administrador do servidor pode recuperar as conexões ativas para uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] recuperando o conjunto de linhas do esquema DISCOVER_CONNECTIONS que usa o método `Discover` XMLA.  
  
## <a name="canceling-server-processes"></a>Cancelando processos do servidor  
 Especificando um identificador de processo do servidor (SPID) na [SPID](../xmla/xml-elements-properties/spid-element-xmla.md) propriedade do `Cancel` de comando, um administrador de servidor pode cancelar os comandos associados a um determinado SPID.  
  
## <a name="canceling-associated-sessions-and-connections"></a>Cancelando sessões e conexões associadas  
 Você pode definir as [CancelAssociated](../xmla/xml-elements-properties/cancelassociated-element-xmla.md) propriedade como true para cancelar as conexões, sessões e comandos associados com a conexão, sessão ou SPID especificado no `Cancel` comando.  
  
## <a name="see-also"></a>Consulte também  
 [Descobrir o método &#40;XMLA&#41;](../xmla/xml-elements-methods-discover.md)   
 [Desenvolvendo com XMLA no Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
