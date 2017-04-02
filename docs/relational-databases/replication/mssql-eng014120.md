---
title: "MSSQL_ENG014120 | Microsoft Docs"
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
  - "erro MSSQL_ENG014120"
ms.assetid: 6b169a3b-30da-4981-b998-b52d61811572
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# MSSQL_ENG014120
    
## Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|14120|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Não foi possível descartar o banco de dados de distribuição '%s'. O banco de dados do distribuidor está associado a um Publicador.|  
  
## Explicação  
 O banco de dados de distribuição armazena metadados e dados de histórico para todos os tipos de replicação e transações para replicação transacional. Esse erro ocorre ao tentar descartar um banco de dados de distribuição associado a um ou mais Publicadores.  
  
## Ação do usuário  
 Para descartar um banco de dados de distribuição, é necessário primeiro descartar a associação entre o Distribuidor e o Publicador. Para obter mais informações, consulte [sp_dropdistpublisher & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md).  
  
## Consulte também  
 [Erros e eventos referência & #40. Replicação e 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Configurar a distribuição](../../relational-databases/replication/configure-distribution.md)  
  
  