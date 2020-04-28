---
title: logmarkhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- logmarkhistory
- logmarkhistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- logmarkhistory system table
ms.assetid: 5c1becc5-f34e-4869-bf69-dfafab684540
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0674bf993087b349d4e8b6f9947c65167e94df8e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68001807"
---
# <a name="logmarkhistory-transact-sql"></a>logmarkhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada transação marcada que foi confirmada. Essa tabela é armazenada no banco de dados **msdb** .  
  

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|Banco de dados local onde transação marcada ocorreu.|  
|**mark_name**|**nvarchar(128)**|Nome fornecido pelo usuário para a transação marcada.|  
|**ndescrição**|**nvarchar (255)**|Descrição fornecida pelo usuário da transação marcada. Pode ser NULL.|  
|**user_name**|**nvarchar(128)**|Nome do usuário de banco de dados que executou transação marcada. Pode ser NULL.|  
|**lsn**|**numeric(25,0)**|Número de sequência do log do registro da transação onde a marca ocorreu.|  
|**mark_time**|**datetime**|Hora da confirmação da transação marcada (hora local).|  
  
## <a name="see-also"></a>Consulte Também  
 [Restaurar um banco de dados para uma transação marcada &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)   
 [Use transações marcadas para recuperar bancos de dados relacionados de forma consistente &#40;modelo de recuperação completa&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)   
 [Tabelas do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
