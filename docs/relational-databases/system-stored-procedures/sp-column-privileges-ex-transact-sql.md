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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5ec2f3a3f300a6501a23b4bd88234571b0717d2a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85771276"
---
# <a name="sp_column_privileges_ex-transact-sql"></a>sp_column_privileges_ex (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Retorna os privilégios de coluna para a tabela especificada no servidor vinculado especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_column_privileges_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]   
     [ , [ @column_name = ] 'column_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @table_server = ] 'table_server'`É o nome do servidor vinculado para o qual retornar informações. *table_server* é **sysname**, sem padrão.  
  
`[ @table_name = ] 'table_name'`É o nome da tabela que contém a coluna especificada. *table_name* é **sysname**, com um padrão de NULL.  
  
`[ @table_schema = ] 'table_schema'`É o esquema de tabela. *table_schema* é **sysname**, com um padrão de NULL.  
  
`[ @table_catalog = ] 'table_catalog'`É o nome do banco de dados no qual o *table_name* especificado reside. *TABLE_CATALOG* é **sysname**, com um padrão de NULL.  
  
`[ @column_name = ] 'column_name'`É o nome da coluna para a qual fornecer informações de privilégio. *column_name* é **sysname**, com um padrão de NULL (todos os comuns).  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 A tabela a seguir mostra as colunas do conjunto de resultados. Os resultados retornados são ordenados por **TABLE_QUALIFIER**, **TABLE_OWNER**, **table_name**, **column_name**e **privilégio**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|Nome do qualificador de tabela. Vários produtos DBMS dão suporte à nomeação de três partes para tabelas (_qualificador_**.** _proprietário_**.** _nome_). No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna representa o nome do banco de dados. Em alguns produtos, ele representa o nome do servidor do ambiente de banco de dados da tabela. Esse campo pode ser NULL.|  
|**TABLE_SCHEM**|**sysname**|Nome do proprietário da tabela. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , essa coluna representa o nome do usuário de banco de dados que criou a tabela. Esse campo sempre retorna um valor.|  
|**TABLE_NAME**|**sysname**|Nome da tabela. Esse campo sempre retorna um valor.|  
|**COLUMN_NAME**|**sysname**|Nome da coluna, para cada coluna da **table_name** retornada. Esse campo sempre retorna um valor.|  
|**CESSO**|**sysname**|O nome de usuário do banco de dados que concedeu permissões neste **column_name** ao **entidade autorizada**listado. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , essa coluna é sempre a mesma que a **TABLE_OWNER**. Esse campo sempre retorna um valor.<br /><br /> A coluna de **concessor** pode ser o proprietário do banco de dados (**TABLE_OWNER**) ou alguém ao qual o proprietário do banco de dados concedeu permissões usando a cláusula com Option Grant na instrução Grant.|  
|**ENTIDADE autorizada**|**sysname**|Nome de usuário do banco de dados que recebeu permissões neste **column_name** pelo **concessor**listado. Esse campo sempre retorna um valor.|  
|**PRIVILEGE**|**varchar (** 32 **)**|Uma das permissões de coluna disponíveis. As permissões de coluna podem ter um dos seguintes valores (ou outros valores que tenham suporte na fonte de dados quando a implementação é definida):<br /><br /> SELECT = **entidade autorizada** pode recuperar dados para as colunas.<br /><br /> INSERT = **entidade autorizada** pode fornecer dados para essa coluna quando novas linhas são inseridas (por **entidade autorizada**) na tabela.<br /><br /> UPDATE = **entidade autorizada** pode modificar os dados existentes na coluna.<br /><br /> REFERENCEs = **entidade autorizada** pode fazer referência a uma coluna em uma tabela estrangeira em uma relação de chave primária/chave estrangeira. As relações de chave primária/chave estrangeira são definidas com restrições de tabela.|  
|**IS_GRANTABLE**|**varchar (** 3 **)**|Indica se o **entidade autorizada** tem permissão para conceder permissões a outros usuários (geralmente chamados de permissão "Grant com Grant"). Pode ser YES, NO ou NULL. Um valor desconhecido, ou nulo, refere-se a uma fonte de dados em que "Grant com Grant" não é aplicável.|  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_table_privileges_ex](../../relational-databases/system-stored-procedures/sp-table-privileges-ex-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
