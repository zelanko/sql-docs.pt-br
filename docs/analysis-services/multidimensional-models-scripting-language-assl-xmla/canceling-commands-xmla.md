---
title: Cancelando comandos (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
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
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e74ce7bd5b03aa84b6c6580342504148a62a68bf
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="canceling-commands-xmla"></a>Cancelando comandos (XMLA)
  Dependendo das permissões administrativas do usuário que emite o comando, o [Cancelar](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md) comando em XML for Analysis (XMLA) pode cancelar um comando em uma sessão, uma sessão, uma conexão, um processo de servidor ou uma sessão associada ou conexão.  
  
## <a name="canceling-commands"></a>Cancelando comandos  
 Um usuário pode cancelar o comando atualmente em execução dentro do contexto de sessão explícita atual enviando um **Cancelar** comando sem propriedades especificadas.  
  
> [!NOTE]  
>  Um comando em execução em uma sessão implícita não poderá ser cancelado por um usuário.  
  
### <a name="canceling-batch-commands"></a>Cancelando comandos em lote  
 Se um usuário cancela um **lote** comando, em seguida, todos os demais comandos ainda não foi executados dentro de **lote** comando são canceladas. Se o **lote** comando era transacional, quaisquer comandos que foram executadas antes do **Cancelar** execuções de comando são revertidas.  
  
## <a name="canceling-sessions"></a>Cancelando sessões  
 Especificando um identificador de sessão para uma sessão explícita no [SessionID](../../analysis-services/xmla/xml-elements-properties/sessionid-element-xmla.md) propriedade o **Cancelar** de comando, um administrador de banco de dados ou administrador de servidor pode cancelar uma sessão, incluindo o executando o comando. Um administrador de banco de dados só poderá cancelar sessões para bancos de dados nos quais tiver permissões administrativas.  
  
 Um administrador de banco de dados pode recuperar as sessões ativas para um banco de dados especificado recuperando o conjunto de linhas do esquema DISCOVER_SESSIONS. Para recuperar o conjunto de linhas de esquema DISCOVER_SESSIONS, o administrador de banco de dados usa o XMLA **Discover** método e especifica o identificador do banco de dados apropriado para a coluna de restrição SESSION_CURRENT_DATABASE no [Restrições](../../analysis-services/xmla/xml-elements-properties/restrictions-element-xmla.md) propriedade o **Discover** método.  
  
## <a name="canceling-connections"></a>Cancelando conexões  
 Especificando um identificador de conexão no [ConnectionID](../../analysis-services/xmla/xml-elements-properties/connectionid-element-xmla.md) propriedade o **Cancelar** de comando, um administrador de servidor pode cancelar todas as sessões associadas a uma determinada conexão, incluindo todos os executando comandos e cancelar a conexão.  
  
> [!NOTE]  
>  Se a instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não é possível localizar e cancelar as sessões associadas a uma conexão, como quando a bomba de dados abre várias sessões enquanto fornece conectividade HTTP, a instância não é possível cancelar a conexão. Se, nesse caso é encontrado durante a execução de um **Cancelar** de comando, ocorrerá um erro.  
  
 Um administrador de servidor pode recuperar as conexões ativas para um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instância recuperando linhas de esquema DISCOVER_CONNECTIONS usando o XMLA **Discover** método.  
  
## <a name="canceling-server-processes"></a>Cancelando processos do servidor  
 Especificando um identificador de processo do servidor (SPID) no [SPID](../../analysis-services/xmla/xml-elements-properties/spid-element-xmla.md) propriedade o **Cancelar** de comando, um administrador de servidor pode cancelar os comandos associados a um determinado SPID.  
  
## <a name="canceling-associated-sessions-and-connections"></a>Cancelando sessões e conexões associadas  
 Você pode definir o [CancelAssociated](../../analysis-services/xmla/xml-elements-properties/cancelassociated-element-xmla.md) propriedade como true para cancelar os comandos associados com a conexão, sessão ou SPID especificado no, sessões e conexões de **Cancelar** comando.  
  
## <a name="see-also"></a>Consulte também  
 [Descobrir o método &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-methods-discover.md)   
 [Desenvolvendo com XMLA no Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  

