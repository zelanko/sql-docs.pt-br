---
title: "MSSQL_ENG018456 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "erro MSSQL_ENG018456"
ms.assetid: 3daa8144-d81f-445a-b6c3-4bb3e9fd1526
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# MSSQL_ENG018456
    
## Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do Evento|18456|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Falha de logon do usuário ' %. * ls'.%.\*ls|  
  
## Explicação  
 O erro MSSQL_ENG018456 ocorre sempre que uma tentativa de logon falha. Se a mensagem de erro inclui a conta **distributor_admin** (Falha de logon do usuário 'distributor_admin'.), o problema é com uma conta usada pela replicação. A replicação cria um servidor remoto, **repl_distributor**, que permite a comunicação entre o distribuidor e publicador. O logon **distributor_admin** está associado esse servidor remoto e deve ter uma senha válida.  
  
## Ação do usuário  
 Certifique-se de ter especificado uma senha para a conta. Para obter mais informações, consulte [proteger o distribuidor](../../relational-databases/replication/security/secure-the-distributor.md).  
  
## Consulte também  
 [Erros e eventos referência & #40. Replicação e 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  