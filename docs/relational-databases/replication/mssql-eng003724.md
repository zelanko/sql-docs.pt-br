---
title: "MSSQL_ENG003724 | Microsoft Docs"
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
  - "erro MSSQL_ENG003724"
ms.assetid: 10cb119d-92df-4124-b85d-cd2f2666c99c
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# MSSQL_ENG003724
    
## Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|3724|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Não é possível %S_MSG o %S_MSG '%.*ls' porque está sendo usado para replicação.|  
  
## Explicação  
 Quando os objetos em um banco de dados são replicados, eles são marcados como replicados na tabela do sistema **sysarticles** (para instantâneo e publicações transacionais) ou **sysmergearticles** (para publicações de mesclagem). Se tentar descartar um objeto replicado, ocorrerá esse erro.  
  
## Ação do usuário  
 Certifique-se de que o objeto de banco de dados não está replicado antes de tentar descartá-lo. Por exemplo:  
  
-   Se o erro ocorrer no banco de dados de publicação, descarte o artigo da publicação antes de descartar o objeto. Para obter mais informações, consulte [Adicionar e descartar artigos de publicações existentes](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
-   Se o erro ocorrer no banco de dados de assinatura, descarte a assinatura antes de descartar o objeto. Para obter mais informações, consulte [assinar publicações](../../relational-databases/replication/subscribe-to-publications.md). Para assinaturas de publicações transacionais, é possível descartar a assinatura de um artigo individual em vez de toda a publicação. Para obter mais informações, consulte [sp_dropsubscription & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md).  
  
 Se esse erro ocorrer em um banco de dados não replicado, execute [sp_removedbreplication & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) para garantir que os objetos no banco de dados não estiverem marcados como replicados.  
  
## Consulte também  
 [Erros e eventos referência & #40. Replicação e 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  