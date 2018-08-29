---
title: sp_sproc_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_sproc_columns
- sp_sproc_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_sproc_columns
ms.assetid: 62c18c21-35c5-4772-be0d-ffdcc19c97ab
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8923e4f38ec6ef69de9817ebc3940da07a1518db
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43077166"
---
# <a name="spsproccolumns-transact-sql"></a>sp_sproc_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna informações de coluna por um único procedimento armazenado ou função definida pelo usuário no ambiente atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@procedure_name =** ] **'***nome***'**  
 É o nome do procedimento usado para retornar as informações do catálogo. *nome da* está **nvarchar (** 390 **)**, com um padrão de %, que significa que todas as tabelas no banco de dados atual. Há suporte para a correspondência do padrão curinga.  
  
 [  **@procedure_owner =**] **'***proprietário***'**  
 É o nome do proprietário do procedimento. *proprietário*está **nvarchar (** 384 **)**, com um padrão NULL. Há suporte para a correspondência do padrão curinga. Se *proprietário* não é especificado, serão aplicadas as regras de visibilidade de procedimento padrão do DBMS subjacente.  
  
 Se o usuário atual possuir um procedimento com o nome especificado, serão retornadas informações sobre esse procedimento. Se *proprietário*não for especificado e o usuário atual não possuir um procedimento com o nome especificado, **sp_sproc_columns** procurará um procedimento com o nome especificado que é pertencente ao proprietário do banco de dados. Se o procedimento existir, serão retornadas informações sobre suas colunas.  
  
 [  **@procedure_qualifier =**] **'***qualificador***'**  
 É o nome do qualificador do procedimento. *qualificador* está **sysname**, com um padrão NULL. Vários produtos DBMS dão suporte à nomenclatura de três partes para tabelas (*qualificador*). No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esse parâmetro representa o nome do banco de dados. Em alguns produtos, ele representa o nome do servidor do ambiente de banco de dados da tabela.  
  
 [  **@column_name =**] **'***column_name***'**  
 É uma única coluna e é usada quando somente uma coluna de informações de catálogo é desejada. *column_name* está **nvarchar (** 384 **)**, com um padrão NULL. Se *column_name* é omitido, todas as colunas são retornadas. Há suporte para a correspondência do padrão curinga. Para obter a interoperabilidade máxima, o cliente de gateway deve pressupor correspondência apenas do padrão ISO (curingas com % e _).  
  
 [  **@ODBCVer =**] **'***ODBCVer***'**  
 É a versão do ODBC que está sendo usada. *ODBCVer* está **int**, com um padrão de 2, que indica ODBC versão 2.0. Para obter mais informações sobre a diferença entre ODBC versão 2.0 e ODBC versão 3.0, consulte a **SQLProcedureColumns** especificação para ODBC versão 3.0  
  
 [  **@fUsePattern =**] **'***fUsePattern***'**  
 Determina se os caracteres sublinhado (_), porcentagem (%) e colchetes ([ ]) são interpretados como curingas. Os valores válidos são 0 (correspondência de padrão desativada) e 1 (correspondência de padrão ativada). *fUsePattern* está **bit**, com um padrão de 1.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 None  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**PROCEDURE_QUALIFIER**|**sysname**|Nome do qualificador de procedimento. Esta coluna pode ser NULL.|  
|**PROCEDURE_OWNER**|**sysname**|Nome do proprietário do procedimento. Esta coluna sempre retorna um valor.|  
|**PROCEDURE_NAME**|**nvarchar (** 134 **)**|Nome do procedimento. Esta coluna sempre retorna um valor.|  
|**COLUMN_NAME**|**sysname**|Nome da coluna para cada coluna do **TABLE_NAME** retornado. Esta coluna sempre retorna um valor.|  
|**COLUMN_TYPE**|**smallint**|Este campo sempre retorna um valor:<br /><br /> 0 = SQL_PARAM_TYPE_UNKNOWN<br /><br /> 1 = SQL_PARAM_TYPE_INPUT<br /><br /> 2 = SQL_PARAM_TYPE_OUTPUT<br /><br /> 3 = SQL_RESULT_COL<br /><br /> 4 = SQL_PARAM_OUTPUT<br /><br /> 5 = SQL_RETURN_VALUE|  
|**DATA_TYPE**|**smallint**|Código de inteiro para um tipo de dados de ODBC. Se este tipo de dados não puder ser mapeado para um tipo ISO, o valor será NULL. O nome do tipo de dados nativo é retornado na **TYPE_NAME** coluna.|  
|**TYPE_NAME**|**sysname**|Representação em cadeia de caracteres do tipo de dados. É o nome do tipo de dados como apresentado pelo DBMS subjacente.|  
|**PRECISION**|**int**|Número de dígitos significativos. O valor retornado para o **precisão** coluna está na base 10.|  
|**LENGTH**|**int**|Tamanho da transferência dos dados.|  
|**ESCALA**|**smallint**|Número de dígitos à direita da vírgula decimal.|  
|**RADIX**|**smallint**|É a base para tipos numéricos.|  
|**PERMITE VALOR NULO**|**smallint**|Especifica a condição de nulidade:<br /><br /> 1 = O tipo de dados pode ser criado permitindo valores nulos.<br /><br /> 0 = Não são permitidos valores nulos.|  
|**COMENTÁRIOS**|**varchar (** 254 **)**|Descrição da coluna de procedimento. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não retorna um valor para essa coluna.|  
|**COLUMN_DEF**|**nvarchar (** 4000 **)**|Valor padrão da coluna.|  
|**SQL_DATA_TYPE**|**smallint**|Valor do tipo de dados SQL como ele aparece na **tipo** campo do descritor. Esta coluna é igual a **DATA_TYPE** coluna, exceto para o **datetime** e ISO **intervalo** tipos de dados. Esta coluna sempre retorna um valor.|  
|**SQL_DATETIME_SUB**|**smallint**|O **datetime** ISO **intervalo** subcódigo se o valor de **SQL_DATA_TYPE** é **SQL_DATETIME** ou **SQL_INTERVAL**. Para tipos de dados diferente de **datetime** e ISO **intervalo**, este campo é NULL.|  
|**CHAR_OCTET_LENGTH**|**int**|Comprimento máximo em bytes de um **caractere** ou **binário** coluna de tipo de dados. Para todos os outros tipos de dados, esta coluna retorna um valor nulo.|  
|**ORDINAL_POSITION**|**int**|Posição ordinal da coluna na tabela. A primeira coluna na tabela é 1. Esta coluna sempre retorna um valor.|  
|**IS_NULLABLE**|**varchar(254)**|Possibilidade de nulidade da coluna na tabela. As regras ISO são seguidas para determinar a possibilidade de nulidade. Um DBMS com conformidade de ISO não pode retornar uma cadeia de caracteres vazia.<br /><br /> Exibe YES, se a coluna puder incluir NULLS, e NO, se a coluna não puder incluir NULLS.<br /><br /> Esta coluna retorna uma cadeia de caracteres de comprimento zero se a possibilidade de nulidade for desconhecida.<br /><br /> O valor retornado para esta coluna é diferente do valor retornado para a coluna NULLABLE.|  
|**SS_DATA_TYPE**|**tinyint**|Tipo de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usados por procedimentos armazenados estendidos. Para obter mais informações, veja [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).|  
  
## <a name="remarks"></a>Remarks  
 **sp_sproc_columns** é equivalente a **SQLProcedureColumns** no ODBC. Os resultados retornados são ordenados por **PROCEDURE_QUALIFIER**, **PROCEDURE_OWNER**, **PROCEDURE_NAME**e a ordem em que os parâmetros aparecem no procedimento definição.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão SELECT no esquema.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
