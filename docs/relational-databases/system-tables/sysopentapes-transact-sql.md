---
title: sysopentapes (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c899ae69ff42eff84bd85a3553c4ff3f1b64c651
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="sysopentapes-transact-sql"></a>sysopentapes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada dispositivo de fita aberto atualmente. Essa exibição é armazenada no **mestre** banco de dados.  
  
> [!IMPORTANT]  
>  Essa tabela do sistema é incluída como uma exibição para compatibilidade com versões anteriores. Em vez disso, use o [sys.DM io_backup_tapes &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md) exibição de gerenciamento dinâmico.  
  
> [!NOTE]  
>  Não é possível descartar o **sysopentapes** exibição.  

  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**openTape**|**nvarchar(64)**|Nome de arquivo físico do dispositivo de fita aberto. Para obter mais informações sobre abertura e liberação de dispositivos de fita, consulte [BACKUP &#40; Transact-SQL &#41; ](../../t-sql/statements/backup-transact-sql.md) e [restauração &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-transact-sql.md).|  
  
## <a name="permissions"></a>Permissões  
 O usuário precisa da permissão VIEW SERVER STATE no servidor.  
  
  
