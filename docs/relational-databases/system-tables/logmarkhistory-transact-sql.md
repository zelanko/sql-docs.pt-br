---
title: logmarkhistory (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- logmarkhistory
- logmarkhistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- logmarkhistory system table
ms.assetid: 5c1becc5-f34e-4869-bf69-dfafab684540
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5d4948a79bfd4b529b87cd0f5c223e302172a26a
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="logmarkhistory-transact-sql"></a>logmarkhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada transação marcada que foi confirmada. Essa tabela é armazenada no **msdb** banco de dados.  
  

|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|Banco de dados local onde transação marcada ocorreu.|  
|**mark_name**|**nvarchar(128)**|Nome fornecido pelo usuário para a transação marcada.|  
|**description**|**nvarchar(255)**|Descrição fornecida pelo usuário da transação marcada. Pode ser NULL.|  
|**user_name**|**nvarchar(128)**|Nome do usuário de banco de dados que executou transação marcada. Pode ser NULL.|  
|**lsn**|**numeric(25,0)**|Número de sequência do log do registro da transação onde a marca ocorreu.|  
|**mark_time**|**datetime**|Hora da confirmação da transação marcada (hora local).|  
  
## <a name="see-also"></a>Consulte também  
 [Restaurar um banco de dados para uma transação marcada &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)   
 [Usar transações marcadas para recuperar bancos de dados relacionados de forma consistente &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)   
 [System Tables &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
