---
title: sp_foreignkeys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_foreignkeys_TSQL
- sp_foreignkeys
dev_langs:
- TSQL
helpviewer_keywords:
- sp_foreignkeys
ms.assetid: 935fe385-19ff-41a4-8d0b-30618966991d
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ca6bd786330a3149313c11991454b016f5ed04ea
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spforeignkeys-transact-sql"></a>sp_foreignkeys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna as chaves estrangeiras que referenciam as chaves primárias na tabela do servidor vinculado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_foreignkeys [ @table_server = ] 'table_server'   
     [ , [ @pktab_name = ] 'pktab_name' ]   
     [ , [ @pktab_schema = ] 'pktab_schema' ]   
     [ , [ @pktab_catalog = ] 'pktab_catalog' ]   
     [ , [ @fktab_name = ] 'fktab_name' ]   
     [ , [ @fktab_schema = ] 'fktab_schema' ]   
     [ , [ @fktab_catalog = ] 'fktab_catalog' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@table_server =** ] **'***table_server***'**  
 É o nome do servidor vinculado para o qual as informações de tabela devem ser retornadas. *table_server* é **sysname**, sem padrão.  
  
 [  **@pktab_name =** ] **'***pktab_name***'**  
 É o nome da tabela com uma chave primária. *pktab_name* é **sysname**, com um padrão NULL.  
  
 [  **@pktab_schema =** ] **'***pktab_schema***'**  
 É o nome do esquema com uma chave primária. *pktab_schema*é **sysname**, com um padrão NULL. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ele contém o nome do proprietário.  
  
 [  **@pktab_catalog =** ] **'***pktab_catalog***'**  
 É o nome do catálogo com uma chave primária. *pktab_catalog*é **sysname**, com um padrão NULL. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ele contém o nome do banco de dados.  
  
 [  **@fktab_name =** ] **'***fktab_name***'**  
 É o nome do proprietário da tabela com uma chave estrangeira. *fktab_name*é **sysname**, com um padrão NULL.  
  
 [  **@fktab_schema =** ] **'***fktab_schema***'**  
 É o nome do esquema com uma chave estrangeira. *fktab_schema*é **sysname**, com um padrão NULL.  
  
 [  **@fktab_catalog =** ] **'***fktab_catalog***'**  
 É o nome do catálogo com uma chave estrangeira. *fktab_catalog*é **sysname**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhuma  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Vários produtos DBMS dão suporte à nomenclatura de três partes para tabelas (*catálogo ***.*** esquema ***.*** tabela*), que é representado no conjunto de resultados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**PKTABLE_CAT**|**sysname**|Catálogo para a tabela na qual a chave primária reside.|  
|**PKTABLE_SCHEM**|**sysname**|Esquema para a tabela na qual a chave primária reside.|  
|**PKTABLE_NAME**|**sysname**|Nome da tabela (com a chave primária). Esse campo sempre retorna um valor.|  
|**PKCOLUMN_NAME**|**sysname**|Nome da coluna de chave primária ou colunas, para cada coluna do **TABLE_NAME** retornado. Esse campo sempre retorna um valor.|  
|**FKTABLE_CAT**|**sysname**|Catálogo para a tabela na qual a chave estrangeira reside.|  
|**FKTABLE_SCHEM**|**sysname**|Esquema para a tabela na qual a chave estrangeira reside.|  
|**FKTABLE_NAME**|**sysname**|Nome da tabela (com a chave estrangeira). Esse campo sempre retorna um valor.|  
|**FKCOLUMN_NAME**|**sysname**|Nome das colunas de chave estrangeira, para cada coluna do TABLE_NAME retornado. Esse campo sempre retorna um valor.|  
|**KEY_SEQ**|**smallint**|Número de sequência da coluna em uma chave primária de várias colunas. Esse campo sempre retorna um valor.|  
|**UPDATE_RULE**|**smallint**|Ação aplicada à chave estrangeira quando a operação SQL é uma atualização. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna 0, 1 ou 2 para estas colunas:<br /><br /> 0=CASCADE altera para chave estrangeira.<br /><br /> 1=NO ACTION altera se a chave estrangeira estiver presente.<br /><br /> 2=SET_NULL define a chave estrangeira como NULL.|  
|**DELETE_RULE**|**smallint**|Ação aplicada à chave estrangeira quando a operação SQL é uma exclusão. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna 0, 1 ou 2 para estas colunas:<br /><br /> 0=CASCADE altera para chave estrangeira.<br /><br /> 1=NO ACTION altera se a chave estrangeira estiver presente.<br /><br /> 2=SET_NULL define a chave estrangeira como NULL.|  
|**COLUNAS FK_NAME**|**sysname**|Identificador de chave estrangeira. Será NULL se não for aplicável à fonte de dados. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna o nome da restrição de FOREIGN KEY.|  
|**PK_NAME**|**sysname**|Identificador da chave primária. Será NULL se não for aplicável à fonte de dados. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna o nome da restrição de PRIMARY KEY.|  
|**ADIAMENTO**|**smallint**|Indica se a verificação de restrição é adiável.|  
  
 No conjunto de resultados, as colunas FK_NAME e PK_NAME sempre retornam NULL.  
  
## <a name="remarks"></a>Remarks  
 **sp_foreignkeys** consulta o conjunto de linhas FOREIGN_KEYS o **IDBSchemaRowset** interface do provedor OLE DB que corresponde à *table_server*. O *table_name*, *table_schema*, *table_catalog*, e *coluna* parâmetros são passados para essa interface para restringir as linhas retornado.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão SELECT no esquema.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações de chave estrangeira sobre a tabela `Department` no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] do servidor vinculado, `Seattle1`.  
  
```  
EXEC sp_foreignkeys @table_server = N'Seattle1',   
   @pktab_name = N'Department',   
   @pktab_catalog = N'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_column_privileges &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_primarykeys &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-primarykeys-transact-sql.md)   
 [sp_tables_ex &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [sp_table_privileges &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
