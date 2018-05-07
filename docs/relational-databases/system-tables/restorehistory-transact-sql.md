---
title: RestoreHistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- restorehistory
- restorehistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- restorehistory system table
ms.assetid: 9140ecc1-d912-4d76-ae70-e2a857da6d44
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 72f788cf3248ba87bfa4ded7efed219ef3043cf5
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="restorehistory-transact-sql"></a>restorehistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada operação de restauração. Essa tabela é armazenada no **msdb** banco de dados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**restore_history_id**|**Int**|Número de identificação exclusivo que identifica cada operação de restauração. Identidade, chave primária.|  
|**restore_date**|**datetime**|Data e hora da conclusão da operação de restauração. Pode ser NULL.|  
|**destination_database_name**|**nvarchar(128)**|Nome do banco de dados de destino para a operação de restauração. Pode ser NULL.|  
|**user_name**|**nvarchar(128)**|Nome do usuário que realizou a operação de restauração. Pode ser NULL.|  
|**backup_set_id**|**Int**|Número de identificação exclusivo que identifica o backup que está sendo restaurado. Referências **backupset (backup_set_id)**.|  
|**restore_type**|**char(1)**|Tipo de operação de restauração:<br /><br /> D = Banco de dados<br /><br /> F = Arquivo<br /><br /> G = Grupos de arquivos<br /><br /> I = Diferencial<br /><br /> L = Log<br /><br /> V = Verifyonly<br /><br /> Pode ser NULL.|  
|**replace**|**bit**|Indica se a operação de restauração especificou a opção REPLACE:<br /><br /> 1 = Especificada<br /><br /> NULL = Não especificada<br /><br /> Pode ser NULL.<br /><br /> Quando um banco de dados é revertido a um instantâneo do banco de dados, 0 é a única opção.|  
|**recuperação**|**bit**|Indica se a operação de restauração especificou a opção RECOVERY ou NORECOVERY:<br /><br /> 1 = RECOVERY<br /><br /> Pode ser NULL.<br /><br /> Quando um banco de dados é revertido para um instantâneo do banco de dados, 1 é a única opção.<br /><br /> 0 = NORECOVERY|  
|**restart**|**bit**|Indica se a operação de restauração especificou a opção RESTART:<br /><br /> 1 = Especificada<br /><br /> NULL = Não especificada<br /><br /> Pode ser NULL.<br /><br /> Quando um banco de dados é revertido a um instantâneo do banco de dados, 0 é a única opção.|  
|**stop_at**|**datetime**|Ponto específico em que o banco de dados foi recuperado. Pode ser NULL.|  
|**device_count**|**tinyint**|Número de dispositivos envolvidos na operação de restauração. Esse número pode ser menor do que o número de famílias de mídia para o backup. Pode ser NULL.<br /><br /> Quando um banco de dados é revertido a um instantâneo do banco de dados, o número é sempre 1.|  
|**stop_at_mark_name**|**nvarchar(128)**|Indica recuperação para a transação que contém a marca nomeada. Pode ser NULL.<br /><br /> Quando um banco de dados é revertido a um instantâneo do banco de dados, esse valor é sempre NULL.|  
|**stop_before**|**bit**|Indica se a transação que contém a marca nomeada foi incluída na recuperação.<br /><br /> 0 = A recuperação parou antes da transação marcada.<br /><br /> 1 = A recuperação incluiu a transação marcada.<br /><br /> Pode ser NULL.<br /><br /> Quando um banco de dados é revertido a um instantâneo do banco de dados, esse valor é sempre NULL.|  
  
## <a name="remarks"></a>Remarks  
 Para reduzir o número de linhas nessa tabela e em outras tabelas de histórico e de backup, execute o [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) procedimento armazenado.  
  
## <a name="see-also"></a>Consulte também  
 [Backup e restauração tabelas &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [restorefile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/restorefile-transact-sql.md)   
 [restorefilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/restorefilegroup-transact-sql.md)   
 [Tabelas do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
