---
title: restorefile (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- restorefile
- restorefile_TSQL
dev_langs: TSQL
helpviewer_keywords:
- restorefile system table
- restoring files [SQL Server], restorefile system table
- file restores [SQL Server], restorefile system table
ms.assetid: 8e40145a-8559-4abe-8e2a-39b818928009
caps.latest.revision: "34"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 803b8ec7682c1d3b40f339f1aef9c144e307053e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="restorefile-transact-sql"></a>restorefile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada arquivo restaurado, inclusive arquivos restaurados indiretamente por nome de grupo de arquivos. Essa tabela é armazenada no **msdb** banco de dados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**restore_history_id**|**int**|Número de identificação exclusivo que identifica a operação de restauração correspondente. Referências **RestoreHistory (restore_history_id)**.|  
|**file_number**|**numeric(10,0)**|Número de identificação do arquivo restaurado. Esse número deve ser exclusivo em cada banco de dados. Pode ser NULL.<br /><br /> Quando um banco de dados é revertido para um instantâneo do banco de dados, esse valor é preenchido da mesma maneira que uma restauração completa.|  
|**destination_phys_drive**|**nvarchar (260)**|Unidade ou partição para a qual o arquivo foi restaurado. Pode ser NULL.<br /><br /> Quando um banco de dados é revertido para um instantâneo do banco de dados, esse valor é preenchido da mesma maneira que uma restauração completa.|  
|**destination_phys_name**|**nvarchar (260)**|Nome do arquivo, sem as informações de unidade ou partição, onde o arquivo foi restaurado. Pode ser NULL.<br /><br /> Quando um banco de dados é revertido para um instantâneo do banco de dados, esse valor é preenchido da mesma maneira que uma restauração completa.|  
  
## <a name="remarks"></a>Comentários  
 Para reduzir o número de linhas nessa tabela e em outras tabelas de histórico e de backup, execute o [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) procedimento armazenado.  
  
## <a name="see-also"></a>Consulte também  
 [Backup e restauração tabelas &#40; Transact-SQL &#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [restorefilegroup &#40; Transact-SQL &#41;](../../relational-databases/system-tables/restorefilegroup-transact-sql.md)   
 [RestoreHistory &#40; Transact-SQL &#41;](../../relational-databases/system-tables/restorehistory-transact-sql.md)   
 [Tabelas do sistema &#40; Transact-SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
