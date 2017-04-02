---
title: "MSSQL_ENG014121 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "erro MSSQL_ENG014121"
ms.assetid: c8595854-cce1-4566-ad64-d565555caded
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# MSSQL_ENG014121
    
## Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|14121|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Não foi possível descartar o Distribuidor '%s'. Esse Distribuidor possui bancos de dados de distribuição associados.|  
  
## Explicação  
 Uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurada como Distribuidor não pode ser removida da função de Distribuidor porque existem bancos de dados de distribuição associados a essa instância. Esse erro ocorre ao tentar descartar um banco de dados de distribuição associado a um ou mais Publicadores.  
  
## Ação do usuário  
 Para localizar os nomes de editores e bancos de dados de distribuição associados a esse distribuidor, execute [sp_helpdistpublisher & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md) de qualquer banco de dados no distribuidor.  
  
 Executar [sp_dropdistributiondb & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md) para qualquer banco de dados de distribuição associado ao distribuidor. Após todas as associações de banco de dados de distribuição serem removidas, é possível desabilitar a distribuição.  
  
## Consulte também  
 [Erros e eventos referência & #40. Replicação e 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Configurar a distribuição](../../relational-databases/replication/configure-distribution.md)  
  
  