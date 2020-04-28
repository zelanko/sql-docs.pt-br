---
title: sp_sproc_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_sproc_columns
- sp_sproc_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_sproc_columns
ms.assetid: 62c18c21-35c5-4772-be0d-ffdcc19c97ab
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6739d9bcff2639b4b4f3562624beaf2cb3a76507
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68032817"
---
# <a name="sp_sproc_columns-transact-sql"></a>sp_sproc_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna informações de coluna por um único procedimento armazenado ou função definida pelo usuário no ambiente atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_sproc_columns [[@procedure_name = ] 'name']   
    [ , [@procedure_owner = ] 'owner']   
    [ , [@procedure_qualifier = ] 'qualifier']   
    [ , [@column_name = ] 'column_name']  
    [ , [@ODBCVer = ] 'ODBCVer']  
    [ , [@fUsePattern = ] 'fUsePattern']  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @procedure_name = ] 'name'`É o nome do procedimento usado para retornar informações do catálogo. *Name* é **nvarchar (** 390 **)**, com um padrão de%, que significa todas as tabelas no banco de dados atual. Há suporte para a correspondência do padrão curinga.  
  
`[ @procedure_owner = ] 'owner'`É o nome do proprietário do procedimento. *Owner*é **nvarchar (** 384 **)**, com um padrão de NULL. Há suporte para a correspondência do padrão curinga. Se o *proprietário* não for especificado, as regras de visibilidade de procedimento padrão do DBMS subjacente se aplicarão.  
  
 Se o usuário atual possuir um procedimento com o nome especificado, serão retornadas informações sobre esse procedimento. Se o *proprietário*não for especificado e o usuário atual não possuir um procedimento com o nome especificado, **sp_sproc_columns** procurará um procedimento com o nome especificado que pertence ao proprietário do banco de dados. Se o procedimento existir, serão retornadas informações sobre suas colunas.  
  
`[ @procedure_qualifier = ] 'qualifier'`É o nome do qualificador de procedimento. o *qualificador* é **sysname**, com um padrão de NULL. Vários produtos DBMS dão suporte à nomenclatura de três partes para tabelas (*Qualifier.Owner.Name*). No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esse parâmetro representa o nome do banco de dados. Em alguns produtos, ele representa o nome do servidor do ambiente de banco de dados da tabela.  
  
`[ @column_name = ] 'column_name'`É uma única coluna e é usada quando apenas uma coluna de informações de catálogo é desejada. *column_name* é **nvarchar (** 384 **)**, com um padrão de NULL. Se *column_name* for omitido, todas as colunas serão retornadas. Há suporte para a correspondência do padrão curinga. Para obter a interoperabilidade máxima, o cliente de gateway deve pressupor correspondência apenas do padrão ISO (curingas com % e _).  
  
`[ @ODBCVer = ] 'ODBCVer'`É a versão do ODBC que está sendo usada. *ODBCVer* é **int**, com um padrão de 2, que indica a versão do ODBC 2,0. Para obter mais informações sobre a diferença entre o ODBC versão 2,0 e a versão 3,0 do ODBC, consulte a especificação ODBC **SQLProcedureColumns** para odbc versão 3,0  
  
`[ @fUsePattern = ] 'fUsePattern'`Determina se os caracteres sublinhado (_), porcentagem (%) e colchete ([]) são interpretados como caracteres curinga. Os valores válidos são 0 (correspondência de padrão desativada) e 1 (correspondência de padrão ativada). *fUsePattern* é **bit**, com um padrão de 1.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhum  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**PROCEDURE_QUALIFIER**|**sysname**|Nome do qualificador de procedimento. Esta coluna pode ser NULL.|  
|**PROCEDURE_OWNER**|**sysname**|Nome do proprietário do procedimento. Esta coluna sempre retorna um valor.|  
|**PROCEDURE_NAME**|**nvarchar (** 134 **)**|Nome do procedimento. Esta coluna sempre retorna um valor.|  
|**COLUMN_NAME**|**sysname**|Nome da coluna para cada coluna do **table_name** retornado. Esta coluna sempre retorna um valor.|  
|**COLUMN_TYPE**|**smallint**|Este campo sempre retorna um valor:<br /><br /> 0 = SQL_PARAM_TYPE_UNKNOWN<br /><br /> 1 = SQL_PARAM_TYPE_INPUT<br /><br /> 2 = SQL_PARAM_TYPE_OUTPUT<br /><br /> 3 = SQL_RESULT_COL<br /><br /> 4 = SQL_PARAM_OUTPUT<br /><br /> 5 = SQL_RETURN_VALUE|  
|**DATA_TYPE**|**smallint**|Código de inteiro para um tipo de dados de ODBC. Se este tipo de dados não puder ser mapeado para um tipo ISO, o valor será NULL. O nome do tipo de dados nativo é retornado na coluna **type_name** .|  
|**TYPE_NAME**|**sysname**|Representação em cadeia de caracteres do tipo de dados. É o nome do tipo de dados como apresentado pelo DBMS subjacente.|  
|**Preciso**|**int**|Número de dígitos significativos. O valor de retorno para a coluna de **precisão** está na base 10.|  
|**COMPRIMENTO**|**int**|Tamanho da transferência dos dados.|  
|**ESCALONÁVE**|**smallint**|Número de dígitos à direita da vírgula decimal.|  
|**RADIX**|**smallint**|É a base para tipos numéricos.|  
|**ANULA**|**smallint**|Especifica a nulidade:<br /><br /> 1 = O tipo de dados pode ser criado permitindo valores nulos.<br /><br /> 0 = Não são permitidos valores nulos.|  
|**COMENTÁRIOS**|**varchar (** 254 **)**|Descrição da coluna de procedimento. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não retorna um valor para essa coluna.|  
|**COLUMN_DEF**|**nvarchar (** 4000 **)**|Valor padrão da coluna.|  
|**SQL_DATA_TYPE**|**smallint**|Valor do tipo de dados SQL como ele aparece no campo **tipo** do descritor. Essa coluna é igual à **data_type** coluna, exceto para os tipos de dados **DateTime** e **intervalo** ISO. Esta coluna sempre retorna um valor.|  
|**SQL_DATETIME_SUB**|**smallint**|O subcódigo de **interval** ISO de **datetime**, se o valor de **SQL_DATA_TYPE** for **SQL_DATETIME** ou **SQL_INTERVAL**. Para tipos de dados diferentes de **DateTime** e o **intervalo**ISO, esse campo é nulo.|  
|**CHAR_OCTET_LENGTH**|**int**|Comprimento máximo em bytes de uma coluna de tipo de dados **Binary** ou de **caractere** . Para todos os outros tipos de dados, essa coluna retorna um valor nulo.|  
|**ORDINAL_POSITION**|**int**|Posição ordinal da coluna na tabela. A primeira coluna na tabela é 1. Esta coluna sempre retorna um valor.|  
|**IS_NULLABLE**|**varchar (254)**|Possibilidade de nulidade da coluna na tabela. As regras ISO são seguidas para determinar a possibilidade de nulidade. Um DBMS com conformidade de ISO não pode retornar uma cadeia de caracteres vazia.<br /><br /> Exibe YES, se a coluna puder incluir NULLS, e NO, se a coluna não puder incluir NULLS.<br /><br /> Esta coluna retorna uma cadeia de caracteres de comprimento zero se a possibilidade de nulidade for desconhecida.<br /><br /> O valor retornado para esta coluna é diferente do valor retornado para a coluna NULLABLE.|  
|**SS_DATA_TYPE**|**tinyint**|Tipo de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usados por procedimentos armazenados estendidos. Para obter mais informações, veja [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).|  
  
## <a name="remarks"></a>Comentários  
 **sp_sproc_columns** é equivalente a **SQLProcedureColumns** no ODBC. Os resultados retornados são ordenados por **PROCEDURE_QUALIFIER**, **PROCEDURE_OWNER**, **procedure_name**e a ordem em que os parâmetros aparecem na definição do procedimento.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão SELECT no esquema.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
