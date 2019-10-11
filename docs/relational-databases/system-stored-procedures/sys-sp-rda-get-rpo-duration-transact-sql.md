---
title: sys.sp_rda_get_rpo_duration (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_get_rpo_duration
- sys.sp_rda_get_rpo_duration_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_get_rpo_duration stored procedure
ms.assetid: 35882067-3072-47ff-9024-ca453c0f49a7
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 715ceb531f2334f4cf9580c630d922f45faae74e
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252065"
---
# <a name="syssp_rda_get_rpo_duration-transact-sql"></a>sys.sp_rda_get_rpo_duration (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Obtém o número de horas de dados migrados que SQL Server retém em uma tabela de preparo para ajudar a garantir uma restauração completa do banco de dados remoto do Azure, se uma restauração pontual for necessária. 
  
  Para obter mais informações, consulte [Stretch Database reduz o risco de perda de dados para seus dados do Azure mantendo as linhas migradas temporariamente](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md#stretchRPO).  
    
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>Sintaxe    
    
```    
    
sp_rda_get_rpo_duration @durationinhours output    
    
```    
    
## <a name="output-parameter"></a>Parâmetro de saída    
 *\@durationinhours*    
  É o número de horas (um valor inteiro não nulo) de dados migrados que SQL Server retém para o banco de dado habilitado para Stretch atual.    
    
## <a name="permissions"></a>Permissões    
 Requer permissões db_owner.    
    
## <a name="remarks"></a>Comentários    
 Altere o valor executando [Sys. sp_rda_set_rpo_duration &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md).    
    
## <a name="see-also"></a>Consulte também    
 [sys.sp_rda_set_rpo_duration &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md)     
 [Restaurar bancos de dados habilitados para Stretch (Stretch Database)](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)    
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)    
    
  
