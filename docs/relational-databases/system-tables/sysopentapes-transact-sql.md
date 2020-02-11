---
title: sysopentapes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysopentapes
- sysopentapes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backup media [SQL Server], sysopentapes system table
- sysopentapes system table
ms.assetid: c066ca9b-9cfd-46b1-90a3-5c8dc9e7b6ae
author: stevestein
ms.author: sstein
ms.openlocfilehash: 813592ffa5b67a4926dff611c2ba0e0faf36d273
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68029802"
---
# <a name="sysopentapes-transact-sql"></a>sysopentapes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada dispositivo de fita aberto atualmente. Essa exibição é armazenada no banco de dados **mestre** .  
  
> [!IMPORTANT]  
>  Essa tabela do sistema é incluída como uma exibição para compatibilidade com versões anteriores. Em vez disso, use a exibição de gerenciamento dinâmico de [&#41;de &#40;do Transact-SQL dm_io_backup_tapes](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md) .  
  
> [!NOTE]  
>  Não é possível descartar a exibição **sysopentapes** .  

  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**openTape**|**nvarchar (64)**|Nome de arquivo físico do dispositivo de fita aberto. Para obter mais informações sobre como abrir e liberar dispositivos de fita, consulte [BACKUP &#40;Transact-sql&#41;](../../t-sql/statements/backup-transact-sql.md) e [restaurar &#40;&#41;do Transact-SQL ](../../t-sql/statements/restore-statements-transact-sql.md).|  
  
## <a name="permissions"></a>Permissões  
 O usuário precisa da permissão VIEW SERVER STATE no servidor.  
  
  
