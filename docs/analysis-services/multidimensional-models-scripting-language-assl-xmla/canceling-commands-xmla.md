---
title: Cancelando comandos (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 313708ad1575c7b9922ac796791d0d623c51b54b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63182945"
---
# <a name="canceling-commands-xmla"></a>Cancelando comandos (XMLA)
  Dependendo das permissões administrativas do usuário que emite o comando, o [Cancelar](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla) comando no XML for Analysis (XMLA) pode cancelar um comando em uma sessão, uma sessão, uma conexão, um processo do servidor ou uma sessão associada ou conexão.  
  
## <a name="canceling-commands"></a>Cancelando comandos  
 Um usuário pode cancelar o comando atualmente em execução dentro do contexto de sessão explícita atual, enviando uma **Cancelar** comando sem propriedades especificadas.  
  
> [!NOTE]  
>  Um comando em execução em uma sessão implícita não poderá ser cancelado por um usuário.  
  
### <a name="canceling-batch-commands"></a>Cancelando comandos em lote  
 Se um usuário cancela uma **lote** comando e, em seguida, todos os demais comandos ainda não executados na **lote** comando são canceladas. Se o **lote** comando era transacional, qualquer que foram executadas antes do **Cancelar** execuções de comando são revertidas.  
  
## <a name="canceling-sessions"></a>Cancelando sessões  
 Especificando um identificador de sessão para uma sessão explícita na [SessionID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla) propriedade da **Cancelar** de comando, um administrador de banco de dados ou administrador de servidor pode cancelar uma sessão, incluindo o Executando comando. Um administrador de banco de dados só poderá cancelar sessões para bancos de dados nos quais tiver permissões administrativas.  
  
 Um administrador de banco de dados pode recuperar as sessões ativas para um banco de dados especificado recuperando o conjunto de linhas do esquema DISCOVER_SESSIONS. Para recuperar o conjunto de linhas de esquema DISCOVER_SESSIONS, o administrador de banco de dados usa o XMLA **Discover** método e especifica o identificador do banco de dados apropriado para a coluna de restrição SESSION_CURRENT_DATABASE na [Restrições](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/restrictions-element-xmla) propriedade do **Discover** método.  
  
## <a name="canceling-connections"></a>Cancelando conexões  
 Especificando um identificador de conexão na [ConnectionID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/connectionid-element-xmla) propriedade da **Cancelar** de comando, um administrador de servidor pode cancelar todas as sessões associadas a uma determinada conexão, incluindo todos os executando comandos e cancelar a conexão.  
  
> [!NOTE]
>  Se a instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não é possível localizar e cancelar as sessões associadas a uma conexão, como quando a bomba de dados abre várias sessões enquanto fornece conectividade HTTP, a instância não é possível cancelar a conexão. Se esse caso é encontrado durante a execução de um **Cancelar** de comando, ocorre um erro.  
  
 Um administrador de servidor pode recuperar as conexões ativas para um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instância recuperando o conjunto de linhas de esquema DISCOVER_CONNECTIONS usando o XMLA **Discover** método.  
  
## <a name="canceling-server-processes"></a>Cancelando processos do servidor  
 Especificando um identificador de processo do servidor (SPID) na [SPID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla) propriedade da **Cancelar** de comando, um administrador de servidor pode cancelar os comandos associados a um determinado SPID.  
  
## <a name="canceling-associated-sessions-and-connections"></a>Cancelando sessões e conexões associadas  
 Você pode definir as [CancelAssociated](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cancelassociated-element-xmla) propriedade como true para cancelar as conexões, sessões e comandos associados com a conexão, sessão ou SPID especificado na **Cancelar** comando.  
  
## <a name="see-also"></a>Consulte também  
 [Descobrir o método &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)   
 [Desenvolvendo com XMLA no Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
