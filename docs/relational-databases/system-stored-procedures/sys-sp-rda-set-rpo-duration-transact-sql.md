---
title: sys. sp_rda_set_rpo_duration (Transact-SQL) | Microsoft Docs
description: Saiba mais sobre sys. sp_rda_set_rpo_duration. Use este procedimento armazenado para definir o número de horas de dados migrados que SQL Server retém em uma tabela de preparo.
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_set_rpo_duration
- sys.sp_rda_set_rpo_duration_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_set_rpo_duration stored procedure
ms.assetid: 95c80c5b-9252-4612-9ea7-544c48834fd2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d37717f2b2c8a3dad804538a9268e64023776422
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540431"
---
# <a name="syssp_rda_set_rpo_duration-transact-sql"></a>sys. sp_rda_set_rpo_duration (Transact-SQL)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  Define o número de horas de dados migrados que SQL Server retém em uma tabela de preparo para ajudar a garantir uma restauração completa do banco de dados remoto do Azure, se uma restauração pontual for necessária.    
    
 Para obter mais informações, consulte [Stretch Database reduz o risco de perda de dados para seus dados do Azure mantendo as linhas migradas temporariamente](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md#stretchRPO).  
   
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
     
## <a name="syntax"></a>Sintaxe    
    
```    
    
sp_rda_set_rpo_duration [ @duration_hrs = ] duration_hrs    
    
```    
    
## <a name="arguments"></a>Argumentos    
 [ @duration_hrs =] *duration_hrs*    
 É o número de horas (um valor inteiro não nulo) de dados migrados que você deseja que SQL Server retenha para o banco de dado habilitado para Stretch atual. O valor padrão e o valor mínimo são 8 horas.    
 
 > [!NOTE]
 > Valores mais altos exigem mais espaço de armazenamento em SQL Server.
    
## <a name="permissions"></a>Permissões    
 Requer db_owner permissões.    
    
## <a name="remarks"></a>Comentários    
 Obtenha o valor atual executando [Sys. sp_rda_get_rpo_duration &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md).    
    
## <a name="see-also"></a>Consulte Também    
 [sys. sp_rda_get_rpo_duration &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md)     
 [Restaurar bancos de dados habilitados para Stretch (Stretch Database)](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)     
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)    
    
  
