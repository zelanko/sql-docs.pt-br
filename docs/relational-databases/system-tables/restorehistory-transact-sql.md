---
title: RestoreHistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- restorehistory
- restorehistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- restorehistory system table
ms.assetid: 9140ecc1-d912-4d76-ae70-e2a857da6d44
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 50823db39b3369c5e9f2fe54b8acbbe5dd424fc0
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827164"
---
# <a name="restorehistory-transact-sql"></a>restorehistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada operação de restauração. Essa tabela é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**restore_history_id**|**int**|Número de identificação exclusivo que identifica cada operação de restauração. Identidade, chave primária.|  
|**restore_date**|**datetime**|Data e hora do início da operação de restauração. Pode ser NULL.|  
|**destination_database_name**|**nvarchar(128)**|Nome do banco de dados de destino para a operação de restauração. Pode ser NULL.|  
|**user_name**|**nvarchar(128)**|Nome do usuário que realizou a operação de restauração. Pode ser NULL.|  
|**backup_set_id**|**int**|Número de identificação exclusivo que identifica o backup que está sendo restaurado. Faz referência a **backupset (backup_set_id)**.|  
|**restore_type**|**Char (1)**|Tipo de operação de restauração:<br /><br /> D = Banco de dados<br /><br /> F = Arquivo<br /><br /> G = Grupos de arquivos<br /><br /> I = Diferencial<br /><br /> L = Log<br /><br /> V = Verifyonly<br /><br /> Pode ser NULL.|  
|**replace**|**bit**|Indica se a operação de restauração especificou a opção REPLACE:<br /><br /> 1 = Especificada<br /><br /> NULL = Não especificada<br /><br /> Pode ser NULL.<br /><br /> Quando um banco de dados é revertido a um instantâneo do banco de dados, 0 é a única opção.|  
|**recuperação**|**bit**|Indica se a operação de restauração especificou a opção RECOVERY ou NORECOVERY:<br /><br /> 1 = RECOVERY<br /><br /> Pode ser NULL.<br /><br /> Quando um banco de dados é revertido para um instantâneo de banco de dados, 1 é a única opção.<br /><br /> 0 = NORECOVERY|  
|**restart**|**bit**|Indica se a operação de restauração especificou a opção RESTART:<br /><br /> 1 = Especificada<br /><br /> NULL = Não especificada<br /><br /> Pode ser NULL.<br /><br /> Quando um banco de dados é revertido a um instantâneo do banco de dados, 0 é a única opção.|  
|**stop_at**|**datetime**|Ponto específico em que o banco de dados foi recuperado. Pode ser NULL.|  
|**device_count**|**tinyint**|Número de dispositivos envolvidos na operação de restauração. Esse número pode ser menor do que o número de famílias de mídia para o backup. Pode ser NULL.<br /><br /> Quando um banco de dados é revertido a um instantâneo do banco de dados, o número é sempre 1.|  
|**stop_at_mark_name**|**nvarchar(128)**|Indica recuperação para a transação que contém a marca nomeada. Pode ser NULL.<br /><br /> Quando um banco de dados é revertido a um instantâneo do banco de dados, esse valor é sempre NULL.|  
|**stop_before**|**bit**|Indica se a transação que contém a marca nomeada foi incluída na recuperação.<br /><br /> 0 = A recuperação parou antes da transação marcada.<br /><br /> 1 = A recuperação incluiu a transação marcada.<br /><br /> Pode ser NULL.<br /><br /> Quando um banco de dados é revertido a um instantâneo do banco de dados, esse valor é sempre NULL.|  
  
## <a name="remarks"></a>Comentários  
 Para reduzir o número de linhas nesta tabela e em outras tabelas de backup e histórico, execute o procedimento armazenado [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) .  
  
## <a name="see-also"></a>Consulte Também  
 [Backup e restauração de tabelas &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [restaurarfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/restorefile-transact-sql.md)   
 [&#41;restorefilegroup &#40;Transact-SQL](../../relational-databases/system-tables/restorefilegroup-transact-sql.md)   
 [Tabelas do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
