---
title: sys.sp_rda_reconcile_columns (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_reconcile_columns
- sys.sp_rda_reconcile_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reconcile_columns stored procedure
ms.assetid: 60d9cc4e-1828-450b-9d88-5b8485800d73
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ac447329552758ad6070cf4a22489c9d1ed44e64
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="syssprdareconcilecolumns-transact-sql"></a>sys.sp_rda_reconcile_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Reconcilia as colunas na tabela do Azure remota para as colunas da a tabela do SQL Server habilitado para Stretch.  
    
  **sp_rda_reconcile_columns** adiciona colunas à tabela remota existentes na tabela do SQL Server habilitados para Stretch, mas não na tabela remota. Essas colunas podem ser colunas que foram acidentalmente excluídas da tabela remota. No entanto, **sp_rda_reconcile_columns** não exclui colunas da tabela remota existentes na tabela remota, mas não na tabela do SQL Server.
  
  > [!IMPORTANT]
  > Quando **sp_rda_reconcile_columns** recria colunas que foram acidentalmente excluídas da tabela remota, ele não restaura os dados que estavam anteriormente nas colunas excluídas.
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
   
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_rda_reconcile_columns @objname = '@objname'  
  
```  
  
## <a name="arguments"></a>Argumentos  
 @objname = '*@objname*'  
 O nome da tabela do SQL Server habilitados para Stretch.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou >0 (falha)  
  
## <a name="permissions"></a>Permissões  
 Requer permissões db_owner.  
   
## <a name="remarks"></a>Remarks  
 Se houver colunas na tabela remota do Azure que não existem mais na tabela do SQL Server habilitada para Stretch, essas colunas extras não impedirão o funcionamento normal do Stretch Database. Opcionalmente, é possível remover as colunas extras manualmente.  
  
## <a name="example"></a>Exemplo  
 Para reconciliar as colunas na tabela remota do Azure, execute a seguinte instrução.  
  
```sql  
EXEC sp_rda_reconcile_columns @objname = N'StretchEnabledTableName';  
```  
  
  
