---
description: sp_special_columns_100 (Azure Synapse Analytics)
title: sp_special_columns_100 (Azure Synapse Analytics)
ms.custom: ''
ms.date: 03/14/2017
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.subservice: design
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5774fadc-77cc-46f8-8f9f-a0f9efe95e21
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 03397db88a1a99e2fbf661662311537671bfa862
ms.sourcegitcommit: 76ab3b57718341c6057613c9bd38cf82fb17786e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92059444"
---
# <a name="sp_special_columns_100-azure-synapse-analytics"></a>sp_special_columns_100 (Azure Synapse Analytics)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Retorna o conjunto ideal de colunas que identificam, de forma exclusiva, uma linha na tabela. Também retorna colunas atualizadas automaticamente quando qualquer valor na linha for atualizado por uma transação.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql  
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
sp_special_columns_100 [ @table_name = ] 'table_name'     
     [ , [ @table_owner = ] 'table_owner' ]   
     [ , [ @qualifier = ] 'qualifier' ]   
     [ , [ @col_type = ] 'col_type' ]   
     [ , [ @scope = ] 'scope' ]  
     [ , [ @nullable = ] 'nullable' ]   
     [ , [ @ODBCVer = ] 'ODBCVer' ]   
[ ; ]  
```

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]
  
## <a name="arguments"></a>Argumentos  
 [ @table_name =] '*table_name*'  
 É o nome da tabela usada para retornar informações do catálogo. o *nome* é **sysname**, sem padrão. Não há suporte para a correspondência de padrão curinga.  
  
 [ @table_owner =] '*TABLE_OWNER*'  
 É o proprietário da tabela usado para retornar as informações do catálogo. *Owner* é **sysname**, com um padrão de NULL. Não há suporte para a correspondência de padrão curinga. Se o *proprietário* não for especificado, as regras de visibilidade de tabela padrão do DBMS subjacente se aplicarão.  
  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , se o usuário atual possuir uma tabela com o nome especificado, as colunas dessa tabela serão retornadas. Se o *proprietário* não for especificado e o usuário atual não possuir uma tabela do *nome*especificado, esse procedimento procurará uma tabela do *nome* especificado de Propriedade do proprietário do banco de dados. Se a tabela existir, suas colunas serão retornadas.  
  
 [ @qualifier =] '*qualificador*'  
 É o nome do qualificador da tabela. o *qualificador* é **sysname**, com um padrão de NULL. Vários produtos DBMS dão suporte à nomenclatura de três partes para tabelas (*Qualifier.Owner.Name*). No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna representa o nome do banco de dados. Em alguns produtos, representa o nome do servidor do ambiente de banco de dados da tabela.  
  
 [ @col_type =] '*col_type*'  
 É o tipo da coluna. *col_type* é **Char (** 1 **)**, com um padrão de r. o tipo r retorna a coluna ou conjunto de colunas ideal que, recuperando valores da coluna ou das colunas, permite que qualquer linha na tabela especificada seja identificada exclusivamente. A coluna pode ser uma pseudocoluna especificamente projetada para esta finalidade ou a coluna ou colunas de qualquer índice exclusivo da tabela. O tipo V retorna a coluna ou as colunas da tabela especificada, se houver, que são automaticamente atualizadas pela fonte de dados quando qualquer valor na linha é atualizado por qualquer transação.  
  
 [ @scope =] '*escopo*'  
 É o escopo mínimo necessário de ROWID. o *escopo* é **Char (** 1 **)**, com um padrão de T. Scope C especifica que ROWID é válido somente quando posicionado nessa linha. O escopo T especifica que a ROWID é válida para a transação.  
  
 [ @nullable =] '*Nullable*'  
 Indica se as colunas especiais podem aceitar um valor nulo. *Nullable* é **Char (** 1 **)**, com um padrão de U. O especifica colunas especiais que não permitem valores nulos. U especifica colunas que permitem valor parcialmente nulo.  
  
 [ @ODBCVer =] '*ODBCVer*'  
 É a versão do ODBC que está sendo utilizada. *ODBCVer* é **int (** 4 **)**, com um padrão de 2. Isso indica o ODBC versão 2.0. Para obter mais informações sobre a diferença entre ODBC versão 2.0 e ODBC versão 3.0, consulte a especificação SQLSpecialColumns para ODBC versão 3.0.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhum  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|SCOPE|**smallint**|Escopo real da ID da linha. Pode ser 0, 1 ou 2. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sempre retorna 0. Esse campo sempre retorna um valor.<br /><br /> 0 = SQL_SCOPE_CURROW. A ID da linha tem a garantia de ser válida somente quando posicionada nessa linha. Uma nova seleção posterior que utilize a ID da linha talvez não retorne uma linha se a linha foi atualizada ou excluída por outra transação.<br /><br /> 1 = SQL_SCOPE_TRANSACTION. A ID da linha tem a garantia de ser válida durante a transação atual.<br /><br /> 2 = SQL_SCOPE_SESSION. A ID da linha tem a garantia de ser válida durante a sessão (dentro dos limites da transação).|  
|COLUMN_NAME|**sysname**|Nome da coluna para cada coluna da *tabela* retornada. Esse campo sempre retorna um valor.|  
|DATA_TYPE|**smallint**|Tipo de dados SQL ODBC.|  
|TYPE_NAME|**sysname**|Nome do tipo de dados dependente de fonte de dados; por exemplo, **Char**, **varchar**, **Money**ou **Text**.|  
|PRECISION|**Int**|Precisão da coluna na fonte de dados. Esse campo sempre retorna um valor.|  
|LENGTH|**Int**|Comprimento, em bytes, necessário para o tipo de dados em seu formato binário na fonte de dados, por exemplo, 10 para **Char (** 10 **)**, 4 para **Integer**e 2 para **smallint**.|  
|SCALE|**smallint**|Escala da coluna na fonte de dados. NULL é retornado para os tipos de dados para os quais a escala não é aplicável.|  
|PSEUDO_COLUMN|**smallint**|Indica se a coluna é um pseudocoluna. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sempre retorna 1:<br /><br /> 0 = SQL_PC_UNKNOWN<br /><br /> 1 = SQL_PC_NOT_PSEUDO<br /><br /> 2 = SQL_PC_PSEUDO|  
  
## <a name="remarks"></a>Comentários  
 sp_special_columns é equivalente a SQLSpecialColumns em ODBC. Os resultados retornados são ordenados por SCOPE.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão SELECT no esquema.  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir retorna informações sobre a coluna que identifica linhas de forma exclusiva na tabela `FactFinance`.  
  
```sql  
-- Uses AdventureWorks  
  
EXEC sp_special_columns_100 @table_name = 'FactFinance';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do Azure Synapse Analytics](../../relational-databases/system-stored-procedures/sql-data-warehouse-stored-procedures.md)  
  
  

