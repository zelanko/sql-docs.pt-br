---
description: sp_columns (Transact-SQL)
title: sp_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/17/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_columns_TSQL
- sp_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sp_columns
ms.assetid: 2dec79cf-2baf-4c0f-8cbb-afb1a8654e1e
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0c7a46f76385a724f1aa8622ac85301cdc7e12b6
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "92006511"
---
# <a name="sp_columns-transact-sql"></a>sp_columns (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna as informações de colunas dos objetos especificados que podem ser consultados no ambiente atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql  
-- Syntax for SQL Server, Azure SQL Database, Azure Synapse Analytics, Parallel Data Warehouse  
  
sp_columns [ @table_name = ] object  
     [ , [ @table_owner = ] owner ]   
     [ , [ @table_qualifier = ] qualifier ]   
     [ , [ @column_name = ] column ]   
     [ , [ @ODBCVer = ] ODBCVer ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ \@table_name = ] object` É o nome do objeto usado para retornar as informações do catálogo. o *objeto* pode ser uma tabela, exibição ou outro objeto que tenha colunas como funções com valor de tabela. o *objeto* é **nvarchar (384)**, sem padrão. Há suporte para a correspondência do padrão curinga.  
  
`[ \@table_owner = ] owner` É o proprietário do objeto do objeto usado para retornar as informações do catálogo. *Owner* é **nvarchar (384)**, com um padrão de NULL. Há suporte para a correspondência do padrão curinga. Se o *proprietário* não for especificado, as regras de visibilidade de objeto padrão do DBMS subjacente se aplicarão.  
  
 Se o usuário atual possuir um objeto com o nome especificado, as colunas desse objeto serão retornadas. Se o *proprietário* não for especificado e o usuário atual não possuir um objeto com o *objeto*especificado, **sp_columns** procurará um objeto com o *objeto* especificado de Propriedade do proprietário do banco de dados. Se existir, as colunas desse objeto serão retornadas.  
  
`[ \@table_qualifier = ] qualifier` É o nome do qualificador de objeto. o *qualificador* é **sysname**, com um padrão de NULL. Vários produtos DBMS dão suporte à nomeação de três partes para objetos (_qualificador_**.** _proprietário_**.** _nome_). No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna representa o nome do banco de dados. Em alguns produtos, ela representa o nome do servidor do ambiente de banco de dados do objeto.  
  
`[ \@column_name = ] column` É uma única coluna e é usada quando é desejada apenas uma coluna de informações de catálogo. a *coluna* é **nvarchar (384)**, com um padrão de NULL. Se a *coluna* não for especificada, todas as colunas serão retornadas. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , *coluna* representa o nome da coluna, conforme listado na tabela **syscolumns** . Há suporte para a correspondência do padrão curinga. Para interoperabilidade máxima, o cliente de gateway deve pressupor correspondência apenas do padrão SQL-92 (os caracteres curinga % e _).  
  
`[ \@ODBCVer = ] ODBCVer` É a versão do ODBC que está sendo usada. *ODBCVer* é **int**, com um padrão de 2. Isto indica ODBC versão 2. Os valores válidos são 2 ou 3. Para as diferenças de comportamento entre as versões 2 e 3, consulte a especificação ODBC **SQLColumns** .  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhum  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 O procedimento armazenado do catálogo **sp_columns** é equivalente a **SQLColumns** no ODBC. Os resultados retornados são ordenados por **TABLE_QUALIFIER**, **TABLE_OWNER**e **table_name**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**TABLE_QUALIFIER**|**sysname**|Nome do qualificador do objeto. Esse campo pode ser NULL.|  
|**TABLE_OWNER**|**sysname**|Nome do proprietário do objeto. Esse campo sempre retorna um valor.|  
|**TABLE_NAME**|**sysname**|Nome do objeto. Esse campo sempre retorna um valor.|  
|**COLUMN_NAME**|**sysname**|Nome da coluna, para cada coluna da **table_name** retornada. Esse campo sempre retorna um valor.|  
|**DATA_TYPE**|**smallint**|Código inteiro para o tipo de dados do ODBC. Se este for um tipo de dados que não pode ser mapeado para um tipo do ODBC, ele será NULL. O nome do tipo de dados nativo é retornado na coluna **type_name** .|  
|**TYPE_NAME**|**sysname**|Cadeia de caracteres que representa um tipo de dados. O DBMS subjacente apresenta este nome de tipo de dados.|  
|**PRECISION**|**int**|Número de dígitos significativos. O valor de retorno para a coluna de **precisão** está na base 10.|  
|**COMPRIMENTO**|**int**|Tamanho da transferência dos dados. <sup>1</sup>|  
|**ESCALONÁVE**|**smallint**|Número de dígitos à direita da vírgula decimal.|  
|**RADIX**|**smallint**|Base para tipos de dados numéricos.|  
|**ANULA**|**smallint**|Especifica possibilidade de nulidade:<br /><br /> 1 = NULL é possível.<br /><br /> 0 = NOT NULL.|  
|**COMENTÁRIOS**|**varchar (254)**|Esse campo sempre retorna NULL.|  
|**COLUMN_DEF**|**nvarchar(4000)**|Valor padrão da coluna.|  
|**SQL_DATA_TYPE**|**smallint**|Valor do tipo de dados SQL conforme exibido no campo TYPE do descritor. Essa coluna é igual à **data_type** coluna, exceto para os tipos de dados **DateTime** e SQL-92 **Interval** . Esta coluna sempre retorna um valor.|  
|**SQL_DATETIME_SUB**|**smallint**|Código de subtipo para tipos de dados **DateTime** e SQL-92 **Interval** . Para outros tipos de dados, esta coluna retorna NULL.|  
|**CHAR_OCTET_LENGTH**|**int**|Comprimento máximo em bytes de uma coluna do tipo de dados caractere ou inteiro. Para todos os outros tipos de dados, esta coluna retorna NULL.|  
|**ORDINAL_POSITION**|**int**|Posição ordinal da coluna no objeto. A primeira coluna no objeto é 1. Esta coluna sempre retorna um valor.|  
|**IS_NULLABLE**|**varchar (254)**|A nulidade da coluna no objeto. As regras ISO são seguidas para determinar a possibilidade de nulidade. Um DBMS em conformidade com ISO SQL não pode retornar uma cadeia de caracteres vazia.<br /><br /> YES = A coluna pode incluir NULLS.<br /><br /> NO = A coluna não pode incluir NULLS.<br /><br /> Esta coluna retorna uma cadeia de caracteres de comprimento zero se a possibilidade de nulidade for desconhecida.<br /><br /> O valor retornado para essa coluna é diferente do valor retornado para a coluna que **permite valor nulo** .|  
|**SS_DATA_TYPE**|**tinyint**|Tipo de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usados por procedimentos armazenados estendidos. Para obter mais informações, veja [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).|  
  
 <sup>1</sup> para obter mais informações, consulte a documentação ODBC da Microsoft.  
  
## <a name="permissions"></a>Permissões  
 Requer permissões SELECT e VIEW DEFINITION no esquema.  
  
## <a name="remarks"></a>Comentários  
 **sp_columns** segue os requisitos para identificadores delimitados. Para obter mais informações, consulte [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações de coluna para uma tabela especificada.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_columns @table_name = N'Department',  
   @table_owner = N'HumanResources';  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir retorna informações de coluna para uma tabela especificada.  
  
```sql  
-- Uses AdventureWorks  
  
EXEC sp_columns @table_name = N'DimEmployee',  
   @table_owner = N'dbo';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_tables ](../../relational-databases/system-stored-procedures/sp-tables-transact-sql.md)   
 [Procedimentos armazenados de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  


