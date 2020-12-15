---
description: CHANGE_TRACKING_IS_COLUMN_IN_MASK (Transact-SQL)
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
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e1961dec1f32006d7a4b3d91b7b8763f34ce3514
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97440604"
---
# <a name="change_tracking_is_column_in_mask-transact-sql"></a>CHANGE_TRACKING_IS_COLUMN_IN_MASK (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Interpreta o valor SYS_CHANGE_COLUMNS retornado pela função CHANGEtable (CHANGES...). Permite que um aplicativo determine se a coluna especificada deve ser incluída nos valores retornados para SYS_CHANGE_COLUMNS.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CHANGE_TRACKING_IS_COLUMN_IN_MASK ( column_id , change_columns )  
```  
  
## <a name="arguments"></a>Argumentos  
 *column_id*  
 É a ID da coluna que está sendo verificada. A ID da coluna pode ser obtida usando a função [COLUMNPROPERTY](../../t-sql/functions/columnproperty-transact-sql.md) .  
  
 *change_columns*  
 São os dados binários da coluna SYS_CHANGE_COLUMNS dos dados [CHANGETABLE](../../relational-databases/system-functions/changetable-transact-sql.md) .  
  
## <a name="return-type"></a>Tipo de retorno  
 **bit**  
  
## <a name="return-values"></a>Valores de retorno  
 CHANGE_TRACKING_IS_COLUMN_IN_MASK retorna os seguintes valores.  
  
|Valor retornado|Descrição|  
|------------------|-----------------|  
|0|A coluna especificada não está na lista de *change_columns* .|  
|1|A coluna especificada está na lista de *change_columns* .|  
  
## <a name="remarks"></a>Comentários  
 CHANGE_TRACKING_IS_COLUMN_IN_MASK não executa nenhuma verificação para validar o valor de *column_id* ou que o parâmetro *change_columns* foi obtido da tabela da qual o *column_id* foi obtido.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir determina se a coluna `Salary` da tabela `Employees` foi atualizada. A `COLUMNPROPERTY` função retorna a ID da coluna da `Salary` coluna. A variável local `@change_columns` deve ser definida para os resultados de uma consulta usando CHANGETABLE como fonte de dados.  
  
```sql  
SET @SalaryChanged = CHANGE_TRACKING_IS_COLUMN_IN_MASK  
    (COLUMNPROPERTY(OBJECT_ID('Employees'), 'Salary', 'ColumnId')  
    ,@change_columns);  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções do controle de alterações &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [CHANGETABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/changetable-transact-sql.md)   
 [Controle de alterações de dados &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
