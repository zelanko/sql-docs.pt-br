---
title: sp_primarykeys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_primarykeys_TSQL
- sp_primarykeys
dev_langs:
- TSQL
helpviewer_keywords:
- sp_primarykeys
ms.assetid: 0f76dd31-5b7b-4209-9e2e-b9ed5cac164d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 05a1563188b5a8332c547901247ef43e07b1efa5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85646124"
---
# <a name="sp_primarykeys-transact-sql"></a>sp_primarykeys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Retorna as colunas de chave primária, uma linha por coluna de chave, da tabela remota especificada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_primarykeys [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @table_server = ] 'table_server'_`É o nome do servidor vinculado do qual retornar informações de chave primária. *table_server* é **sysname**, sem padrão.  
  
`[ @table_name = ] 'table_name'`É o nome da tabela para a qual fornecer informações de chave primária. *table_name*é **sysname**, com um padrão de NULL.  
  
`[ @table_schema = ] 'table_schema'`É o esquema de tabela. *table_schema* é **sysname**, com um padrão de NULL. No ambiente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], isso corresponde ao proprietário de tabela.  
  
`[ @table_catalog = ] 'table_catalog'`É o nome do catálogo no qual o *table_name* especificado reside. No ambiente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], isto corresponde ao nome do banco de dados. *TABLE_CATALOG* é **sysname**, com um padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhum  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|Catálogo da tabela.|  
|**TABLE_SCHEM**|**sysname**|Esquema da tabela.|  
|**TABLE_NAME**|**sysname**|Nome da tabela.|  
|**COLUMN_NAME**|**sysname**|Nome da coluna.|  
|**KEY_SEQ**|**int**|Número de sequência da coluna em uma chave primária de várias colunas.|  
|**PK_NAME**|**sysname**|Identificador da chave primária. Retorna NULL se não for aplicável à fonte de dados.|  
  
## <a name="remarks"></a>Comentários  
 **sp_primarykeys** é executado consultando o conjunto de linhas de PRIMARY_KEYS da interface **IDBSchemaRowset** do provedor de OLE DB correspondente ao *table_server*. Os parâmetros *table_name*, *table_schema*, *TABLE_CATALOG*e *coluna* são passados para essa interface para restringir as linhas retornadas.  
  
 **sp_primarykeys** retornará um conjunto de resultados vazio se o provedor de OLE DB do servidor vinculado especificado não oferecer suporte ao conjunto de linhas PRIMARY_KEYS da interface **IDBSchemaRowset** .  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão SELECT no esquema.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna as colunas da chave primária do servidor `LONDON1` para a tabela `HumanResources.JobCandidate` no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
EXEC sp_primarykeys @table_server = N'LONDON1',   
   @table_name = N'JobCandidate',  
   @table_catalog = N'AdventureWorks2012',   
   @table_schema = N'HumanResources';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de consultas distribuídas &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_catalogs](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_column_privileges](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_foreignkeys](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_indexes](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_linkedservers](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_tables_ex](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_table_privileges](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
