---
title: sys. sp_rda_reconcile_batch (Transact-SQL) | Microsoft Docs
description: Saiba como usar sys. sp_rda_reconcile_batch para reconciliar a ID de lote na tabela de SQL Server habilitada para Stretch com a ID de lote armazenada na tabela remota do Azure.
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_reconcile_batch
- sys.sp_rda_reconcile_batch_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reconcile_batch stored procedure
ms.assetid: 6d21eac3-7b6c-4fe0-8bc4-bf503f3948a6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 744d863e22bad3dc84ed1fd46350926228b01607
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541019"
---
# <a name="syssp_rda_reconcile_batch-transact-sql"></a>sys. sp_rda_reconcile_batch (Transact-SQL)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  Reconcilia a ID de lote armazenada na tabela de SQL Server habilitada para Stretch com a ID de lote armazenada na tabela remota do Azure.  
  
 Normalmente, você só precisa executar **sp_rda_reconcile_batch** se tiver excluído manualmente os dados migrados mais recentemente da tabela remota. Quando você exclui manualmente os dados remotos que incluem o lote mais recente, as IDs de lote estão fora de sincronização e a migração é interrompida.  
 
 Para excluir dados que já foram migrados para o Azure, consulte os comentários nesta página.
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
   
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_rda_reconcile_batch @objname = '@objname'  
  
```  
  
## <a name="arguments"></a>Argumentos  
 \@objname = '* \@ objname*'  
 O nome da tabela de SQL Server habilitada para Stretch.  
  
## <a name="permissions"></a>Permissões  
 Requer db_owner permissões.  
  
## <a name="remarks"></a>Comentários  
 Se você quiser excluir dados que já foram migrados para o Azure, faça o seguinte.  
  
1.  Pausar migração de dados. Para obter mais informações, consulte [Pausar e retomar a migração de dados &#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).  
  
2.  Exclua os dados da tabela SQL Server preparo executando um comando DELETE com a dica STAGE_ONLY. Para obter mais informações, consulte [fazer atualizações administrativas e exclusões](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md#adminHints).
  
3.  Exclua os mesmos dados da tabela remota do Azure executando um comando DELETE com a dica REMOTE_ONLY.  
  
4.  Execute **sp_rda_reconcile_batch**.  
  
5.  Retome a migração de dados. Para obter mais informações, consulte [Pausar e retomar a migração de dados &#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).  
  
## <a name="example"></a>Exemplo  
 Para reconciliar as IDs de lote, execute a instrução a seguir.  
  
```sql  
EXEC sp_rda_reconcile_batch @objname = N'StretchEnabledTableName';  
```  
  
  
