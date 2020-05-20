---
title: sp_tables_ex (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_tables_ex
- sp_tables_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_tables_ex
ms.assetid: 33755c33-7e1e-4ef7-af14-a9cebb1e2ed4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5ebb27860d7b7da46680a61486c59de3929117ce
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82834183"
---
# <a name="sp_tables_ex-transact-sql"></a>sp_tables_ex (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna as informações de tabela sobre as tabelas do servidor vinculado especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_tables_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]  
     [ , [ @table_catalog = ] 'table_catalog' ]   
     [ , [ @table_type = ] 'table_type' ]   
     [ , [@fUsePattern = ] 'fUsePattern' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @table_server = ] 'table_server'`É o nome do servidor vinculado para o qual retornar informações de tabela. *table_server* é **sysname**, sem padrão.  
  
``[ , [ @table_name = ] 'table_name']``É o nome da tabela para a qual retornar informações de tipo de dados. *table_name*é **sysname**, com um padrão de NULL.  
  
`[ @table_schema = ] 'table_schema']`É o esquema de tabela. *table_schema*é **sysname**, com um padrão de NULL.  
  
`[ @table_catalog = ] 'table_catalog'`É o nome do banco de dados no qual o *table_name* especificado reside. *TABLE_CATALOG* é **sysname**, com um padrão de NULL.  
  
`[ @table_type = ] 'table_type'`É o tipo da tabela a ser retornada. *TABLE_TYPE* é **sysname**, com um padrão de NULL, e pode ter um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**RECEBER**|Nome de um alias.|  
|**GLOBAL TEMPORARY**|Nome de uma tabela temporária disponível no sistema.|  
|**LOCAL TEMPORARY**|Nome de uma tabela temporária disponível somente para o trabalho atual.|  
|**SYNONYM**|Nome de um sinônimo.|  
|**TABELA DO SISTEMA**|Nome de uma tabela do sistema.|  
|**EXIBIÇÃO DO SISTEMA**|Nome de uma exibição do sistema.|  
|**TABELA**|Nome de uma tabela de usuário.|  
|**VIEW**|Nome de uma exibição.|  
  
`[ @fUsePattern = ] 'fUsePattern'`Determina se os caracteres **_**, **%** , **[** e **]** são interpretados como caracteres curinga. Os valores válidos são 0 (correspondência de padrão desativada) e 1 (correspondência de padrão ativada). *fUsePattern* é **bit**, com um padrão de 1.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Não  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|Nome do qualificador de tabela. Vários produtos DBMS dão suporte à nomeação de três partes para tabelas (_qualificador_**.** _proprietário_**.** _nome_). No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna representa o nome do banco de dados. Em outros produtos, ela representa o nome do servidor do ambiente de banco de dados da tabela. Esse campo pode ser NULL.|  
|**TABLE_SCHEM**|**sysname**|Nome do proprietário da tabela. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , essa coluna representa o nome do usuário de banco de dados que criou a tabela. Esse campo sempre retorna um valor.|  
|**TABLE_NAME**|**sysname**|Nome da tabela. Esse campo sempre retorna um valor.|  
|**TABLE_TYPE**|**varchar (32)**|Tabela, tabela do sistema ou exibição.|  
|**COMENTÁRIOS**|**varchar (254)**|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não retorna um valor para essa coluna.|  
  
## <a name="remarks"></a>Comentários  
 **sp_tables_ex** é executado consultando o conjunto de linhas de tabelas da interface **IDBSchemaRowset** do provedor de OLE DB correspondente ao *table_server*. Os parâmetros *table_name*, *table_schema*, *TABLE_CATALOG*e *coluna* são passados para essa interface para restringir as linhas retornadas.  
  
 **sp_tables_ex** retornará um conjunto de resultados vazio se o provedor de OLE DB do servidor vinculado especificado não oferecer suporte ao conjunto de linhas de tabelas da interface **IDBSchemaRowset** .  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão SELECT no esquema.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações sobre as tabelas que estão contidas no esquema `HumanResources` do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] do servidor vinculado `LONDON2`.  
  
```  
EXEC sp_tables_ex @table_server = 'LONDON2',   
@table_catalog = 'AdventureWorks2012',   
@table_schema = 'HumanResources',   
@table_type = 'TABLE';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de consultas distribuídas &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_catalogs](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_columns_ex](../../relational-databases/system-stored-procedures/sp-columns-ex-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_column_privileges](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_foreignkeys](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_indexes](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_linkedservers](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_table_privileges](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
