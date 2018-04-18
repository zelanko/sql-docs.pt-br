---
title: backupfilegroup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- backupfilegroup_TSQL
- backupfilegroup
dev_langs:
- TSQL
helpviewer_keywords:
- filegroups [SQL Server], backupfilegroup system table
- backupfilegroup system table
ms.assetid: d26e8fbe-f5c5-4e10-b2bd-0d8e16ea21f9
caps.latest.revision: 53
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e3a0ffb005b52f4460415f166a6edc197218671d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="backupfilegroup-transact-sql"></a>backupfilegroup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada grupo de arquivos em um banco de dados no momento do backup. **backupfilegroup** é armazenado no **msdb** banco de dados.  
  
> [!NOTE]  
>  O **backupfilegroup** tabela mostra a configuração do grupo de arquivos do banco de dados, não do conjunto de backup. Para identificar se um arquivo está incluído no conjunto de backup, use o **is_present** coluna o [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md) tabela.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**backup_set_id**|**Int**|Conjunto de backup que contém este grupo de arquivos.|  
|**name**|**sysname**|Nome do grupo de arquivos.|  
|**filegroup_id**|**Int**|ID de grupo de arquivos, exclusivo no banco de dados. Corresponde à **data_space_id** na **sys. filegroups**.|  
|**filegroup_guid**|**uniqueidentifier**|Identificador Global Exclusivo do grupo de arquivos. Pode ser NULL.|  
|**type**|**char(2)**|Tipo de conteúdo, um de:<br /><br /> FG = Grupo de arquivos de “linhas”<br /><br /> SL = Grupo de arquivos de log do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**type_desc**|**nvarchar(60)**|Descrição de tipo de função, um de:<br /><br /> ROWS_FILEGROUP<br /><br /> SQL_LOG_FILEGROUP|  
|**is_default**|**bit**|O grupo de arquivos padrão, usado quando nenhum grupo de arquivos é especificado em CREATE TABLE ou CREATE INDEX.|  
|**is_readonly**|**bit**|1 = O grupo de arquivos é somente leitura.|  
|**log_filegroup_guid**|**uniqueidentifier**|Pode ser NULL.|  
  
## <a name="remarks"></a>Remarks  
  
> [!IMPORTANT]  
>  O mesmo nome de grupo de arquivos pode aparecer em bancos de dados diferentes; porém, cada grupo de arquivos tem seu próprio GUID. Portanto, **(backup_set_id, filegroup_guid)** é uma chave exclusiva que identifica um grupo de arquivos em **backupfilegroup**.  
  
 RESTORE VERIFYONLY FROM *backup_device* WITH LOADHISTORY preenche as colunas da **backupmediaset** tabela com os valores apropriados do cabeçalho de conjunto de mídias.  
  
 Para reduzir o número de linhas nessa tabela e em outras tabelas de histórico e de backup, execute o [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) procedimento armazenado.  
  
## <a name="see-also"></a>Consulte também  
 [Backup e restauração tabelas &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [conjunto de backup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [Tabelas do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
