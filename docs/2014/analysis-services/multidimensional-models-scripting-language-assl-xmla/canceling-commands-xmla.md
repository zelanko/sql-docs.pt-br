---
title: Cancelando comandos (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
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
ms.openlocfilehash: 80bddac8f800c1b9394c1ed605007ab0f2137b88
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62727460"
---
# <a name="canceling-commands-xmla"></a>Cancelando comandos (XMLA)
  Dependendo das permissões administrativas do usuário que está emitindo o comando, o comando [Cancel](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla) no XML for Analysis (XMLA) pode cancelar um comando em uma sessão, uma sessão, uma conexão, um processo do servidor ou uma sessão ou conexão associada.  
  
## <a name="canceling-commands"></a>Cancelando comandos  
 Um usuário pode cancelar o comando em execução no contexto da sessão explícita atual ao enviar um comando `Cancel` sem propriedades especificadas.  
  
> [!NOTE]  
>  Um comando em execução em uma sessão implícita não poderá ser cancelado por um usuário.  
  
### <a name="canceling-batch-commands"></a>Cancelando comandos em lote  
 Se um usuário cancelar um comando `Batch`, todos os comandos restantes ainda não executados no comando `Batch` serão cancelados. Se o comando `Batch` for transacional, qualquer comando executado antes do comando `Cancel` será revertido.  
  
## <a name="canceling-sessions"></a>Cancelando sessões  
 Ao especificar um identificador de sessão para uma sessão explícita na propriedade [SessionID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla) do `Cancel` comando, um administrador de banco de dados ou um administrador de servidor pode cancelar uma sessão, incluindo o comando atualmente em execução. Um administrador de banco de dados só poderá cancelar sessões para bancos de dados nos quais tiver permissões administrativas.  
  
 Um administrador de banco de dados pode recuperar as sessões ativas para um banco de dados especificado recuperando o conjunto de linhas do esquema DISCOVER_SESSIONS. Para recuperar o conjunto de linhas de esquema DISCOVER_SESSIONS, o administrador de `Discover` banco de dados usa o método XMLA e especifica o identificador de banco de dados apropriado para a `Discover` coluna de restrição SESSION_CURRENT_DATABASE na propriedade [Restrictions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/restrictions-element-xmla) do método.  
  
## <a name="canceling-connections"></a>Cancelando conexões  
 Ao especificar um identificador de conexão na propriedade [ConnectionID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/connectionid-element-xmla) do `Cancel` comando, um administrador de servidor pode cancelar todas as sessões associadas a uma determinada conexão, incluindo todos os comandos em execução e cancelar a conexão.  
  
> [!NOTE]  
>  Se a instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não puder localizar e cancelar as sessões associadas a uma conexão, como quando a bomba de dados abrir várias sessões ao fornecer conectividade http, a instância não poderá cancelar a conexão. Se esse for o caso durante a execução de um comando `Cancel`, ocorrerá um erro.  
  
 Um administrador do servidor pode recuperar as conexões ativas para uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] recuperando o conjunto de linhas do esquema DISCOVER_CONNECTIONS que usa o método `Discover` XMLA.  
  
## <a name="canceling-server-processes"></a>Cancelando processos do servidor  
 Ao especificar um identificador de processo de servidor (SPID) na propriedade [SPID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla) do `Cancel` comando, um administrador de servidor pode cancelar os comandos associados a um determinado SPID.  
  
## <a name="canceling-associated-sessions-and-connections"></a>Cancelando sessões e conexões associadas  
 Você pode definir a propriedade [CancelAssociated](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cancelassociated-element-xmla) como true para cancelar as conexões, as sessões e os comandos associados à conexão, à sessão ou ao SPID especificados no `Cancel` comando.  
  
## <a name="see-also"></a>Consulte Também  
 [Método Discover &#40;&#41;XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)   
 [Desenvolvendo com XMLA no Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
