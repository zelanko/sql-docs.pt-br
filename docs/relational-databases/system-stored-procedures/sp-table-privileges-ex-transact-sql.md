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
manager: craigg
ms.openlocfilehash: a11fb3f879336f5217abe138c91755154df868b5
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58534268"
---
# <a name="sptableprivilegesex-transact-sql"></a>sp_table_privileges_ex (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna as informações de privilégio sobre a tabela especificada do servidor vinculado especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_table_privileges_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]  
     [ , [@fUsePattern =] 'fUsePattern']  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @table_server = ] 'table_server'` É o nome do servidor vinculado para o qual retornar informações. *table_server* está **sysname**, sem padrão.  
  
`[ @table_name = ] 'table_name']` É o nome da tabela para a qual fornecer informações de privilégio de tabela. *table_name* está **sysname**, com um padrão NULL.  
  
`[ @table_schema = ] 'table_schema'` É o esquema da tabela. Em alguns ambientes DBMS, é o proprietário da tabela. *table_schema* está **sysname**, com um padrão NULL.  
  
`[ @table_catalog = ] 'table_catalog'` É o nome do banco de dados em que a especificada *table_name* reside. *table_catalog* está **sysname**, com um padrão NULL.  
  
`[ @fUsePattern = ] 'fUsePattern'` Determina se os caracteres '_', '%', ' [', e ']' são interpretados como caracteres curinga. Os valores válidos são 0 (correspondência de padrão desativada) e 1 (correspondência de padrão ativada). *fUsePattern* está **bit**, com um padrão de 1.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 None  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|Nome do qualificador de tabela. Vários produtos DBMS dão suporte à nomenclatura de três partes para tabelas (_qualificador_**.** _proprietário_**.** _nome_). No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna representa o nome do banco de dados. Em alguns produtos, ele representa o nome do servidor do ambiente de banco de dados da tabela. Esse campo pode ser NULL.|  
|**TABLE_SCHEM**|**sysname**|Nome do proprietário de tabela. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta coluna representa o nome do usuário de banco de dados que criou a tabela. Esse campo sempre retorna um valor.|  
|**TABLE_NAME**|**sysname**|Nome da tabela. Esse campo sempre retorna um valor.|  
|**CONCESSOR**|**sysname**|Nome de usuário de banco de dados que concedeu permissões neste **TABLE_NAME** para listado **usuário autorizado**. Na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna é sempre igual a **TABLE_OWNER**. Esse campo sempre retorna um valor. Além disso, a coluna GRANTOR pode ser o proprietário do banco de dados (**TABLE_OWNER**) ou um usuário a quem o proprietário do banco de dados concedeu permissão usando a cláusula WITH GRANT OPTION na instrução GRANT.|  
|**USUÁRIO AUTORIZADO**|**sysname**|Nome de usuário de banco de dados que concedeu permissões neste **TABLE_NAME** por listado **CONCESSOR**. Esse campo sempre retorna um valor.|  
|**PRIVILÉGIO**|**varchar(** 32 **)**|Uma das permissões de tabela disponíveis. As permissões de tabela podem ter um dos valores a seguir, ou outros valores que tenham suporte na fonte de dados quando a implementação é definida.<br /><br /> Selecione = **ao usuário autorizado** pode recuperar dados para um ou mais das colunas.<br /><br /> INSERT = **ao usuário autorizado** pode fornecer dados para novas linhas para uma ou mais das colunas.<br /><br /> UPDATE = **ao usuário autorizado** pode modificar dados existentes para um ou mais das colunas.<br /><br /> Excluir = **ao usuário autorizado** pode remover linhas da tabela.<br /><br /> REFERÊNCIAS = **ao usuário autorizado** pode fazer referência a uma coluna em uma tabela estrangeira em uma relação de chave estrangeira/chave primária. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as relações de chave primária/chave estrangeira são definidas usando restrições de tabela.<br /><br /> O escopo de ação dado para o **ao usuário autorizado** por uma tabela específica privilégio é dependente da fonte de dados. Por exemplo, a permissão UPDATE pode habilitar o **ao usuário autorizado** para atualizar todas as colunas em uma tabela em uma fonte de dados e somente aquelas colunas para o qual o **CONCESSOR** possui permissão UPDATE em outra fonte de dados.|  
|**IS_GRANTABLE**|**varchar(** 3 **)**|Indica se o **ao usuário autorizado** tem permissão para conceder permissões a outros usuários. Isso é frequentemente chamado de permissão de "concessão com concessão". Pode ser YES, NO ou NULL. Um valor desconhecido ou NULL refere-se a uma fonte de dados na qual a "concessão com concessão" não é aplicável.|  
  
## <a name="remarks"></a>Comentários  
 Os resultados retornados são ordenados por **TABLE_QUALIFIER**, **TABLE_OWNER**, **TABLE_NAME**, e **PRIVILÉGIO**.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão SELECT no esquema.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna as informações de privilégio sobre as tabelas com nomes que começam com `Product` no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] do servidor vinculado especificado `Seattle1`. ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é assumida como o servidor vinculado).  
  
```  
EXEC sp_table_privileges_ex @table_server = 'Seattle1',   
   @table_name = 'Product%',   
   @table_schema = 'Production',  
   @table_catalog ='AdventureWorks2012';  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_column_privileges_ex &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-ex-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Distribuído procedimentos armazenados de consultas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)  
  
  
