---
title: backupmediaset (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- backupmediaset
- backupmediaset_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backup media [SQL Server], backupmediaset system table
- backupmediaset system table
ms.assetid: d9c18a93-cab9-4db8-ae09-c6bd8145ab8f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1dbaf429acb94334540f0e147eae2808e1655309
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68119352"
---
# <a name="backupmediaset-transact-sql"></a>backupmediaset (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada conjunto de mídias de backup. Essa tabela é armazenada no banco de dados **msdb** .  
 
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**media_set_id**|**int**|Número exclusivo de identificação do conjunto de mídias. Identidade, chave primária.|  
|**media_uuid**|**uniqueidentifier**|O UUID do conjunto de mídias. Todos [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os conjuntos de mídia têm um UUID.<br /><br /> Para versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], no entanto, se um conjunto de mídias contiver apenas uma família de mídia, a coluna **MEDIA_UUID** poderá ser nula (**media_family_count** é 1).|  
|**media_family_count**|**tinyint**|Número de famílias de mídias no conjunto de mídias. Pode ser NULL.|  
|**name**|**nvarchar(128)**|Nome do conjunto de mídias. Pode ser NULL.<br /><br /> Para obter mais informações, consulte MEDIAname e MEDIADESCRIPTION no [BACKUP &#40;&#41;Transact-SQL ](../../t-sql/statements/backup-transact-sql.md).|  
|**ndescrição**|**nvarchar (255)**|Descrição textual do conjunto de mídias. Pode ser NULL.<br /><br /> Para obter mais informações, consulte MEDIAname e MEDIADESCRIPTION no [BACKUP &#40;&#41;Transact-SQL ](../../t-sql/statements/backup-transact-sql.md).|  
|**software_name**|**nvarchar(128)**|Nome do software de backup que gravou o rótulo da mídia. Pode ser NULL.|  
|**software_vendor_id**|**int**|Número de identificação do fornecedor de software que gravou o rótulo de backup da mídia. Pode ser NULL.<br /><br /> O valor de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é 0x1200 hexadecimal.|  
|**MTF_major_version**|**tinyint**|Número de versão principal do formato de fita do [!INCLUDE[msCoName](../../includes/msconame-md.md)] usado para gerar este conjunto de mídias. Pode ser NULL.|  
|**mirror_count**|**tinyint**|Número de espelhos no conjunto de mídias.|  
|**is_password_protected**|**bit**|É o conjunto de mídias protegido por senha:<br /><br /> 0 = Não protegido<br /><br /> 1 = Protegido|  
|**is_compressed**|**bit**|Se o backup é compactado:<br /><br /> 0 = Não compactado<br /><br /> 1 = Compactado<br /><br /> Durante uma atualização do **msdb** , esse valor é definido como nulo. o que indica um backup não compactado.|  
|**is_encrypted**|**Parte**|Se o backup for criptografado:<br /><br /> 0 = não criptografado<br /><br /> 1 = Criptografado|  
  
## <a name="remarks"></a>Comentários  
 RESTOre VERIFYONLY de *backup_device* com LOADHISTORY popula as colunas da tabela **backupmediaset** com os valores apropriados do cabeçalho conjunto de mídias.  
  
 Para reduzir o número de linhas nesta tabela e em outras tabelas de backup e histórico, execute o procedimento armazenado [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) .  
  
## <a name="see-also"></a>Consulte Também  
 [Backup e restauração de tabelas &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [&#41;backupfilegroup &#40;Transact-SQL](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [&#41;backupmediafamily &#40;Transact-SQL](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [&#41;do conjunto de backup &#40;Transact-SQL](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [Tabelas do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
