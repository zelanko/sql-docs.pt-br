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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7dc119aaaf24457bc9267ee750ce82a9a4a69104
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47687254"
---
# <a name="backupmediafamily-transact-sql"></a>backupmediafamily (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada família de mídia. Se uma família de mídia residir em um conjunto de mídias espelhado, a família terá uma linha separada para cada espelho no conjunto de mídias. Essa tabela é armazenada na **msdb** banco de dados.  
    
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**media_set_id**|**int**|Número de identificação exclusivo que identifica o conjunto de mídias do qual esta família é um membro. Referências **backupmediaset (media_set_id)**|  
|**family_sequence_number**|**tinyint**|Posição desta família de mídias no conjunto de mídias.|  
|**media_family_id**|**uniqueidentifier**|Número de identificação exclusivo que identifica a família de mídias. Pode ser NULL.|  
|**media_count**|**int**|Número de mídias na família. Pode ser NULL.|  
|**logical_device_name**|**nvarchar(128)**|Nome do dispositivo de backup no **backup_devices**. Quando se trata de um dispositivo de backup temporário (em vez de um dispositivo de backup permanente que existe no **sys. backup_devices**), o valor de **logical_device_name** é NULL.|  
|**physical_device_name**|**nvarchar(260)**|Nome físico do dispositivo de backup. Pode ser NULL. Este campo é compartilhado entre o processo de backup e restauração. Ele pode conter o caminho de destino de backup original ou o caminho de origem de restauração original. Dependendo de se backup ou restauração ocorreu pela primeira vez em um servidor para um banco de dados. Observe que restaurações consecutivas do mesmo arquivo de backup não atualizará o caminho, independentemente de sua localização no momento da restauração. Por isso, **physical_device_name** campo não pode ser usado para ver o caminho de restauração usado.|  
|**device_type**|**tinyint**|Tipo de dispositivo de backup:<br /><br /> 2 = Disco<br /><br /> 5 = Fita<br /><br /> 7 = Dispositivo virtual<br /><br /> 9 = armazenamento do azure<br /><br /> 105 = Um dispositivo de backup.<br /><br /> Pode ser NULL.<br /><br /> Todos os nomes de dispositivos permanentes e números de dispositivo podem ser encontrados no **sys. backup_devices**.|  
|**physical_block_size**|**int**|Tamanho do bloco físico usado para gravar a família de mídias. Pode ser NULL.|  
|**mirror**|**tinyint**|Número de espelhos (0-3).|  
  
## <a name="remarks"></a>Comentários  
 RESTORE VERIFYONLY FROM *backup_device* WITH LOADHISTORY preenche as colunas da **backupmediaset** tabela com os valores apropriados do cabeçalho de conjunto de mídias.  
  
 Para reduzir o número de linhas nessa tabela e em outras tabelas de histórico e backup, execute as [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) procedimento armazenado.  
  
## <a name="see-also"></a>Consulte também  
 [Backup e restauração de tabelas &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [conjunto de backup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [Tabelas do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
