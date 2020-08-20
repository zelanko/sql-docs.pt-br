---
description: restorefile (Transact-SQL)
title: restaurarfile (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- restorefile
- restorefile_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- restorefile system table
- restoring files [SQL Server], restorefile system table
- file restores [SQL Server], restorefile system table
ms.assetid: 8e40145a-8559-4abe-8e2a-39b818928009
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 82dc6bf152f9ba0a951536357f2d7147ba4e5960
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460308"
---
# <a name="restorefile-transact-sql"></a>restorefile (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para cada arquivo restaurado, inclusive arquivos restaurados indiretamente por nome de grupo de arquivos. Essa tabela é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**restore_history_id**|**int**|Número de identificação exclusivo que identifica a operação de restauração correspondente. Faz referência a **RestoreHistory (restore_history_id)**.|  
|**file_number**|**numeric (10, 0)**|Número de identificação do arquivo restaurado. Esse número deve ser exclusivo em cada banco de dados. Pode ser NULL.<br /><br /> Quando um banco de dados é revertido para um instantâneo do banco de dados, esse valor é preenchido da mesma maneira que uma restauração completa.|  
|**destination_phys_drive**|**nvarchar(260)**|Unidade ou partição para a qual o arquivo foi restaurado. Pode ser NULL.<br /><br /> Quando um banco de dados é revertido para um instantâneo do banco de dados, esse valor é preenchido da mesma maneira que uma restauração completa.|  
|**destination_phys_name**|**nvarchar(260)**|Nome do arquivo, sem as informações de unidade ou partição, onde o arquivo foi restaurado. Pode ser NULL.<br /><br /> Quando um banco de dados é revertido para um instantâneo do banco de dados, esse valor é preenchido da mesma maneira que uma restauração completa.|  
  
## <a name="remarks"></a>Comentários  
 Para reduzir o número de linhas nesta tabela e em outras tabelas de backup e histórico, execute o procedimento armazenado [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) .  
  
## <a name="see-also"></a>Consulte Também  
 [Backup e restauração de tabelas &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [&#41;restorefilegroup &#40;Transact-SQL ](../../relational-databases/system-tables/restorefilegroup-transact-sql.md)   
 [&#41;RestoreHistory &#40;Transact-SQL ](../../relational-databases/system-tables/restorehistory-transact-sql.md)   
 [Tabelas do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
