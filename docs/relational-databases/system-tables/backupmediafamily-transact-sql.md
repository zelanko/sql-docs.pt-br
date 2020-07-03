---
title: backupmediafamily (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- backupmediafamily
- backupmediafamily_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backupmediafamily system table
- backup media [SQL Server], backupmediafamily system table
ms.assetid: ee16de24-3d95-4b2e-a094-78df2514d18a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 32afb0e6aaa3e447c9cc2b73121879be93ffc28b
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890675"
---
# <a name="backupmediafamily-transact-sql"></a>backupmediafamily (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para cada família de mídia. Se uma família de mídia residir em um conjunto de mídias espelhado, a família terá uma linha separada para cada espelho no conjunto de mídias. Essa tabela é armazenada no banco de dados **msdb** .  
    
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**media_set_id**|**int**|Número de identificação exclusivo que identifica o conjunto de mídias do qual esta família é um membro. Faz referência a **backupmediaset (media_set_id)**|  
|**family_sequence_number**|**tinyint**|Posição desta família de mídias no conjunto de mídias.|  
|**media_family_id**|**uniqueidentifier**|Número de identificação exclusivo que identifica a família de mídias. Pode ser NULL.|  
|**media_count**|**int**|Número de mídias na família. Pode ser NULL.|  
|**logical_device_name**|**nvarchar(128)**|Nome deste dispositivo de backup em **Sys. backup_devices. Name**. Se esse for um dispositivo de backup temporário (em oposição a um dispositivo de backup permanente que existe em **Sys. backup_devices**), o valor de **logical_device_name** será nulo.|  
|**physical_device_name**|**nvarchar(260)**|Nome físico do dispositivo de backup. Pode ser NULL. Esse campo é compartilhado entre o processo de backup e restauração. Ele pode conter o caminho de destino do backup original ou o caminho de origem da restauração original. Dependendo se o backup ou a restauração ocorreram primeiro em um servidor para um banco de dados. Observe que as restaurações consecutivas do mesmo arquivo de backup não atualizarão o caminho independentemente do local no momento da restauração. Por isso, **physical_device_name** campo não pode ser usado para ver o caminho de restauração usado.|  
|**device_type**|**tinyint**|Tipo de dispositivo de backup:<br /><br /> 2 = Disco<br /><br /> 5 = Fita<br /><br /> 7 = Dispositivo virtual<br /><br /> 9 = armazenamento do Azure<br /><br /> 105 = Um dispositivo de backup.<br /><br /> Pode ser NULL.<br /><br /> Todos os nomes de dispositivo permanentes e números de dispositivo podem ser encontrados em **Sys. backup_devices**.|  
|**physical_block_size**|**int**|Tamanho do bloco físico usado para gravar a família de mídias. Pode ser NULL.|  
|**mirror**|**tinyint**|Número de espelhos (0-3).|  
  
## <a name="remarks"></a>Comentários  
 RESTOre VERIFYONLY de *backup_device* com LOADHISTORY popula as colunas da tabela **backupmediaset** com os valores apropriados do cabeçalho conjunto de mídias.  
  
 Para reduzir o número de linhas nesta tabela e em outras tabelas de backup e histórico, execute o procedimento armazenado [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) .  
  
## <a name="see-also"></a>Consulte Também  
 [Backup e restauração de tabelas &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [conjunto de backup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [Tabelas do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
