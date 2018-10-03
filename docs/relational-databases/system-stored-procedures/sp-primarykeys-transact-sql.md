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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d994e44e3db00921ca184ed063bcf1bdff487297
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47753594"
---
# <a name="spprimarykeys-transact-sql"></a>sp_primarykeys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna as colunas de chave primária, uma linha por coluna de chave, da tabela remota especificada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_primarykeys [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@table_server =** ] **' * * * table_server'*  
 É o nome do servidor vinculado a partir do qual as informações de chave primária devem ser retornadas. *table_server* está **sysname**, sem padrão.  
  
 [  **@table_name =** ] **'***table_name***'**  
 É o nome da tabela para a qual as informações de chave primária devem ser fornecidas. *table_name*está **sysname**, com um padrão NULL.  
  
 [  **@table_schema =** ] **'***table_schema***'**  
 É o esquema de tabela. *table_schema* está **sysname**, com um padrão NULL. No ambiente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], isso corresponde ao proprietário de tabela.  
  
 [  **@table_catalog =** ] **'***table_catalog***'**  
 É o nome do catálogo no qual especificado *table_name* reside. No ambiente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], isto corresponde ao nome do banco de dados. *table_catalog* está **sysname**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 None  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|Catálogo da tabela.|  
|**TABLE_SCHEM**|**sysname**|Esquema da tabela.|  
|**TABLE_NAME**|**sysname**|Nome da tabela.|  
|**COLUMN_NAME**|**sysname**|Nome da coluna.|  
|**KEY_SEQ**|**int**|Número de sequência da coluna em uma chave primária de várias colunas.|  
|**PK_NAME**|**sysname**|Identificador da chave primária. Retorna NULL se não for aplicável à fonte de dados.|  
  
## <a name="remarks"></a>Comentários  
 **sp_primarykeys** é executado consultando o conjunto de linhas PRIMARY_KEYS dos **IDBSchemaRowset** interface do provedor OLE DB correspondente *table_server*. O *table_name*, *table_schema*, *table_catalog*, e *coluna* parâmetros são passados para essa interface para restringir as linhas retornado.  
  
 **sp_primarykeys** retorna um resultado vazio definido se o provedor OLE DB do servidor vinculado especificado não dá suporte para o conjunto de linhas PRIMARY_KEYS dos **IDBSchemaRowset** interface.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Distribuído procedimentos armazenados de consultas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_column_privileges &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_foreignkeys &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [sp_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_tables_ex &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [sp_table_privileges &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
