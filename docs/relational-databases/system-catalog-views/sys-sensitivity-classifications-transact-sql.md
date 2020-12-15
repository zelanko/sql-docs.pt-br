---
description: sys.sensitivity_classifications (Transact-SQL)
title: sys.sensitivity_classifications (Transact-SQL) | Microsoft Docs
ms.date: 03/25/2019
ms.reviewer: ''
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
ms.custom: ''
ms.author: mibar
author: barmichal
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
- rank
monikerRange: '>= sql-server-ver15 || = azuresqldb-current || = azure-sqldw-latest'
ms.openlocfilehash: 908151d19df364171063bffcd280786a354c2654
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472947"
---
# <a name="syssensitivity_classifications-transact-sql"></a>sys.sensitivity_classifications (Transact-SQL)
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

Retorna uma linha para cada item classificado no banco de dados.

|Nome da coluna|Tipo de dados|Descrição|
|-----------------|---------------|-----------------|  
|**class**|**int**|Identifica a classe do item no qual a classificação existe. Sempre terá o valor 1 (representando uma coluna)|  
|**class_desc**|**varchar (16)**|Uma descrição da classe do item no qual a classificação existe. sempre terá o valor *OBJECT_OR_COLUMN*|  
|**major_id**|**int**|Representa a ID da tabela que contém a coluna classificada, correspondente a sys. All _objects. object_id|  
|**minor_id**|**int**|Representa a ID da coluna na qual a classificação existe, correspondente a sys. All _columns. column_id|   
|**label**|**sysname**|O rótulo (legível por humanos) atribuído para a classificação de sensibilidade|  
|**label_id**|**sysname**|Uma ID associada ao rótulo, que pode ser usada por um sistema de proteção de informações, como a proteção de informações do Azure (AIP)|  
|**information_type**|**sysname**|O tipo de informação (legível humana) atribuído para a classificação de sensibilidade|  
|**information_type_id**|**sysname**|Uma ID associada ao tipo de informação, que pode ser usada por um sistema de proteção de informações, como a proteção de informações do Azure (AIP)|  
|**Fique**|**int**|Um valor numérico da classificação: <br><br>0 para nenhum<br>10 para baixo<br>20 para média<br>30 para alta<br>40 para crítico| 
|**rank_desc**|**sysname**|Representação textual da classificação:  <br><br>NENHUM, BAIXO, MÉDIO, ALTO, CRÍTICO|  
| &nbsp; | &nbsp; | &nbsp; |

## <a name="remarks"></a>Comentários  

- Essa exibição fornece visibilidade do estado de classificação do banco de dados. Ele pode ser usado para gerenciar as classificações de banco de dados, bem como para gerar relatórios.
- Atualmente, há suporte apenas para a classificação de colunas de banco de dados.
 
## <a name="examples"></a>Exemplos

### <a name="a-listing-all-classified-columns-and-their-corresponding-classification"></a>a. Listando todas as colunas classificadas e sua classificação correspondente

O exemplo a seguir retorna uma tabela que lista o nome da tabela, o nome da coluna, o rótulo, a ID do rótulo, o tipo de informação, a ID do tipo de informação, a classificação e a descrição da classificação para cada coluna classificada no banco de dados.

> [!NOTE]
> O rótulo é uma palavra-chave para o Azure Synapse Analytics.

```sql
SELECT
    SCHEMA_NAME(sys.all_objects.schema_id) as SchemaName,
    sys.all_objects.name AS [TableName], sys.all_columns.name As [ColumnName],
    [Label], [Label_ID], [Information_Type], [Information_Type_ID], [Rank], [Rank_Desc]
FROM
          sys.sensitivity_classifications
left join sys.all_objects on sys.sensitivity_classifications.major_id = sys.all_objects.object_id
left join sys.all_columns on sys.sensitivity_classifications.major_id = sys.all_columns.object_id
                         and sys.sensitivity_classifications.minor_id = sys.all_columns.column_id
```

## <a name="permissions"></a>Permissões  
 Requer a permissão **View any sensibilidade de classificação** . 
 
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  

## <a name="see-also"></a>Consulte Também  

[ADICIONAR CLASSIFICAÇÃO DE CONFIDENCIALIDADE (Transact-SQL)](../../t-sql/statements/add-sensitivity-classification-transact-sql.md)

[DROP SENSITIVITY CLASSIFICATION (Transact-SQL)](../../t-sql/statements/drop-sensitivity-classification-transact-sql.md)

[Introdução à Proteção de Informações do SQL](/azure/azure-sql/database/data-discovery-and-classification-overview)