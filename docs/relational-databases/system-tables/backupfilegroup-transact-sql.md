---
description: backupfilegroup (Transact-SQL)
title: backupfilegroup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: dc0f1651c0c5532e387e4b878182a2cb99f66936
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88373932"
---
# <a name="backupfilegroup-transact-sql"></a>backupfilegroup (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para cada grupo de arquivos em um banco de dados no momento do backup. **backupfilegroup** é armazenado no banco de dados **msdb** .  
  
> [!NOTE]  
>  A tabela **backupfilegroup** mostra a configuração do grupo de arquivos do banco de dados, não do conjunto de backup. Para identificar se um arquivo está incluído no conjunto de backup, use a coluna **is_present** da tabela [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md) .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**backup_set_id**|**int**|Conjunto de backup que contém este grupo de arquivos.|  
|**name**|**sysname**|Nome do grupo de arquivos.|  
|**filegroup_id**|**int**|ID de grupo de arquivos, exclusivo no banco de dados. Corresponde a **data_space_id** em **Sys. FileGroups**.|  
|**filegroup_guid**|**uniqueidentifier**|Identificador Global Exclusivo do grupo de arquivos. Pode ser NULL.|  
|**tipo**|**char(2)**|Tipo de conteúdo, um de:<br /><br /> FG = Grupo de arquivos de “linhas”<br /><br /> SL = Grupo de arquivos de log do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**type_desc**|**nvarchar(60)**|Descrição de tipo de função, um de:<br /><br /> ROWS_FILEGROUP<br /><br /> SQL_LOG_FILEGROUP|  
|**is_default**|**bit**|O grupo de arquivos padrão, usado quando nenhum grupo de arquivos é especificado em CREATE TABLE ou CREATE INDEX.|  
|**is_readonly**|**bit**|1 = O grupo de arquivos é somente leitura.|  
|**log_filegroup_guid**|**uniqueidentifier**|Pode ser NULL.|  
  
## <a name="remarks"></a>Comentários  
  
> [!IMPORTANT]  
>  O mesmo nome de grupo de arquivos pode aparecer em bancos de dados diferentes; porém, cada grupo de arquivos tem seu próprio GUID. Portanto, **(backup_set_id, filegroup_guid)** é uma chave exclusiva que identifica um grupo de arquivos no **backupfilegroup**.  
  
 RESTOre VERIFYONLY de *backup_device* com LOADHISTORY popula as colunas da tabela **backupmediaset** com os valores apropriados do cabeçalho conjunto de mídias.  
  
 Para reduzir o número de linhas nesta tabela e em outras tabelas de backup e histórico, execute o procedimento armazenado [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) .  
  
## <a name="see-also"></a>Consulte Também  
 [Backup e restauração de tabelas &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [conjunto de backup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [Tabelas do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
