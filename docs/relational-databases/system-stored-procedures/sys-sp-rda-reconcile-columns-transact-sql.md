---
title: sys.sp_rda_reconcile_columns (Transact-SQL) | Microsoft Docs
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1d077da2847a430b2a225ea896b1eafd289218a6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47603954"
---
# <a name="syssprdareconcilecolumns-transact-sql"></a>sys.sp_rda_reconcile_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Reconcilia as colunas na tabela do Azure remota para as colunas na a tabela do SQL Server habilitados para Stretch.  
    
  **sp_rda_reconcile_columns** adiciona colunas à tabela remota existentes na tabela do SQL Server habilitados para Stretch, mas não na tabela remota. Essas colunas podem ser colunas que foram acidentalmente excluídas da tabela remota. No entanto, **sp_rda_reconcile_columns** não exclui colunas da tabela remota existentes na tabela remota, mas não na tabela do SQL Server.
  
  > [!IMPORTANT]
  > Quando **sp_rda_reconcile_columns** recria colunas que foram acidentalmente excluídas da tabela remota, ele não restaura os dados que estavam anteriormente nas colunas excluídas.
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
   
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_rda_reconcile_columns @objname = '@objname'  
  
```  
  
## <a name="arguments"></a>Argumentos  
 \@objname = '*\@objname*'  
 O nome da tabela do SQL Server habilitados para Stretch.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou >0 (falha)  
  
## <a name="permissions"></a>Permissões  
 Exige permissões db_owner.  
   
## <a name="remarks"></a>Comentários  
 Se houver colunas na tabela remota do Azure que não existem mais na tabela do SQL Server habilitada para Stretch, essas colunas extras não impedirão o funcionamento normal do Stretch Database. Opcionalmente, é possível remover as colunas extras manualmente.  
  
## <a name="example"></a>Exemplo  
 Para reconciliar as colunas na tabela do Azure remota, execute a seguinte instrução.  
  
```sql  
EXEC sp_rda_reconcile_columns @objname = N'StretchEnabledTableName';  
```  
  
  
