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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5d135b3b4b0f9d63ccd89db04be259f3c7031b7e
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58538488"
---
# <a name="sptablesex-transact-sql"></a>sp_tables_ex (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna as informações de tabela sobre as tabelas do servidor vinculado especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @table_server = ] 'table_server'` É o nome do servidor vinculado para o qual retornar informações de tabela. *table_server* está **sysname**, sem padrão.  
  
``[ , [ @table_name = ] 'table_name']`` É o nome da tabela para a qual retornar informações de tipo de dados. *table_name*está **sysname**, com um padrão NULL.  
  
`[ @table_schema = ] 'table_schema']` É o esquema da tabela. *table_schema*está **sysname**, com um padrão NULL.  
  
`[ @table_catalog = ] 'table_catalog'` É o nome do banco de dados em que a especificada *table_name* reside. *table_catalog* está **sysname**, com um padrão NULL.  
  
`[ @table_type = ] 'table_type'` É o tipo da tabela para retornar. *TABLE_TYPE* está **sysname**, com um padrão de NULL e pode ter um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**ALIAS**|Nome de um alias.|  
|**TEMPORÁRIO GLOBAL**|Nome de uma tabela temporária disponível no sistema.|  
|**TEMPORÁRIO LOCAL**|Nome de uma tabela temporária disponível somente para o trabalho atual.|  
|**SYNONYM**|Nome de um sinônimo.|  
|**TABELA DO SISTEMA**|Nome de uma tabela do sistema.|  
|**EXIBIÇÃO DO SISTEMA**|Nome de uma exibição do sistema.|  
|**TABLE**|Nome de uma tabela de usuário.|  
|**VIEW**|Nome de uma exibição.|  
  
`[ @fUsePattern = ] 'fUsePattern'` Determina se os caracteres **_**, **%**, **[**, e **]** são interpretados como caracteres curinga. Os valores válidos são 0 (correspondência de padrão desativada) e 1 (correspondência de padrão ativada). *fUsePattern* está **bit**, com um padrão de 1.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 None  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|Nome do qualificador de tabela. Vários produtos DBMS dão suporte à nomenclatura de três partes para tabelas (_qualificador_**.** _proprietário_**.** _nome_). No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna representa o nome do banco de dados. Em outros produtos, ela representa o nome do servidor do ambiente de banco de dados da tabela. Esse campo pode ser NULL.|  
|**TABLE_SCHEM**|**sysname**|Nome do proprietário de tabela. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta coluna representa o nome do usuário de banco de dados que criou a tabela. Esse campo sempre retorna um valor.|  
|**TABLE_NAME**|**sysname**|Nome da tabela. Esse campo sempre retorna um valor.|  
|**TABLE_TYPE**|**varchar(32)**|Tabela, tabela do sistema ou exibição.|  
|**REMARKS**|**varchar(254)**|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não retorna um valor para essa coluna.|  
  
## <a name="remarks"></a>Comentários  
 **sp_tables_ex** é executado consultando o conjunto de linhas de tabelas do **IDBSchemaRowset** interface do provedor OLE DB correspondente a *table_server*. O *table_name*, *table_schema*, *table_catalog*, e *coluna* parâmetros são passados para essa interface para restringir as linhas retornado.  
  
 **sp_tables_ex** retorna um resultado vazio definido se o provedor OLE DB do servidor vinculado especificado não dá suporte para o conjunto de linhas de tabelas do **IDBSchemaRowset** interface.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Distribuído procedimentos armazenados de consultas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_columns_ex &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-columns-ex-transact-sql.md)   
 [sp_column_privileges &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_foreignkeys &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [sp_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_table_privileges &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
