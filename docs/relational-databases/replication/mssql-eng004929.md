---
title: "MSSQL_ENG004929 | Microsoft Docs"
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
  - "erro MSSQL_ENG004929"
ms.assetid: 1d9b1d88-1fbf-4089-b392-687d3b0220ca
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# MSSQL_ENG004929
    
## Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|4929|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Não é possível alterar %S_MSG '%.*ls' porque ele está sendo publicado para replicação.|  
  
## Explicação  
 Geralmente, esse erro ocorre ao tentar descartar a restrição de chave primária em uma tabela publicada para replicação transacional. As replicações transacionais exigem uma chave primária para cada tabela publicada; portanto, não é possível descartar a restrição.  
  
## Ação do usuário  
 Para descartar a restrição, primeiro descarte o artigo associado à tabela. Para obter mais informações, consulte [Adicionar e descartar artigos de publicações existentes](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md). Se esse erro ocorrer em um banco de dados não replicado, execute [sp_removedbreplication & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) para garantir que os objetos no banco de dados não estiverem marcados como replicados.  
  
## Consulte também  
 [Erros e eventos referência & #40. Replicação e 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  