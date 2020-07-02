---
title: Restrições em conexões regulares e de contexto | Microsoft Docs
description: Este artigo descreve as restrições associadas ao código em execução no processo de Microsoft SQL Server por meio de conexões de contexto e regulares.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: 0c6fe4cb-d846-40b5-8884-35a9c770f5e8
author: rothja
ms.author: jroth
ms.openlocfilehash: 5491e736bfa075c4cc9f001bc2515184de865ee2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717907"
---
# <a name="context-connections-and-regular-connections---restrictions"></a>Conexões de contexto e conexões normais – Restrições
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  Este tópico discute as restrições associadas ao código em execução no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] processo por meio de contexto e conexões regulares.  
  
## <a name="restrictions-on-context-connections"></a>Restrições em conexões de contexto  
 Ao desenvolver seu aplicativo, leve em consideração as restrições a seguir que se aplicam a conexões de contexto:  
  
-   Você pode ter apenas uma conexão de contexto aberta em um determinado momento para uma determinada conexão. Se você tiver várias instruções em execução simultânea em conexões separadas, cada uma delas poderá obter sua própria conexão de contexto. A restrição não afeta solicitações simultâneas de conexões diferentes; ela afeta apenas uma determinada solicitação em uma determinada conexão.  
  
-   Uma conexão de contexto não oferece suporte a Vários Conjuntos de Resultados Ativos (MARS).  
  
-   A classe **SqlBulkCopy** não funciona em uma conexão de contexto.  
  
-   Não existe suporte para a execução de atualizações em lote em uma conexão de contexto.  
  
-   **SqlNotificationRequest** não pode ser usado com comandos que são executados em uma conexão de contexto.  
  
-   Não existe suporte para o cancelamento de comandos que estão sendo executados na conexão de contexto. O método **SqlCommand. Cancel** ignora silenciosamente a solicitação.  
  
-   Nenhuma outra palavra-chave de cadeia de conexão poderá ser usada quando você usar "context connection=true".  
  
-   A propriedade **SqlConnection. DataSource** retornará NULL se a cadeia de conexão para **SqlConnection** for "context connection = true", em vez do nome da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   Definir a propriedade **SqlCommand. CommandTimeout** não tem efeito quando o comando é executado em uma conexão de contexto.  
  
## <a name="restrictions-on-regular-connections"></a>Restrições em conexões comuns  
 Ao desenvolver seu aplicativo, leve em consideração as restrições a seguir que se aplicam a conexões comuns:  
  
-   Não existe suporte para a execução assíncrona de comandos em servidores internos. Incluir "Async = true" na cadeia de conexão de um comando e, em seguida, executar o comando, resulta em **System. NotSupportedException** que está sendo gerado. Esta mensagem será exibida: "Não existe suporte para processamento assíncrono quando executado dentro do processo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Não há suporte para o objeto **SqlDependency** .  
  
## <a name="see-also"></a>Consulte Também  
 [Conexão de contexto](../../../relational-databases/clr-integration/data-access/context-connection.md)  
  
  
