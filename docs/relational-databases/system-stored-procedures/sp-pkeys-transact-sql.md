---
title: sp_pkeys (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_pkeys
- sp_pkeys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_pkeys
ms.assetid: e614c75d-847b-4726-8f6f-cd18de688eda
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bbf8a10a560bcf058f30281ceebe34a47689e3b1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sppkeys-transact-sql"></a>sp_pkeys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna informações de chave primária para uma única tabela no ambiente atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_pkeys [ @table_name = ] 'name'       
    [ , [ @table_owner = ] 'owner' ]   
    [ , [ @table_qualifier = ] 'qualifier' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @table_name=] '*nome*'  
 É a tabela para a qual retornar informações. *nome* é **sysname**, sem padrão. Não há suporte para a correspondência de padrão curinga.  
  
 [ @table_owner=] '*proprietário*'  
 Especifica o proprietário da tabela especificada. *proprietário* é **sysname**, com um padrão NULL. Não há suporte para a correspondência de padrão curinga. Se *proprietário* não for especificado, serão aplicadas as regras de visibilidade de tabela padrão do DBMS subjacente.  
  
 Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se o usuário atual possuir uma tabela com o nome especificado, as colunas dessa tabela serão retornadas. Se o *proprietário* não for especificado e o usuário atual não possuir uma tabela com especificado *nome*, esse procedimento procurará uma tabela com especificado *nome* pertencentes a proprietário do banco de dados. Caso exista, as colunas dessa tabela serão retornadas.  
  
 [ @table_qualifier=] '*qualificador*'  
 É o qualificador da tabela. *qualificador* é **sysname**, com um padrão NULL. Vários produtos DBMS dão suporte à nomenclatura de três partes para tabelas (*qualificador***.** *proprietário***.** *nome*). No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna representa o nome do banco de dados. Em alguns produtos, representa o nome do servidor do ambiente de banco de dados da tabela.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhuma  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|TABLE_QUALIFIER|**sysname**|Nome do qualificador da tabela. Esse campo pode ser NULL.|  
|TABLE_OWNER|**sysname**|Nome do proprietário da tabela. Esse campo sempre retorna um valor.|  
|TABLE_NAME|**sysname**|Nome da tabela. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta coluna representa o nome da tabela como listado na tabela sysobjects. Esse campo sempre retorna um valor.|  
|COLUMN_NAME|**sysname**|Nome da coluna, para cada coluna do TABLE_NAME retornado. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta coluna representa o nome da coluna conforme listado na tabela sys. Columns. Esse campo sempre retorna um valor.|  
|KEY_SEQ|**smallint**|Número de sequência da coluna em uma chave primária de várias colunas.|  
|PK_NAME|**sysname**|Identificador da chave primária. Retorna NULL se não for aplicável à fonte de dados.|  
  
## <a name="remarks"></a>Comentários  
 sp_pkeys retorna informações sobre colunas explicitamente definidas com uma restrição de chave primária. Como nem todos os sistemas oferecem suporte a chaves primárias explicitamente nomeadas, o implementador de gateway determina o que constitui uma chave primária. Observe que o termo chave primária refere-se a uma chave primária lógica para uma tabela. Espera-se que cada chave listada como chave primária lógica tenha um índice exclusivo definido. Este índice exclusivo também é retornado no sp_statistics.  
  
 O procedimento armazenado de sp_pkeys é equivalente a SQLPrimaryKeys no ODBC. Os resultados retornados são ordenados por TABLE_QUALIFIER, TABLE_OWNER, TABLE_NAME e KEY_SEQ.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão SELECT no esquema.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir recupera a chaves primária para a tabela `HumanResources.Department` no banco de dados `AdventureWorks2012`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_pkeys @table_name = N'Department'  
    ,@table_owner = N'HumanResources';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir recupera a chaves primária para a tabela `DimAccount` no banco de dados `AdventureWorksPDW2012`. Ele retorna zero linhas indicando que a tabela não tem uma chave primária.  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_pkeys @table_name = N'DimAccount;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados &#40; do catálogo Transact-SQL &#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

