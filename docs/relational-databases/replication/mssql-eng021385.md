---
title: "MSSQL_ENG021385 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "erro MSSQL_ENG021385"
ms.assetid: a2c0444f-d97b-4760-8905-3574791c2e26
caps.latest.revision: 12
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 12
---
# MSSQL_ENG021385
    
## Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|21385|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Falha no instantâneo ao processar a publicação '%s'. Possivelmente devido à atividade de alteração de esquema ativa ou à adição de novos artigos.|  
  
## Explicação  
 Esse erro é gerado se o Snapshot Agent é executado quando há alterações em andamento no banco de dados de publicação, incluindo adição ou descarte de artigos e alterações de esquema nos objetos publicados.  
  
## Ação do usuário  
 Reinicie o Snapshot Agent após a conclusão das alterações no banco de dados de publicação. Para obter mais informações, consulte [Iniciar e parar um agente de replicação e 40; SQL Server Management Studio e 41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) e [conceitos dos executáveis do Replication Agent](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
## Consulte também  
 [Erros e eventos referência & #40. Replicação e 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  