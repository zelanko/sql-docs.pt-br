---
title: sys. sp_rda_reconcile_columns (Transact-SQL) | Microsoft Docs
description: Saiba mais sobre sys. sp_rda_reconcile_columns. Use este procedimento armazenado para reconciliar colunas em tabelas remotas do Azure e tabelas de SQL Server habilitadas para Stretch.
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_reconcile_columns
- sys.sp_rda_reconcile_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reconcile_columns stored procedure
ms.assetid: 60d9cc4e-1828-450b-9d88-5b8485800d73
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 939bc5cbe299ce144b8617391fd33d740011b08a
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87245743"
---
# <a name="syssp_rda_reconcile_columns-transact-sql"></a>sys. sp_rda_reconcile_columns (Transact-SQL)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  Reconcilia as colunas na tabela remota do Azure para as colunas na tabela de SQL Server habilitada para Stretch.  
    
  **sp_rda_reconcile_columns** adiciona colunas à tabela remota que existem na tabela de SQL Server habilitada para Stretch, mas não na tabela remota. Essas colunas podem ser colunas que você excluiu acidentalmente da tabela remota. No entanto, **sp_rda_reconcile_columns** não exclui colunas da tabela remota que existem na tabela remota, mas não na tabela SQL Server.
  
  > [!IMPORTANT]
  > Quando **sp_rda_reconcile_columns** recria colunas que foram acidentalmente excluídas da tabela remota, ele não restaura os dados que estavam anteriormente nas colunas excluídas.
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
   
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_rda_reconcile_columns @objname = '@objname'  
  
```  
  
## <a name="arguments"></a>Argumentos  
 \@objname = '* \@ objname*'  
 O nome da tabela de SQL Server habilitada para Stretch.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou >0 (falha)  
  
## <a name="permissions"></a>Permissões  
 Requer db_owner permissões.  
   
## <a name="remarks"></a>Comentários  
 Se houver colunas na tabela remota do Azure que não existem mais na tabela do SQL Server habilitada para Stretch, essas colunas extras não impedirão o funcionamento normal do Stretch Database. Opcionalmente, é possível remover as colunas extras manualmente.  
  
## <a name="example"></a>Exemplo  
 Para reconciliar as colunas na tabela remota do Azure, execute a instrução a seguir.  
  
```sql  
EXEC sp_rda_reconcile_columns @objname = N'StretchEnabledTableName';  
```  
  
  
