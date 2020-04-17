---
title: Restrições às conexões regulares e de contexto | Microsoft Docs
description: Este artigo descreve as restrições associadas ao código em execução no processo do Microsoft SQL Server através de contexto e conexões regulares.
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
ms.openlocfilehash: fac92658366cceffc3d4fac5ba650f9a14501185
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81485188"
---
# <a name="context-connections-and-regular-connections---restrictions"></a>Conexões de contexto e conexões normais – Restrições
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico discute as restrições associadas [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] à execução de códigos no processo por meio de contexto e conexões regulares.  
  
## <a name="restrictions-on-context-connections"></a>Restrições em conexões de contexto  
 Ao desenvolver seu aplicativo, leve em consideração as restrições a seguir que se aplicam a conexões de contexto:  
  
-   Você pode ter apenas uma conexão de contexto aberta em um determinado momento para uma determinada conexão. Se você tiver várias instruções em execução simultânea em conexões separadas, cada uma delas poderá obter sua própria conexão de contexto. A restrição não afeta solicitações simultâneas de conexões diferentes; ela afeta apenas uma determinada solicitação em uma determinada conexão.  
  
-   Uma conexão de contexto não oferece suporte a Vários Conjuntos de Resultados Ativos (MARS).  
  
-   A classe **SqlBulkCopy** não opera em uma conexão de contexto.  
  
-   Não existe suporte para a execução de atualizações em lote em uma conexão de contexto.  
  
-   **SqlNotificationRequest** não pode ser usado com comandos que executam contra uma conexão de contexto.  
  
-   Não existe suporte para o cancelamento de comandos que estão sendo executados na conexão de contexto. O método **SqlCommand.Cancel** silenciosamente ignora a solicitação.  
  
-   Nenhuma outra palavra-chave de cadeia de conexão poderá ser usada quando você usar "context connection=true".  
  
-   A propriedade **SqlConnection.DataSource** retorna nula se a seqüência de conexão para o **SqlConnection** for "context connection=true", em vez do nome da instância de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   A configuração da propriedade **SqlCommand.CommandTimeout** não tem efeito quando o comando é executado contra uma conexão de contexto.  
  
## <a name="restrictions-on-regular-connections"></a>Restrições em conexões comuns  
 Ao desenvolver seu aplicativo, leve em consideração as restrições a seguir que se aplicam a conexões comuns:  
  
-   Não existe suporte para a execução assíncrona de comandos em servidores internos. Incluir "async=true" na seqüência de conexão de um comando e, em seguida, executar o comando, resulta em **System.NotSupportedException** sendo lançado. Esta mensagem será exibida: "Não existe suporte para processamento assíncrono quando executado dentro do processo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   O objeto **SqlDependency** não é suportado.  
  
## <a name="see-also"></a>Consulte Também  
 [Conexão de contexto](../../../relational-databases/clr-integration/data-access/context-connection.md)  
  
  
