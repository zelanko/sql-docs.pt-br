---
title: sp_columns_ex (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_columns_ex
- sp_columns_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_columns_ex
ms.assetid: c12ef6df-58c6-4391-bbbf-683ea874bd81
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2aa75e2f742cbafd64f5bb8d76d7cd8dbf4028ed
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85771254"
---
# <a name="sp_columns_ex-transact-sql"></a>sp_columns_ex (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Retorna as informações da coluna, uma linha por coluna, para as tabelas especificadas do servidor vinculado. **sp_columns_ex** retornará informações de coluna somente para a coluna específica se a *coluna* for especificada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_columns_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]   
     [ , [ @column_name = ] 'column' ]   
     [ , [ @ODBCVer = ] 'ODBCVer' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @table_server = ] 'table_server'`É o nome do servidor vinculado para o qual retornar informações de coluna. *table_server* é **sysname**, sem padrão.  
  
`[ @table_name = ] 'table_name'`É o nome da tabela para a qual retornar informações de coluna. *table_name* é **sysname**, com um padrão de NULL.  
  
`[ @table_schema = ] 'table_schema'`É o nome do esquema da tabela para a qual retornar informações de coluna. *table_schema* é **sysname**, com um padrão de NULL.  
  
`[ @table_catalog = ] 'table_catalog'`É o nome do catálogo da tabela para a qual retornar informações de coluna. *TABLE_CATALOG* é **sysname**, com um padrão de NULL.  
  
`[ @column_name = ] 'column'`É o nome da coluna de banco de dados para a qual fornecer informações. a *coluna* é **sysname**, com um padrão de NULL.  
  
`[ @ODBCVer = ] 'ODBCVer'`É a versão do ODBC que está sendo usada. *ODBCVer* é **int**, com um padrão de 2. Isto indica ODBC versão 2. Os valores válidos são 2 ou 3. Para obter informações sobre as diferenças de comportamento entre as versões 2 e 3, consulte a especificação de SQLColumns ODBC.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhum  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|Nome do qualificador da tabela ou exibição. Vários produtos DBMS dão suporte à nomeação de três partes para tabelas (_qualificador_**.** _proprietário_**.** _nome_). No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta coluna representa o nome do banco de dados. Em alguns produtos, ele representa o nome do servidor do ambiente de banco de dados da tabela. Esse campo pode ser NULL.|  
|**TABLE_SCHEM**|**sysname**|Nome do proprietário da tabela ou exibição. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta coluna representa o nome do usuário de banco de dados que criou a tabela. Esse campo sempre retorna um valor.|  
|**TABLE_NAME**|**sysname**|Nome da tabela ou exibição. Esse campo sempre retorna um valor.|  
|**COLUMN_NAME**|**sysname**|Nome da coluna, para cada coluna da **table_name** retornada. Esse campo sempre retorna um valor.|  
|**DATA_TYPE**|**smallint**|Valor inteiro que corresponde aos indicadores de tipo ODBC. Se for um tipo de dados que não pode ser mapeado para um tipo ODBC, este valor será NULL. O nome do tipo de dados nativo é retornado na coluna **type_name** .|  
|**TYPE_NAME**|**varchar (** 13 **)**|Cadeia de caracteres que representa um tipo de dados. O DBMS subjacente apresenta este nome de tipo de dados.|  
|**COLUMN_SIZE**|**int**|Número de dígitos significativos. O valor de retorno para a coluna de **precisão** está na base 10.|  
|**BUFFER_LENGTH**|**int**|Tamanho da transferência dos dados.1|  
|**DECIMAL_DIGITS**|**smallint**|Número de dígitos à direita da vírgula decimal.|  
|**NUM_PREC_RADIX**|**smallint**|É a base para tipos de dados numéricos.|  
|**ANULA**|**smallint**|Especifica possibilidade de nulidade:<br /><br /> 1 = NULL é possível.<br /><br /> 0 = NOT NULL.|  
|**COMENTÁRIOS**|**varchar (** 254 **)**|Esse campo sempre retorna NULL.|  
|**COLUMN_DEF**|**varchar (** 254 **)**|Valor padrão da coluna.|  
|**SQL_DATA_TYPE**|**smallint**|Valor do tipo de dados SQL conforme exibido no campo TYPE do descritor. Essa coluna é igual à **data_type** coluna, exceto para os tipos de dados **DateTime** e SQL-92 **Interval** . Esta coluna sempre retorna um valor.|  
|**SQL_DATETIME_SUB**|**smallint**|Código de subtipo para tipos de dados **DateTime** e SQL-92 **Interval** . Para outros tipos de dados, esta coluna retorna NULL.|  
|**CHAR_OCTET_LENGTH**|**int**|Comprimento máximo em bytes de uma coluna do tipo de dados caractere ou inteiro. Para todos os outros tipos de dados, esta coluna retorna NULL.|  
|**ORDINAL_POSITION**|**int**|Posição ordinal da coluna na tabela. A primeira coluna na tabela é 1. Esta coluna sempre retorna um valor.|  
|**IS_NULLABLE**|**varchar (** 254 **)**|Possibilidade de nulidade da coluna na tabela. As regras ISO são seguidas para determinar a possibilidade de nulidade. Um DBMS em conformidade com ISO SQL não pode retornar uma cadeia de caracteres vazia.<br /><br /> YES = A coluna pode incluir NULLS.<br /><br /> NO = A coluna não pode incluir NULLS.<br /><br /> Esta coluna retorna uma cadeia de caracteres de comprimento zero se a possibilidade de nulidade for desconhecida.<br /><br /> O valor retornado para essa coluna é diferente do valor retornado para a coluna que **permite valor nulo** .|  
|**SS_DATA_TYPE**|**tinyint**|Tipo de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usado por procedimentos armazenados estendidos.|  
  
 Para obter mais informações, consulte a documentação do Microsoft ODBC.  
  
## <a name="remarks"></a>Comentários  
 **sp_columns_ex** é executado consultando o conjunto de linhas COLUMNS da interface **IDBSchemaRowset** do provedor de OLE DB correspondente ao *table_server*. Os parâmetros *table_name*, *table_schema*, *TABLE_CATALOG*e *coluna* são passados para essa interface para restringir as linhas retornadas.  
  
 **sp_columns_ex** retornará um conjunto de resultados vazio se o provedor de OLE DB do servidor vinculado especificado não oferecer suporte ao conjunto de linhas de colunas da interface **IDBSchemaRowset** .  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão SELECT no esquema.  
  
## <a name="remarks"></a>Comentários  
 **sp_columns_ex** segue os requisitos para identificadores delimitados. Para obter mais informações, consulte [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna o tipo de dados da coluna `JobTitle` da tabela `HumanResources.Employee` no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] do servidor vinculado `Seattle1`.  
  
```  
EXEC sp_columns_ex 'Seattle1',   
   'Employee',   
   'HumanResources',   
   'AdventureWorks2012',   
   'JobTitle';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_catalogs](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_foreignkeys](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_indexes](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_linkedservers](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_primarykeys](../../relational-databases/system-stored-procedures/sp-primarykeys-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_tables_ex](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_table_privileges](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
