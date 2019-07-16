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
ms.openlocfilehash: 15a188a912d9338b6e786248e9242914d5759196
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905079"
---
# <a name="syssprdagetrpoduration-transact-sql"></a>sys.sp_rda_get_rpo_duration (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Obtém o número de horas de dados migrados que o SQL Server mantém em uma tabela de preparo para ajudar a garantir uma restauração completa do Azure banco de dados remoto, se um ponto de restauração pontual é necessário. 
  
  Para obter mais informações, consulte [Stretch Database reduz o risco de perda de dados para os dados do Azure retendo temporariamente as linhas migradas](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md#stretchRPO).  
    
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>Sintaxe    
    
```    
    
sp_rda_get_rpo_duration @durationinhours output    
    
```    
    
## <a name="output-parameter"></a>Parâmetro de saída    
 *@durationinhours*    
  É o número de horas (um valor inteiro não nulo) de dados migrados que o SQL Server retém do atual banco de dados habilitados para Stretch.    
    
## <a name="permissions"></a>Permissões    
 Exige permissões db_owner.    
    
## <a name="remarks"></a>Comentários    
 Alterar o valor executando [sp_rda_set_rpo_duration &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md).    
    
## <a name="see-also"></a>Consulte também    
 [sys.sp_rda_set_rpo_duration &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md)     
 [Restaurar bancos de dados habilitados para Stretch (Stretch Database)](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)    
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)    
    
  
