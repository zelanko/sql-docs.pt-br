---
title: sys.sp_rda_reconcile_batch (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_reconcile_batch
- sys.sp_rda_reconcile_batch_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reconcile_batch stored procedure
ms.assetid: 6d21eac3-7b6c-4fe0-8bc4-bf503f3948a6
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 88a14afd9dd1dfb944a64e9f62d5f02328a2aa05
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="syssprdareconcilebatch-transact-sql"></a>sys.sp_rda_reconcile_batch (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Reconcilia a ID do lote armazenada na tabela do SQL Server habilitado para Stretch com a ID de lote armazenada na tabela remota do Azure.  
  
 Normalmente você só precisa executar **sp_rda_reconcile_batch** se você excluiu manualmente os dados migrados mais recentemente da tabela remota. Quando você excluir manualmente os dados remotos que inclui o lote mais recente, as IDs de lote estão fora de sincronia e para de migração.  
 
 Para excluir os dados que já tem sido migrados para o Azure, consulte os comentários nesta página.
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
   
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_rda_reconcile_batch @objname = '@objname'  
  
```  
  
## <a name="arguments"></a>Argumentos  
 @objname = '*@objname*'  
 O nome da tabela do SQL Server habilitados para Stretch.  
  
## <a name="permissions"></a>Permissões  
 Requer permissões db_owner.  
  
## <a name="remarks"></a>Remarks  
 Se você quiser excluir dados que já tem sido migrados para o Azure, siga estas etapas.  
  
1.  Pausar a migração de dados. Para obter mais informações, consulte [Pausar e retomar a migração de dados &#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).  
  
2.  Exclua os dados da tabela de preparo do SQL Server executando um comando DELETE com a dica STAGE_ONLY. Para obter mais informações, consulte [fazer exclusões e atualizações administrativas](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md#adminHints).
  
3.  Exclua os mesmos dados da tabela remota do Azure executando um comando DELETE com a dica REMOTE_ONLY.  
  
4.  Executar **sp_rda_reconcile_batch**.  
  
5.  Retomar a migração de dados. Para obter mais informações, consulte [Pausar e retomar a migração de dados &#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).  
  
## <a name="example"></a>Exemplo  
 Para reconciliar as IDs de lote, execute a seguinte instrução.  
  
```sql  
EXEC sp_rda_reconcile_batch @objname = N'StretchEnabledTableName';  
```  
  
  
