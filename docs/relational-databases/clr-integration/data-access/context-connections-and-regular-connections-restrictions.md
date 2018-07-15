---
title: Restrições em conexões de contexto e normais | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: 0c6fe4cb-d846-40b5-8884-35a9c770f5e8
caps.latest.revision: 24
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6e3f290a689cc1914548204e95a3a690d045a7d4
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37358158"
---
# <a name="context-connections-and-regular-connections---restrictions"></a>Conexões de contexto e conexões normais – restrições
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico discute as restrições associadas à execução de código na [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] processo por meio do contexto e conexões normais.  
  
## <a name="restrictions-on-context-connections"></a>Restrições em conexões de contexto  
 Ao desenvolver seu aplicativo, leve em consideração as restrições a seguir que se aplicam a conexões de contexto:  
  
-   Você pode ter apenas uma conexão de contexto aberta em um determinado momento para uma determinada conexão. Se você tiver várias instruções em execução simultânea em conexões separadas, cada uma delas poderá obter sua própria conexão de contexto. A restrição não afeta solicitações simultâneas de conexões diferentes; ela afeta apenas uma determinada solicitação em uma determinada conexão.  
  
-   Uma conexão de contexto não oferece suporte a Vários Conjuntos de Resultados Ativos (MARS).  
  
-   O **SqlBulkCopy** classe não opera em uma conexão de contexto.  
  
-   Não existe suporte para a execução de atualizações em lote em uma conexão de contexto.  
  
-   **SqlNotificationRequest** não pode ser usado com comandos que são executadas em uma conexão de contexto.  
  
-   Não existe suporte para o cancelamento de comandos que estão sendo executados na conexão de contexto. O **SqlCommand.Cancel** método ignora a solicitação silenciosamente.  
  
-   Nenhuma outra palavra-chave de cadeia de conexão poderá ser usada quando você usar "context connection=true".  
  
-   O **SqlConnection.DataSource** propriedade retornará nula se a conexão de cadeia de caracteres para o **SqlConnection** é "conexão de contexto = true", em vez do nome da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Definindo o **SqlCommand.CommandTimeout** propriedade não tem nenhum efeito quando o comando é executado em uma conexão de contexto.  
  
## <a name="restrictions-on-regular-connections"></a>Restrições em conexões comuns  
 Ao desenvolver seu aplicativo, leve em consideração as restrições a seguir que se aplicam a conexões comuns:  
  
-   Não existe suporte para a execução assíncrona de comandos em servidores internos. Incluindo "async = true" na cadeia de conexão de um comando e, em seguida, executar o comando resulta em **System. NotSupportedException** que está sendo gerada. Esta mensagem será exibida: "Não existe suporte para processamento assíncrono quando executado dentro do processo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   **SqlDependency** não há suporte para o objeto.  
  
## <a name="see-also"></a>Consulte também  
 [Conexão de contexto](../../../relational-databases/clr-integration/data-access/context-connection.md)  
  
  
