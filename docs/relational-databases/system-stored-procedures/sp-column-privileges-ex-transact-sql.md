---
title: sp_column_privileges_ex (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_column_privileges_ex
- sp_column_privileges_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_column_privileges_ex
ms.assetid: 98cb6e58-4007-40fc-b048-449fb2e7e6be
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b79fbbd504f7294835e92401a2210e6acac3c440
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52514018"
---
# <a name="spcolumnprivilegesex-transact-sql"></a>sp_column_privileges_ex (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna os privilégios de coluna para a tabela especificada no servidor vinculado especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_column_privileges_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]   
     [ , [ @column_name = ] 'column_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@table_server =** ] **'**_table_server_**'**  
 É o nome do servidor vinculado para o qual as informações devem ser retornadas. *table_server* está **sysname**, sem padrão.  
  
 [  **@table_name =** ] **'**_table_name_**'**  
 É o nome da tabela que contém a coluna especificada. *table_name* está **sysname**, com um padrão NULL.  
  
 [  **@table_schema =** ] **'**_table_schema_**'**  
 É o esquema de tabela. *table_schema* está **sysname**, com um padrão NULL.  
  
 [  **@table_catalog =** ] **'**_table_catalog_**'**  
 É o nome do banco de dados em que a especificada *table_name* reside. *table_catalog* está **sysname**, com um padrão NULL.  
  
 [  **@column_name =** ] **'**_column_name_**'**  
 É o nome da coluna para a qual fornecer informações de privilégio. *column_name* está **sysname**, com um padrão de NULL (tudo comum).  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 A tabela a seguir mostra as colunas do conjunto de resultados. Os resultados retornados são ordenados por **TABLE_QUALIFIER**, **TABLE_OWNER**, **TABLE_NAME**, **COLUMN_NAME**, e  **PRIVILÉGIO**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|Nome do qualificador de tabela. Vários produtos DBMS dão suporte à nomenclatura de três partes para tabelas (_qualificador_**.** _proprietário_**.** _nome_). No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna representa o nome do banco de dados. Em alguns produtos, ele representa o nome do servidor do ambiente de banco de dados da tabela. Esse campo pode ser NULL.|  
|**TABLE_SCHEM**|**sysname**|Nome do proprietário de tabela. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta coluna representa o nome do usuário de banco de dados que criou a tabela. Esse campo sempre retorna um valor.|  
|**TABLE_NAME**|**sysname**|Nome da tabela. Esse campo sempre retorna um valor.|  
|**COLUMN_NAME**|**sysname**|Nome da coluna para cada coluna do **TABLE_NAME** retornado. Esse campo sempre retorna um valor.|  
|**CONCESSOR**|**sysname**|Nome de usuário de banco de dados que concedeu permissões neste **COLUMN_NAME** para listado **usuário autorizado**. Na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna é sempre igual a **TABLE_OWNER**. Esse campo sempre retorna um valor.<br /><br /> O **CONCESSOR** coluna pode ser o proprietário do banco de dados (**TABLE_OWNER**) ou alguém para quem o proprietário do banco de dados concedeu permissões usando a cláusula WITH GRANT OPTION na instrução GRANT.|  
|**USUÁRIO AUTORIZADO**|**sysname**|Nome de usuário de banco de dados que concedeu permissões neste **COLUMN_NAME** por listado **CONCESSOR**. Esse campo sempre retorna um valor.|  
|**PRIVILÉGIO**|**varchar(** 32 **)**|Uma das permissões de coluna disponíveis. As permissões de coluna podem ter um dos seguintes valores (ou outros valores que tenham suporte na fonte de dados quando a implementação é definida):<br /><br /> Selecione = **ao usuário autorizado** pode recuperar dados para as colunas.<br /><br /> INSERT = **ao usuário autorizado** pode fornecer dados para esta coluna quando novas linhas são inseridas (pelo **usuário autorizado**) na tabela.<br /><br /> UPDATE = **ao usuário autorizado** pode modificar dados existentes na coluna.<br /><br /> REFERÊNCIAS = **ao usuário autorizado** pode fazer referência a uma coluna em uma tabela estrangeira em uma relação de chave estrangeira/chave primária. As relações de chave primária/chave estrangeira são definidas com restrições de tabela.|  
|**IS_GRANTABLE**|**varchar (** 3 **)**|Indica se o **ao usuário autorizado** tem permissão para conceder permissões a outros usuários (também conhecidos como permissão "concessão com concessão"). Pode ser YES, NO ou NULL. Um desconhecido ou NULL, o valor se refere a uma fonte de dados em que "concessão com concessão" não é aplicável.|  
  
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
 [sp_table_privileges_ex &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-ex-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
