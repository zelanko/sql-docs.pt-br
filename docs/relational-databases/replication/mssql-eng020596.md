---
title: "MSSQL_ENG020596 | Microsoft Docs"
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
  - "erro MSSQL_ENG020596"
ms.assetid: fa33627c-2e99-4be3-9424-52ab83446e07
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# MSSQL_ENG020596
    
## Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|20596|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Somente '%s' ou membros de db_owner podem descartar o agente anônimo.|  
  
## Explicação  
 Você não tem permissões adequadas para descartar o agente da assinatura anônima. O logon usado ao chamar [sp_dropanonymousagent & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-dropanonymousagent-transact-sql.md) deve ser um membro do **sysadmin** a função de servidor fixa no distribuidor ou **db_owner** função de banco de dados fixa no banco de dados de distribuição ou o usuário deve ser feito a primeira execução do agente.  
  
## Ação do usuário  
 Faça logon com as credenciais apropriadas e execute **sp_dropanonymousagent**.  
  
## Consulte também  
 [Erros e eventos referência & #40. Replicação e 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  