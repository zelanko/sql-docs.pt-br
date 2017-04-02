---
title: "MSSQL_ENG014144 | Microsoft Docs"
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
  - "erro MSSQL_ENG014144"
ms.assetid: fdc744d5-530e-48c4-9420-cca032fd482b
caps.latest.revision: 12
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 12
---
# MSSQL_ENG014144
    
## Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|14144|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Não é possível descartar o Assinante '%s'. Existem assinaturas para ele no banco de dados de publicação '%s'.|  
  
## Explicação  
 Uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurada como Assinante não pode ser removida da função de Assinante enquanto houver assinaturas ativas configuradas para a instância.  
  
## Ação do usuário  
 Descarte todas as assinaturas associadas antes de tentar alterar o status Assinante da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
1.  Executar [sp_helpsubscription & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md) o banco de dados de publicação no Editor para localizar inscrições.  
  
2.  Executar [sp_dropsubscription & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md) o banco de dados de publicação para descartar inscrições.  
  
## Consulte também  
 [Erros e eventos referência & #40. Replicação e 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  
  