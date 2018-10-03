---
title: Restrições em conexões de contexto e normais | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: 0c6fe4cb-d846-40b5-8884-35a9c770f5e8
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3b721409f0915cb1e13861f6481909e02af37cb2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48163316"
---
# <a name="restrictions-on-regular-and-context-connections"></a>Restrições em conexões comuns e de contexto
  Este tópico discute as restrições associadas à execução de código no [!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)] processo por meio do contexto e conexões normais.  
  
## <a name="restrictions-on-context-connections"></a>Restrições em conexões de contexto  
 Ao desenvolver seu aplicativo, leve em consideração as restrições a seguir que se aplicam a conexões de contexto:  
  
-   Você pode ter apenas uma conexão de contexto aberta em um determinado momento para uma determinada conexão. Se você tiver várias instruções em execução simultânea em conexões separadas, cada uma delas poderá obter sua própria conexão de contexto. A restrição não afeta solicitações simultâneas de conexões diferentes; ela afeta apenas uma determinada solicitação em uma determinada conexão.  
  
-   Uma conexão de contexto não oferece suporte a Vários Conjuntos de Resultados Ativos (MARS).  
  
-   A classe `SqlBulkCopy` não opera em uma conexão de contexto.  
  
-   Não existe suporte para a execução de atualizações em lote em uma conexão de contexto.  
  
-   `SqlNotificationRequest` não pode ser usado com comandos que são executados em uma conexão de contexto.  
  
-   Não existe suporte para o cancelamento de comandos que estão sendo executados na conexão de contexto. O método `SqlCommand.Cancel` ignora a solicitação silenciosamente.  
  
-   Nenhuma outra palavra-chave de cadeia de conexão poderá ser usada quando você usar "context connection=true".  
  
-   A propriedade `SqlConnection.DataSource` retornará nulo se a cadeia de conexão para `SqlConnection` for "context connection=true", em vez do nome da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Definir a propriedade `SqlCommand.CommandTimeout` não tem nenhum efeito quando o comando é executado em uma conexão de contexto.  
  
## <a name="restrictions-on-regular-connections"></a>Restrições em conexões comuns  
 Ao desenvolver seu aplicativo, leve em consideração as restrições a seguir que se aplicam a conexões comuns:  
  
-   Não existe suporte para a execução assíncrona de comandos em servidores internos. Incluir "async=true" na cadeia de conexão de um comando e, depois, executar o comando resultará na geração de `System.NotSupportedException`. Esta mensagem será exibida: "Não existe suporte para processamento assíncrono quando executado dentro do processo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Não existe suporte para o objeto `SqlDependency`.  
  
## <a name="see-also"></a>Consulte também  
 [Conexão de contexto](context-connection.md)  
  
  
