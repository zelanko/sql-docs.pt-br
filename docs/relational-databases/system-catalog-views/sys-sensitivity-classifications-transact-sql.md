---
title: sys.sensitivity_classifications (Transact-SQL) | Microsoft Docs
ms.date: 06/17/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: sql-database
ms.service: sql-database
ms.technology: t-sql
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.custom: ''
ms.manager: craigg
ms.author: giladm
author: giladmit
f1_keywords:
- 'sys.sensitivity_classifications '
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sensitivity_classifications statement
- dropping labels
- drop labels
- removing labels
- remove labels
- classification [SQL]
- labels [SQL]
- information types
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: d0adbbeb82c06d6a44f3a7439bcbf479d7358401
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37993788"
---
# <a name="syssensitivityclassifications-transact-sql"></a>sys.sensitivity_classifications (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

Retorna uma linha para cada item classificado no banco de dados.

|Nome da coluna|Tipo de dados|Description|
|-----------------|---------------|-----------------|  
|**class**|**int**|Identifica a classe do item no qual existe a classificação|  
|**class_desc**|**varchar(16)**|Uma descrição da classe do item no qual existe a classificação|  
|**major_id**|**int**|ID do item no qual existe a classificação. < br \>< br \>se a classe for 0, major_id será sempre 0.<br>Se a classe for 1, 2 ou 7, major_id será object_id.|  
|**minor_id**|**int**|ID secundária do item no qual a classificação está presente, interpretada de acordo com sua classe.<br><br>Se classe = 1, minor_id será column_id (se coluna), ou 0 (se objeto).<br>Se class = 2, minor_id será parameter_id.<br>Se classe = 7, minor_id será index_id. |  
|**label**|**sysname**|O rótulo (legíveis) atribuído para a classificação de confidencialidade|  
|**label_id**|**sysname**|Uma ID associada com o rótulo, que pode ser usado por um sistema de proteção de informações, como proteção de informações do Azure (AIP)|  
|**information_type**|**sysname**|O tipo de informações (legíveis) atribuído para a classificação de confidencialidade|  
|**information_type_id**|**sysname**|Uma ID associada com o tipo de informação, que pode ser usado por um sistema de proteção de informações, como proteção de informações do Azure (AIP)|  
| &nbsp; | &nbsp; | &nbsp; |

## <a name="remarks"></a>Remarks  

- Essa exibição fornece visibilidade sobre o estado de classificação do banco de dados. Ele pode ser usado para gerenciar as classificações de banco de dados, bem como para geração de relatórios.
- Há suporte para a classificação no momento, somente de colunas de banco de dados. Consequentemente:
    - **classe** -sempre terá o valor 1 (representando uma coluna)
    - **class_desc** -sempre terá o valor *OBJECT_OR_COLUMN*
    - **major_id** -representa a ID da tabela que contém a coluna classificada, correspondente com sys.all_objects.object_id
    - **minor_id** -representa a ID da coluna na qual a classificação existe, correspondente com sys.all_columns.column_id

## <a name="examples"></a>Exemplos

### <a name="a-listing-all-classified-columns-and-their-corresponding-classification"></a>A. Classificado listando todas as colunas e sua classificação correspondente

A exemplo a seguir retorna uma tabela que lista o nome da tabela, o nome da coluna, o rótulo, ID, tipo de informação, ID de tipo de informações para cada coluna classificada no banco de dados do rótulo.

```sql
SELECT
    sys.all_objects.name AS TableName, sys.all_columns.name As ColumnName,
    Label, Label_ID, Information_Type, Information_Type_ID
FROM
          sys.sensitivity_classifications
left join sys.all_objects on sys.sensitivity_classifications.major_id = sys.all_objects.object_id
left join sys.all_columns on sys.sensitivity_classifications.major_id = sys.all_columns.object_id
                         and sys.sensitivity_classifications.minor_id = sys.all_columns.column_id
```

## <a name="see-also"></a>Consulte também  

[Adicionar CLASSIFICTION de SENSIBILIDADE (Transact-SQL)](../../t-sql/statements/add-sensitivity-classification-transact-sql.md)

[Descartar CLASSIFICTION SENSIBILIDADE (Transact-SQL)](../../t-sql/statements/drop-sensitivity-classification-transact-sql.md)

[Introdução à proteção de informações do SQL](http://aka.ms/sqlip)
