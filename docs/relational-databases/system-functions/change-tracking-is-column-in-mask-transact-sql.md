---
title: CHANGE_TRACKING_IS_COLUMN_IN_MASK (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- CHANGE_TRACKING_IS_COLUMN_IN_MASK_TSQL
- CHANGE_TRACKING_IS_COLUMN_IN_MASK
dev_langs:
- TSQL
helpviewer_keywords:
- change tracking [SQL Server], CHANGE_TRACKING_IS_COLUMN_IN_MASK
- CHANGE_TRACKING_IS_COLUMN_IN_MASK
ms.assetid: 649b370b-da54-4915-919d-1b597a39d505
author: rothja
ms.author: jroth
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 534df29b5ad3422ed3290ce4037490f69f988832
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52535748"
---
# <a name="changetrackingiscolumninmask-transact-sql"></a>CHANGE_TRACKING_IS_COLUMN_IN_MASK (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Interpreta o valor SYS_CHANGE_COLUMNS retornado pela função CHANGETABLE(CHANGES...). Permite que um aplicativo determine se a coluna especificada deve ser incluída nos valores retornados para SYS_CHANGE_COLUMNS.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CHANGE_TRACKING_IS_COLUMN_IN_MASK ( column_id , change_columns )  
```  
  
## <a name="arguments"></a>Argumentos  
 *column_id*  
 É a ID da coluna que está sendo verificada. A coluna ID pode ser obtida usando o [COLUMNPROPERTY](../../t-sql/functions/columnproperty-transact-sql.md) função.  
  
 *change_columns*  
 São os dados binários da coluna SYS_CHANGE_COLUMNS dos [CHANGETABLE](../../relational-databases/system-functions/changetable-transact-sql.md) dados.  
  
## <a name="return-type"></a>Tipo de retorno  
 **bit**  
  
## <a name="return-values"></a>Valores de retorno  
 CHANGE_TRACKING_IS_COLUMN_IN_MASK retorna os seguintes valores.  
  
|Valor retornado|Descrição|  
|------------------|-----------------|  
|0|A coluna especificada não está no *change_columns* lista.|  
|1|A coluna especificada está no *change_columns* lista.|  
  
## <a name="remarks"></a>Comentários  
 CHANGE_TRACKING_IS_COLUMN_IN_MASK não executa nenhuma verificação para validar a *column_id* valor ou que o *change_columns* parâmetro foi obtido a tabela da qual o  *column_id* foi obtido.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir determina se a coluna `Salary` da tabela `Employees` foi atualizada. O `COLUMNPROPERTY` função retorna a ID da coluna a `Salary` coluna. A variável local `@change_columns` deve ser definida para os resultados de uma consulta usando CHANGETABLE como fonte de dados.  
  
```sql  
SET @SalaryChanged = CHANGE_TRACKING_IS_COLUMN_IN_MASK  
    (COLUMNPROPERTY(OBJECT_ID('Employees'), 'Salary', 'ColumnId')  
    ,@change_columns);  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções do controle de alterações &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [CHANGETABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/changetable-transact-sql.md)   
 [Controle de alterações de dados &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
