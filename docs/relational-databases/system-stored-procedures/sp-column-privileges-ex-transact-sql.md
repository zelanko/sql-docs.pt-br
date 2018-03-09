---
title: sp_column_privileges_ex (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_column_privileges_ex
- sp_column_privileges_ex_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_column_privileges_ex
ms.assetid: 98cb6e58-4007-40fc-b048-449fb2e7e6be
caps.latest.revision: "34"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1f374a87fe41d08774eca9bd0e90de42d5204cbe
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="spcolumnprivilegesex-transact-sql"></a>sp_column_privileges_ex (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna os privilégios de coluna para a tabela especificada no servidor vinculado especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_column_privileges_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]   
     [ , [ @column_name = ] 'column_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@table_server =** ] **'***table_server***'**  
 É o nome do servidor vinculado para o qual as informações devem ser retornadas. *table_server* é **sysname**, sem padrão.  
  
 [  **@table_name =** ] **'***table_name***'**  
 É o nome da tabela que contém a coluna especificada. *table_name* é **sysname**, com um padrão NULL.  
  
 [  **@table_schema =** ] **'***table_schema***'**  
 É o esquema de tabela. *table_schema* é **sysname**, com um padrão NULL.  
  
 [  **@table_catalog =** ] **'***table_catalog***'**  
 É o nome do banco de dados em que o especificado *table_name* reside. *table_catalog* é **sysname**, com um padrão NULL.  
  
 [  **@column_name =** ] **'***column_name***'**  
 É o nome da coluna para a qual fornecer informações de privilégio. *nome da coluna* é **sysname**, com um padrão de NULL (tudo comum).  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 A tabela a seguir mostra as colunas do conjunto de resultados. Os resultados retornados são ordenados por **TABLE_QUALIFIER**, **TABLE_OWNER**, **TABLE_NAME**, **COLUMN_NAME**, e  **PRIVILÉGIO**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|Nome do qualificador de tabela. Vários produtos DBMS dão suporte à nomenclatura de três partes para tabelas (*qualificador***.** *proprietário***.** *nome*). No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna representa o nome do banco de dados. Em alguns produtos, representa o nome do servidor do ambiente de banco de dados da tabela. Esse campo pode ser NULL.|  
|**TABLE_SCHEM**|**sysname**|Nome do proprietário de tabela. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta coluna representa o nome do usuário de banco de dados que criou a tabela. Esse campo sempre retorna um valor.|  
|**TABLE_NAME**|**sysname**|Nome da tabela. Esse campo sempre retorna um valor.|  
|**NOME DA COLUNA**|**sysname**|Nome da coluna para cada coluna do **TABLE_NAME** retornado. Esse campo sempre retorna um valor.|  
|**CONCESSOR**|**sysname**|Nome de usuário de banco de dados que concedeu permissões neste **COLUMN_NAME** para listado **usuário autorizado**. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna é sempre o mesmo que o **TABLE_OWNER**. Esse campo sempre retorna um valor.<br /><br /> O **CONCESSOR** coluna pode ser o proprietário do banco de dados (**TABLE_OWNER**) ou alguém para quem o proprietário do banco de dados concedeu permissões usando a cláusula WITH GRANT OPTION na instrução GRANT.|  
|**USUÁRIO AUTORIZADO**|**sysname**|Nome de usuário de banco de dados que concedeu permissões neste **COLUMN_NAME** por listado **CONCESSOR**. Esse campo sempre retorna um valor.|  
|**PRIVILÉGIO**|**varchar (**32**)**|Uma das permissões de coluna disponíveis. As permissões de coluna podem ter um dos seguintes valores (ou outros valores que tenham suporte na fonte de dados quando a implementação é definida):<br /><br /> Selecione = **usuário autorizado** pode recuperar dados para as colunas.<br /><br /> INSERT = **usuário autorizado** pode fornecer dados para esta coluna quando novas linhas são inseridas (pelo **usuário autorizado**) na tabela.<br /><br /> UPDATE = **usuário autorizado** pode modificar dados existentes na coluna.<br /><br /> REFERÊNCIAS = **usuário autorizado** pode fazer referência a uma coluna em uma tabela estrangeira em uma relação de chave estrangeira/de chave primária. As relações de chave primária/chave estrangeira são definidas com restrições de tabela.|  
|**IS_GRANTABLE**|**varchar (**3**)**|Indica se o **usuário autorizado** tem permissão para conceder permissões a outros usuários (também conhecidos como permissão "concessão com concessão"). Pode ser YES, NO ou NULL. Um desconhecido ou NULL, o valor refere-se a uma fonte de dados onde "concessão com concessão" não é aplicável.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão SELECT no esquema.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações de privilégio de coluna para a tabela `HumanResources.Department` no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] do servidor vinculado, `Seattle1`.  
  
```  
EXEC sp_column_privileges_ex @table_server = 'Seattle1',   
   @table_name = 'Department',   
   @table_schema = 'HumanResources',  
   @table_catalog ='AdventureWorks2012';  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_table_privileges_ex &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-ex-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
