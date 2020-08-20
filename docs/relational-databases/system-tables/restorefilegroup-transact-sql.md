---
description: restorefilegroup (Transact-SQL)
title: restorefilegroup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- restorefilegroup_TSQL
- restorefilegroup
dev_langs:
- TSQL
helpviewer_keywords:
- filegroups [SQL Server], restorefilegroup system table
- restorefilegroup system table
ms.assetid: 3aa15c55-6b72-4f76-97d7-bd88391d105c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4dc6f220cec0797b47bfe66a1b79842a9c20fc1c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460279"
---
# <a name="restorefilegroup-transact-sql"></a>restorefilegroup (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para cada grupo de arquivos restaurado. Essa tabela é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**restore_history_id**|**int**|Número de identificação exclusivo que identifica a operação de restauração correspondente. Faz referência a **RestoreHistory (restore_history_id)**.|  
|**filegroup_name**|**nvarchar(128)**|Nome do grupo de arquivos sendo restaurado. Pode ser NULL.<br /><br /> Quando um banco de dados é revertido para um instantâneo do banco de dados, esse valor é preenchido da mesma maneira que uma restauração completa.|  
  
## <a name="remarks"></a>Comentários  
 Para reduzir o número de linhas nesta tabela e em outras tabelas de backup e histórico, execute o procedimento armazenado [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) .  
  
## <a name="see-also"></a>Consulte Também  
 [Backup e restauração de tabelas &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [restaurarfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/restorefile-transact-sql.md)   
 [&#41;RestoreHistory &#40;Transact-SQL ](../../relational-databases/system-tables/restorehistory-transact-sql.md)   
 [Tabelas do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
