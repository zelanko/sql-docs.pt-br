---
title: sp_table_privileges_ex (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_table_privileges_ex
- sp_table_privileges_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_table_privileges_ex
ms.assetid: b58d4a07-5c40-4f17-b66e-6d6b17188dda
author: stevestein
ms.author: sstein
ms.openlocfilehash: b40f7233bb3c50203a68c0b01cfcbdaf631e0098
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68096176"
---
# <a name="sp_table_privileges_ex-transact-sql"></a>sp_table_privileges_ex (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna as informações de privilégio sobre a tabela especificada do servidor vinculado especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_table_privileges_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]  
     [ , [@fUsePattern =] 'fUsePattern']  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @table_server = ] 'table_server'`É o nome do servidor vinculado para o qual retornar informações. *table_server* é **sysname**, sem padrão.  
  
`[ @table_name = ] 'table_name']`É o nome da tabela para a qual fornecer informações de privilégio de tabela. *table_name* é **sysname**, com um padrão de NULL.  
  
`[ @table_schema = ] 'table_schema'`É o esquema de tabela. Em alguns ambientes DBMS, é o proprietário da tabela. *table_schema* é **sysname**, com um padrão de NULL.  
  
`[ @table_catalog = ] 'table_catalog'`É o nome do banco de dados no qual o *table_name* especificado reside. *TABLE_CATALOG* é **sysname**, com um padrão de NULL.  
  
`[ @fUsePattern = ] 'fUsePattern'`Determina se os caracteres ' _ ', '% ', ' [' e '] ' são interpretados como caracteres curinga. Os valores válidos são 0 (correspondência de padrão desativada) e 1 (correspondência de padrão ativada). *fUsePattern* é **bit**, com um padrão de 1.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhum  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|Nome do qualificador de tabela. Vários produtos DBMS dão suporte à nomeação de três partes para tabelas (_qualificador_**.** _proprietário_**.** _nome_). No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna representa o nome do banco de dados. Em alguns produtos, ele representa o nome do servidor do ambiente de banco de dados da tabela. Esse campo pode ser NULL.|  
|**TABLE_SCHEM**|**sysname**|Nome do proprietário da tabela. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna representa o nome do usuário de banco de dados que criou a tabela. Esse campo sempre retorna um valor.|  
|**TABLE_NAME**|**sysname**|Nome da tabela. Esse campo sempre retorna um valor.|  
|**CESSO**|**sysname**|O nome de usuário do banco de dados que concedeu permissões neste **table_name** ao **entidade autorizada**listado. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna é sempre a mesma que a **TABLE_OWNER**. Esse campo sempre retorna um valor. Além disso, a coluna concessor pode ser o proprietário do banco de dados (**TABLE_OWNER**) ou um usuário ao qual o proprietário do banco de dados concedeu permissão usando a cláusula com Option Grant na instrução Grant.|  
|**ENTIDADE autorizada**|**sysname**|Nome de usuário do banco de dados ao qual foram concedidas permissões neste **table_name** pelo **concessor**listado. Esse campo sempre retorna um valor.|  
|**PRIVILEGE**|**varchar (** 32 **)**|Uma das permissões de tabela disponíveis. As permissões de tabela podem ter um dos valores a seguir, ou outros valores que tenham suporte na fonte de dados quando a implementação é definida.<br /><br /> SELECT = **entidade autorizada** pode recuperar dados para uma ou mais das colunas.<br /><br /> INSERT = **entidade autorizada** pode fornecer dados para novas linhas para uma ou mais das colunas.<br /><br /> UPDATE = **entidade autorizada** pode modificar os dados existentes para uma ou mais colunas.<br /><br /> DELETE = **entidade autorizada** pode remover linhas da tabela.<br /><br /> REFERENCEs = **entidade autorizada** pode fazer referência a uma coluna em uma tabela estrangeira em uma relação de chave primária/chave estrangeira. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as relações de chave primária/chave estrangeira são definidas usando restrições de tabela.<br /><br /> O escopo de ação fornecido para o **entidade autorizada** por um privilégio de tabela específico é dependente da fonte de dados. Por exemplo, a permissão Atualizar pode permitir que o **entidade autorizada** atualize todas as colunas de uma tabela em uma fonte de dados e somente essas colunas para as quais o **concessor** tenha a permissão atualizar em outra fonte de dados.|  
|**IS_GRANTABLE**|**varchar (** 3 **)**|Indica se o **entidade autorizada** tem permissão para conceder permissões a outros usuários. Isso é frequentemente chamado de permissão de "concessão com concessão". Pode ser YES, NO ou NULL. Um valor desconhecido ou NULL refere-se a uma fonte de dados na qual a "concessão com concessão" não é aplicável.|  
  
## <a name="remarks"></a>Comentários  
 Os resultados retornados são ordenados por **TABLE_QUALIFIER**, **TABLE_OWNER**, **table_name**e **privilégio**.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão SELECT no esquema.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna as informações de privilégio sobre as tabelas com nomes que começam com `Product` no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] do servidor vinculado especificado `Seattle1`. ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] presume-se como o servidor vinculado).  
  
```  
EXEC sp_table_privileges_ex @table_server = 'Seattle1',   
   @table_name = 'Product%',   
   @table_schema = 'Production',  
   @table_catalog ='AdventureWorks2012';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_column_privileges_ex](../../relational-databases/system-stored-procedures/sp-column-privileges-ex-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados de consultas distribuídas &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)  
  
  
