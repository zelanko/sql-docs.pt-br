---
description: sp_pkeys (Transact-SQL)
title: sp_pkeys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_pkeys
- sp_pkeys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_pkeys
ms.assetid: e614c75d-847b-4726-8f6f-cd18de688eda
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ea021b39d01af931a989c55233a7f1cd8fa2cb82
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "92004794"
---
# <a name="sp_pkeys-transact-sql"></a>sp_pkeys (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna informações de chave primária para uma única tabela no ambiente atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql  
-- Syntax for SQL Server, Azure SQL Database, Azure Synapse Analytics, Parallel Data Warehouse  
  
sp_pkeys [ @table_name = ] 'name'       
    [ , [ @table_owner = ] 'owner' ]   
    [ , [ @table_qualifier = ] 'qualifier' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @table_name =] '*nome*'  
 É a tabela para a qual retornar informações. o *nome* é **sysname**, sem padrão. Não há suporte para a correspondência de padrão curinga.  
  
 [ @table_owner =] '*proprietário*'  
 Especifica o proprietário da tabela especificada. *Owner* é **sysname**, com um padrão de NULL. Não há suporte para a correspondência de padrão curinga. Se o *proprietário* não for especificado, as regras de visibilidade de tabela padrão do DBMS subjacente se aplicarão.  
  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , se o usuário atual possuir uma tabela com o nome especificado, as colunas dessa tabela serão retornadas. Se o *proprietário* não for especificado e o usuário atual não possuir uma tabela com o *nome*especificado, esse procedimento procurará uma tabela com o *nome* especificado de Propriedade do proprietário do banco de dados. Caso exista, as colunas dessa tabela serão retornadas.  
  
 [ @table_qualifier =] '*qualificador*'  
 É o qualificador da tabela. o *qualificador* é **sysname**, com um padrão de NULL. Vários produtos DBMS dão suporte à nomeação de três partes para tabelas (_qualificador_**.** _proprietário_**.** _nome_). No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna representa o nome do banco de dados. Em alguns produtos, representa o nome do servidor do ambiente de banco de dados da tabela.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhum  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|TABLE_QUALIFIER|**sysname**|Nome do qualificador da tabela. Esse campo pode ser NULL.|  
|TABLE_OWNER|**sysname**|Nome do proprietário da tabela. Esse campo sempre retorna um valor.|  
|TABLE_NAME|**sysname**|Nome da tabela. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , essa coluna representa o nome da tabela, conforme listado na tabela sysobjects. Esse campo sempre retorna um valor.|  
|COLUMN_NAME|**sysname**|Nome da coluna, para cada coluna de TABLE_NAME retornado. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , essa coluna representa o nome da coluna, conforme listado na tabela sys. Columns. Esse campo sempre retorna um valor.|  
|KEY_SEQ|**smallint**|Número de sequência da coluna em uma chave primária de várias colunas.|  
|PK_NAME|**sysname**|Identificador da chave primária. Retorna NULL se não for aplicável à fonte de dados.|  
  
## <a name="remarks"></a>Comentários  
 sp_pkeys retorna informações sobre colunas explicitamente definidas com uma restrição PRIMARY KEY. Como nem todos os sistemas oferecem suporte a chaves primárias explicitamente nomeadas, o implementador de gateway determina o que constitui uma chave primária. Observe que o termo chave primária refere-se a uma chave primária lógica para uma tabela. Espera-se que cada chave listada como chave primária lógica tenha um índice exclusivo definido. Esse índice exclusivo também é retornado em sp_statistics.  
  
 O procedimento armazenado sp_fkeys é equivalente a SQLForeignKeys em ODBC. Os resultados retornados são ordenados porTABLE_QUALIFIER, TABLE_OWNER, TABLE_NAME e KEY_SEQ.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão SELECT no esquema.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir recupera a chaves primária para a tabela `HumanResources.Department` no banco de dados `AdventureWorks2012`.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_pkeys @table_name = N'Department'  
    ,@table_owner = N'HumanResources';  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir recupera a chaves primária para a tabela `DimAccount` no banco de dados `AdventureWorksPDW2012`. Ele retorna zero linhas indicando que a tabela não tem uma chave primária.  
  
```sql  
-- Uses AdventureWorks  
  
EXEC sp_pkeys @table_name = N'DimAccount';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

