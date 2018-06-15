---
title: sp_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/17/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_columns_TSQL
- sp_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sp_columns
ms.assetid: 2dec79cf-2baf-4c0f-8cbb-afb1a8654e1e
caps.latest.revision: 45
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 784811775a3364544e67d6591de203b091ab5402
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33240466"
---
# <a name="spcolumns-transact-sql"></a>sp_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna as informações de colunas dos objetos especificados que podem ser consultados no ambiente atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_columns [ @table_name = ] object  
     [ , [ @table_owner = ] owner ]   
     [ , [ @table_qualifier = ] qualifier ]   
     [ , [ @column_name = ] column ]   
     [ , [ @ODBCVer = ] ODBCVer ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@table_name=**] *objeto*  
 É o nome do objeto usado para retornar informações do catálogo. *objeto* pode ser uma tabela, exibição ou outro objeto que tem colunas como funções com valor de tabela. *objeto* é **nvarchar(384)**, sem padrão. Há suporte para a correspondência do padrão curinga.  
  
 [  **@table_owner* =**] *proprietário*  
 É o proprietário do objeto usado para retornar informações do catálogo. *proprietário* é **nvarchar(384)**, com um padrão NULL. Há suporte para a correspondência do padrão curinga. Se *proprietário* não for especificado, serão aplicadas as regras de visibilidade de objeto padrão do DBMS subjacente.  
  
 Se o usuário atual possuir um objeto com o nome especificado, as colunas desse objeto serão retornadas. Se *proprietário* não for especificado e o usuário atual não possuir um objeto com especificado *objeto*, **sp_columns** procura um objeto com especificado  *objeto* pertencente ao proprietário do banco de dados. Se existir, as colunas desse objeto serão retornadas.  
  
 [  **@table_qualifier* =**] *qualificador*  
 É o nome do qualificador do objeto. *qualificador* é **sysname**, com um padrão NULL. Vários produtos DBMS dão suporte à nomenclatura de três partes para objetos (*qualificador ***.*** proprietário ***.*** nome*). No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna representa o nome do banco de dados. Em alguns produtos, ela representa o nome do servidor do ambiente de banco de dados do objeto.  
  
 [  **@column_name=**] *coluna*  
 É uma única coluna, usada quando apenas uma coluna de informações de catálogo é desejada. *coluna* é **nvarchar(384)**, com um padrão NULL. Se *coluna* não é especificado, todas as colunas são retornadas. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], *coluna* representa o nome da coluna conforme listado no **syscolumns** tabela. Há suporte para a correspondência do padrão curinga. Para interoperabilidade máxima, o cliente de gateway deve pressupor correspondência apenas do padrão SQL-92 (os caracteres curinga % e _).  
  
 [  **@ODBCVer=**] *ODBCVer*  
 É a versão do ODBC está sendo usada. *ODBCVer* é **int**, com um padrão de 2. Isto indica ODBC versão 2. Os valores válidos são 2 ou 3. Para as diferenças de comportamento entre as versões 2 e 3, consulte a **SQLColumns** especificação.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhuma  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 O **sp_columns** procedimento armazenado de catálogo é equivalente a **SQLColumns** no ODBC. Os resultados retornados são ordenados por **TABLE_QUALIFIER**, **TABLE_OWNER**, e **TABLE_NAME**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_QUALIFIER**|**sysname**|Nome do qualificador do objeto. Esse campo pode ser NULL.|  
|**TABLE_OWNER**|**sysname**|Nome do proprietário do objeto. Esse campo sempre retorna um valor.|  
|**TABLE_NAME**|**sysname**|Nome do objeto. Esse campo sempre retorna um valor.|  
|**COLUMN_NAME**|**sysname**|Nome da coluna para cada coluna do **TABLE_NAME** retornado. Esse campo sempre retorna um valor.|  
|**DATA_TYPE**|**smallint**|Código inteiro para o tipo de dados do ODBC. Se este for um tipo de dados que não pode ser mapeado para um tipo do ODBC, ele será NULL. O nome do tipo de dados nativo é retornado no **TYPE_NAME** coluna.|  
|**TYPE_NAME**|**sysname**|Cadeia de caracteres que representa um tipo de dados. O DBMS subjacente apresenta este nome de tipo de dados.|  
|**PRECISION**|**Int**|Número de dígitos significativos. O valor de retorno para o **precisão** coluna está na base 10.|  
|**LENGTH**|**Int**|Tamanho da transferência dos dados. <sup>1</sup>|  
|**ESCALA**|**smallint**|Número de dígitos à direita da vírgula decimal.|  
|**BASE**|**smallint**|Base para tipos de dados numéricos.|  
|**PERMITE VALOR NULO**|**smallint**|Especifica possibilidade de nulidade:<br /><br /> 1 = NULL é possível.<br /><br /> 0 = NOT NULL.|  
|**COMENTÁRIOS**|**varchar(254)**|Esse campo sempre retorna NULL.|  
|**COLUMN_DEF**|**nvarchar(4000)**|Valor padrão da coluna.|  
|**SQL_DATA_TYPE**|**smallint**|Valor do tipo de dados SQL conforme exibido no campo TYPE do descritor. Essa coluna é o mesmo que o **DATA_TYPE** coluna, exceto para o **datetime** e SQL-92 **intervalo** tipos de dados. Esta coluna sempre retorna um valor.|  
|**SQL_DATETIME_SUB**|**smallint**|Código de subtipo para **datetime** e SQL-92 **intervalo** tipos de dados. Para outros tipos de dados, esta coluna retorna NULL.|  
|**CHAR_OCTET_LENGTH**|**Int**|Comprimento máximo em bytes de uma coluna do tipo de dados caractere ou inteiro. Para todos os outros tipos de dados, esta coluna retorna NULL.|  
|**ORDINAL_POSITION**|**Int**|Posição ordinal da coluna no objeto. A primeira coluna no objeto é 1. Esta coluna sempre retorna um valor.|  
|**IS_NULLABLE**|**varchar(254)**|A nulidade da coluna no objeto. As regras ISO são seguidas para determinar a possibilidade de nulidade. Um DBMS em conformidade com ISO SQL não pode retornar uma cadeia de caracteres vazia.<br /><br /> YES = A coluna pode incluir NULLS.<br /><br /> NO = A coluna não pode incluir NULLS.<br /><br /> Esta coluna retorna uma cadeia de caracteres de comprimento zero se a possibilidade de nulidade for desconhecida.<br /><br /> O valor retornado para essa coluna é diferente do valor retornado para o **NULLABLE** coluna.|  
|**SS_DATA_TYPE**|**tinyint**|Tipo de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usados por procedimentos armazenados estendidos. Para obter mais informações, veja [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).|  
  
 <sup>1</sup> para obter mais informações, consulte a documentação do Microsoft ODBC.  
  
## <a name="permissions"></a>Permissões  
 Requer permissões SELECT e VIEW DEFINITION no esquema.  
  
## <a name="remarks"></a>Remarks  
 **sp_columns** segue os requisitos para identificadores delimitados. Para obter mais informações, consulte [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações de coluna para uma tabela especificada.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_columns @table_name = N'Department',  
   @table_owner = N'HumanResources';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir retorna informações de coluna para uma tabela especificada.  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_columns @table_name = N'DimEmployee',  
   @table_owner = N'dbo';  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_tables &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tables-transact-sql.md)   
 [Procedimentos armazenados de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  


