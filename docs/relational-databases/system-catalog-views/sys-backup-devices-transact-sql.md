---
description: sys.backup_devices (Transact-SQL)
title: sys. backup_devices (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- backup_devices_TSQL
- backup_devices
- sys.backup_devices
- sys.backup_devices_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backup devices [SQL Server], viewing information
- sys.backup_devices catalog view
ms.assetid: 457edaa4-aca1-4bd3-bf8d-734490b80fcd
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b58bfc803d66b8782631ec4fd3d9223041dbce73
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551471"
---
# <a name="sysbackup_devices-transact-sql"></a>sys.backup_devices (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para cada dispositivo de backup registrado usando **sp_addumpdevice** ou criado em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do dispositivo de backup. É exclusivo no conjunto.|  
|**tipo**|**tinyint**|Tipo de dispositivo de backup:<br /><br /> 2 = Disco<br /><br /> 3 = Disquete (obsoleto)<br /><br /> 5 = Fita<br /><br /> 6 = Pipe (obsoleto)<br /><br /> 7 = Dispositivo virtual (para uso opcional por fornecedores terceirizados de backup)<br /><br /> 9 = URL<br /><br />Normalmente, apenas o disco (2) e a URL (9) são usados.|  
|**type_desc**|**nvarchar(60)**|Descrição do tipo de dispositivo de backup.<br /><br /> DISK<br /><br /> DISKETTE (obsoleto)<br /><br /> TAPE<br /><br /> PIPE (obsoleto)<br /><br /> VIRTUAL_DEVICE (para uso opcional por fornecedores terceirizados de backup)<br /><br /> URL <br /><br /> Normalmente, somente o disco e a URL são usados.|  
|**physical_name**|**nvarchar(260)**|O nome de arquivo ou caminho físico do dispositivo de backup.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [Exibição de catálogo do bancos de dados e de arquivos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [Consultando as perguntas frequentes do catálogo do sistema do SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
