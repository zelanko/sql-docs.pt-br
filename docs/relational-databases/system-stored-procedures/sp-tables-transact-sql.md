---
title: sp_tables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_tables
- sp_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_tables
ms.assetid: 787a2fa5-87a1-49bd-938b-6043c245f46b
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 71aaa9e52cfca8435501695a4ebf60b2a6aa6ee4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68096048"
---
# <a name="sp_tables-transact-sql"></a>sp_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma lista de objetos que podem ser consultados no ambiente atual. Isso significa qualquer tabela ou exibição, com exceção de objetos de sinônimo.  
  
> [!NOTE]  
>  Para determinar o nome do objeto base de um sinônimo, consulte a exibição do catálogo [Sys. synonyms](../../relational-databases/system-catalog-views/sys-synonyms-transact-sql.md) .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_tables [ [ @table_name = ] 'name' ]   
     [ , [ @table_owner = ] 'owner' ]   
     [ , [ @table_qualifier = ] 'qualifier' ]   
     [ , [ @table_type = ] "type" ]   
     [ , [@fUsePattern = ] 'fUsePattern'];  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @table_name = ] 'name'`É a tabela usada para retornar as informações do catálogo. o *nome* é **nvarchar (384)**, com um padrão de NULL. Há suporte para a correspondência do padrão curinga.  
  
`[ @table_owner = ] 'owner'`É o proprietário da tabela usado para retornar as informações do catálogo. *Owner* é **nvarchar (384)**, com um padrão de NULL. Há suporte para a correspondência do padrão curinga. Se o proprietário não for especificado, serão aplicadas as regras de visibilidade de tabela padrão do DBMS subjacente.  
  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se o usuário atual possuir uma tabela com o nome especificado, as colunas dessa tabela serão retornadas. Se o proprietário não estiver especificado e o usuário atual não possuir uma tabela com o nome especificado, este procedimento procurará uma tabela com o nome especificado, pertencente ao proprietário do banco de dados. Caso exista, as colunas dessa tabela serão retornadas.  
  
`[ @table_qualifier = ] 'qualifier'`É o nome do qualificador de tabela. o *qualificador* é **sysname**, com um padrão de NULL. Vários produtos DBMS dão suporte à nomeação de três partes para tabelas (_qualificador_**.** _proprietário_**.** _nome_). No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna representa o nome do banco de dados. Em alguns produtos, ele representa o nome do servidor do ambiente de banco de dados da tabela.  
  
``[ , [ @table_type = ] "'type', 'type'" ]``É uma lista de valores, separados por vírgulas, que fornece informações sobre todas as tabelas dos tipos de tabela especificados. Eles incluem **tabela**, **sistematable**e **exibição**. o *tipo* é **varchar (100)**, com um padrão de NULL.  
  
> [!NOTE]  
>  Aspas simples devem incluir cada tipo de tabela e aspas duplas devem incluir o parâmetro inteiro. Os tipos de tabela devem ser em maiúsculas. Se SET QUOTED_IDENTIFIER for ON, cada aspa simples deverá ser duplicada e o parâmetro inteiro deverá ser incluído entre aspas duplas.  
  
`[ @fUsePattern = ] 'fUsePattern'`Determina se os caracteres sublinhado (_), porcentagem (%) e colchete ([ou]) são interpretados como caracteres curinga. Os valores válidos são 0 (correspondência de padrão desativada) e 1 (correspondência de padrão ativada). *fUsePattern* é **bit**, com um padrão de 1.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhum  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**TABLE_QUALIFIER**|**sysname**|Nome do qualificador de tabela. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna representa o nome do banco de dados. Esse campo pode ser NULL.|  
|**TABLE_OWNER**|**sysname**|Nome do proprietário da tabela. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna representa o nome do usuário de banco de dados que criou a tabela. Esse campo sempre retorna um valor.|  
|**TABLE_NAME**|**sysname**|Nome da tabela. Esse campo sempre retorna um valor.|  
|**TABLE_TYPE**|**varchar (32)**|Tabela, tabela do sistema ou exibição.|  
|**COMENTÁRIOS**|**varchar (254)**|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não retorna um valor para essa coluna.|  
  
## <a name="remarks"></a>Comentários  
 Para interoperabilidade máxima, o cliente de gateway deve pressupor correspondência apenas do padrão SQL SQL-92 (os caracteres curinga % e _).  
  
 As informações de privilégio sobre o acesso de leitura ou gravação do usuário atual a uma tabela específica nem sempre são verificadas. Portanto, o acesso não está garantido. Esse conjunto de resultados inclui não apenas tabelas e exibições, mas também sinônimos e aliases de gateways para produtos DBMS que oferecem suporte a esses tipos. Se o atributo de servidor **ACCESSIBLE_TABLES** for Y no conjunto de resultados para **sp_server_info**, somente as tabelas que podem ser acessadas pelo usuário atual serão retornadas.  
  
 **sp_tables** é equivalente a **SQLTables** no ODBC. Os resultados retornados são ordenados por **TABLE_TYPE**, **TABLE_QUALIFIER**, **TABLE_OWNER**e **table_name**.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão SELECT no esquema.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-a-list-of-objects-that-can-be-queried-in-the-current-environment"></a>a. Retornando uma lista de objetos que podem ser consultados no ambiente atual  
 O exemplo a seguir retorna uma lista de objetos que podem ser consultas no ambiente atual.  
  
```  
EXEC sp_tables ;  
```  
  
### <a name="b-returning-information-about-the-tables-in-a-specified-schema"></a>B. Retornando informações sobre as tabelas em um esquema especificado  
 O exemplo a seguir retorna informações sobre as tabelas que pertencem ao esquema `Person` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_tables   
   @table_name = '%',  
   @table_owner = 'Person',  
   @table_qualifier = 'AdventureWorks2012';  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-returning-a-list-of-objects-that-can-be-queried-in-the-current-environment"></a>C. Retornando uma lista de objetos que podem ser consultados no ambiente atual  
 O exemplo a seguir retorna uma lista de objetos que podem ser consultas no ambiente atual.  
  
```  
EXEC sp_tables ;  
```  
  
### <a name="d-returning-information-about-the-tables-in-a-specified-schema"></a>D. Retornando informações sobre as tabelas em um esquema especificado  
 O exemplo a seguir retorna informações sobre as tabelas de dimensões `AdventureWorksPDW201` no banco de dados.  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_tables   
   @table_name = 'Dim%',  
   @table_owner = 'dbo',  
   @table_qualifier = 'AdventureWorksPDW2012';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sys. synonyms &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-synonyms-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

