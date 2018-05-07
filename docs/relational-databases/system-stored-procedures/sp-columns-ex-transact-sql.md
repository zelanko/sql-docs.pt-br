---
title: sp_columns_ex (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_columns_ex
- sp_columns_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_columns_ex
ms.assetid: c12ef6df-58c6-4391-bbbf-683ea874bd81
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: a7f075de05288823c1ed290527de4005b1160c20
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="spcolumnsex-transact-sql"></a>sp_columns_ex (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna as informações da coluna, uma linha por coluna, para as tabelas especificadas do servidor vinculado. **sp_columns_ex** retorna informações de coluna para somente a coluna específica se *coluna* for especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@table_server =** ] **'***table_server***'**  
 É o nome do servidor vinculado para o qual as informações de coluna devem ser retornadas. *table_server* é **sysname**, sem padrão.  
  
 [  **@table_name =** ] **'***table_name***'**  
 É o nome da tabela para a qual as informações de coluna devem ser retornadas. *table_name* é **sysname**, com um padrão NULL.  
  
 [  **@table_schema =** ] **'***table_schema***'**  
 É o nome do esquema da tabela para o qual as informações de coluna devem ser retornadas. *table_schema* é **sysname**, com um padrão NULL.  
  
 [  **@table_catalog =** ] **'***table_catalog***'**  
 É o nome do catálogo da tabela para o qual as informações de coluna devem ser retornadas. *table_catalog* é **sysname**, com um padrão NULL.  
  
 [  **@column_name =** ] **'***coluna***'**  
 É o nome da coluna do banco de dados para a qual fornecer informações. *coluna* é **sysname**, com um padrão NULL.  
  
 [  **@ODBCVer =** ] **'***ODBCVer***'**  
 É a versão do ODBC está sendo usada. *ODBCVer* é **int**, com um padrão de 2. Isto indica ODBC versão 2. Os valores válidos são 2 ou 3. Para obter informações sobre as diferenças de comportamento entre as versões 2 e 3, consulte a especificação de SQLColumns ODBC.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhuma  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|Nome do qualificador da tabela ou exibição. Vários produtos DBMS dão suporte à nomenclatura de três partes para tabelas (*qualificador ***.*** proprietário ***.*** nome*). No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta coluna representa o nome do banco de dados. Em alguns produtos, representa o nome do servidor do ambiente de banco de dados da tabela. Esse campo pode ser NULL.|  
|**TABLE_SCHEM**|**sysname**|Nome do proprietário da tabela ou exibição. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta coluna representa o nome do usuário de banco de dados que criou a tabela. Esse campo sempre retorna um valor.|  
|**TABLE_NAME**|**sysname**|Nome da tabela ou exibição. Esse campo sempre retorna um valor.|  
|**COLUMN_NAME**|**sysname**|Nome da coluna para cada coluna do **TABLE_NAME** retornado. Esse campo sempre retorna um valor.|  
|**DATA_TYPE**|**smallint**|Valor inteiro que corresponde aos indicadores de tipo ODBC. Se for um tipo de dados que não pode ser mapeado para um tipo ODBC, este valor será NULL. O nome do tipo de dados nativo é retornado no **TYPE_NAME** coluna.|  
|**TYPE_NAME**|**varchar (** 13 **)**|Cadeia de caracteres que representa um tipo de dados. O DBMS subjacente apresenta este nome de tipo de dados.|  
|**COLUMN_SIZE**|**Int**|Número de dígitos significativos. O valor de retorno para o **precisão** coluna está na base 10.|  
|**BUFFER_LENGTH**|**Int**|Tamanho da transferência dos dados.1|  
|**DECIMAL_DIGITS**|**smallint**|Número de dígitos à direita da vírgula decimal.|  
|**NUM_PREC_RADIX**|**smallint**|É a base para tipos de dados numéricos.|  
|**PERMITE VALOR NULO**|**smallint**|Especifica possibilidade de nulidade:<br /><br /> 1 = NULL é possível.<br /><br /> 0 = NOT NULL.|  
|**COMENTÁRIOS**|**varchar (** 254 **)**|Esse campo sempre retorna NULL.|  
|**COLUMN_DEF**|**varchar (** 254 **)**|Valor padrão da coluna.|  
|**SQL_DATA_TYPE**|**smallint**|Valor do tipo de dados SQL conforme exibido no campo TYPE do descritor. Essa coluna é o mesmo que o **DATA_TYPE** coluna, exceto para o **datetime** e SQL-92 **intervalo** tipos de dados. Esta coluna sempre retorna um valor.|  
|**SQL_DATETIME_SUB**|**smallint**|Código de subtipo para **datetime** e SQL-92 **intervalo** tipos de dados. Para outros tipos de dados, esta coluna retorna NULL.|  
|**CHAR_OCTET_LENGTH**|**Int**|Comprimento máximo em bytes de uma coluna do tipo de dados caractere ou inteiro. Para todos os outros tipos de dados, esta coluna retorna NULL.|  
|**ORDINAL_POSITION**|**Int**|Posição ordinal da coluna na tabela. A primeira coluna na tabela é 1. Esta coluna sempre retorna um valor.|  
|**IS_NULLABLE**|**varchar (** 254 **)**|Possibilidade de nulidade da coluna na tabela. As regras ISO são seguidas para determinar a possibilidade de nulidade. Um DBMS em conformidade com ISO SQL não pode retornar uma cadeia de caracteres vazia.<br /><br /> YES = A coluna pode incluir NULLS.<br /><br /> NO = A coluna não pode incluir NULLS.<br /><br /> Esta coluna retorna uma cadeia de caracteres de comprimento zero se a possibilidade de nulidade for desconhecida.<br /><br /> O valor retornado para essa coluna é diferente do valor retornado para o **NULLABLE** coluna.|  
|**SS_DATA_TYPE**|**tinyint**|Tipo de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usado por procedimentos armazenados estendidos.|  
  
 Para obter mais informações, consulte a documentação do Microsoft ODBC.  
  
## <a name="remarks"></a>Remarks  
 **sp_columns_ex** é executado consultando o conjunto de linhas de colunas de **IDBSchemaRowset** interface do provedor OLE DB correspondente a *table_server*. O *table_name*, *table_schema*, *table_catalog*, e *coluna* parâmetros são passados para essa interface para restringir as linhas retornado.  
  
 **sp_columns_ex** retorna um resultado vazio definido se o provedor OLE DB do servidor vinculado especificado não suporta o conjunto de linhas de colunas de **IDBSchemaRowset** interface.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão SELECT no esquema.  
  
## <a name="remarks"></a>Remarks  
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
  
## <a name="see-also"></a>Consulte também  
 [sp_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_foreignkeys &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [sp_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_primarykeys &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-primarykeys-transact-sql.md)   
 [sp_tables_ex &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [sp_table_privileges &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
