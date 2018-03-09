---
title: sp_table_privileges (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_table_privileges
- sp_table_privileges_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_table_privileges
ms.assetid: 0512e688-4fc0-4557-8dc8-016672c1e3fe
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3f71b84e9f2aa0f732178a302f3d131f0a448dc0
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="sptableprivileges-transact-sql"></a>sp_table_privileges (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma lista de permissões de tabela (como INSERT, DELETE, UPDATE, SELECT, REFERENCES) para a tabela ou tabelas especificadas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_table_privileges [ @table_name = ] 'table_name'     
     [ , [ @table_owner = ] 'table_owner' ]   
     [ , [ @table_qualifier = ] 'table_qualifier' ]   
     [ , [ @fUsePattern = ] 'fUsePattern' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @table_name=] '*table_name*'  
 É a tabela usada para retornar informações do catálogo. *table_name* é **nvarchar (**384**)**, sem padrão. Há suporte para a correspondência do padrão curinga.  
  
 [ @table_owner=] '*table_owner*'  
 É o proprietário da tabela da tabela usada para retornar informações de catálogo. *table_owner*é **nvarchar (**384**)**, com um padrão NULL. Há suporte para a correspondência do padrão curinga. Se o proprietário não for especificado, serão aplicadas as regras de visibilidade de tabela padrão do DBMS subjacente.  
  
 Se o usuário atual possuir uma tabela com o nome especificado, as colunas dessa tabela serão retornadas. Se *proprietário* não for especificado e o usuário atual não possuir uma tabela com especificado *nome*, esse procedimento procurará uma tabela com especificado *table_name* pertencentes a proprietário do banco de dados. Caso exista, as colunas dessa tabela serão retornadas.  
  
 [ @table_qualifier=] '*table_qualifier*'  
 É o nome do qualificador da tabela. *table_qualifier* é **sysname**, com um padrão NULL. Vários produtos DBMS dão suporte à nomenclatura de três partes para tabelas (*qualificador*). No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna representa o nome do banco de dados. Em alguns produtos, representa o nome do servidor do ambiente de banco de dados da tabela.  
  
 [ @fUsePattern=] '*fUsePattern*'  
 Determina se o caractere de sublinhado (_), porcentagem (%)) e colchete ([ou]) caracteres são interpretados como caracteres curinga. Os valores válidos são 0 (correspondência de padrão desativada) e 1 (correspondência de padrão ativada). *fUsePattern* é **bit**, com um padrão de 1.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhuma  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|TABLE_QUALIFIER|**sysname**|Nome do qualificador de tabela. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna representa o nome do banco de dados. Esse campo pode ser NULL.|  
|TABLE_OWNER|**sysname**|Nome do proprietário de tabela. Esse campo sempre retorna um valor.|  
|TABLE_NAME|**sysname**|Nome da tabela. Esse campo sempre retorna um valor.|  
|GRANTOR|**sysname**|Nome do usuário do banco de dados que concedeu permissões nesse TABLE_NAME para o GRANTEE listado. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna é sempre igual a TABLE_OWNER. Esse campo sempre retorna um valor. Além disso, a coluna GRANTOR pode ser o proprietário do banco de dados (TABLE_OWNER) ou um usuário para o qual o proprietário do banco de dados concedeu permissão usando a cláusula WITH GRANT OPTION na instrução GRANT.|  
|GRANTEE|**sysname**|O nome do usuário do banco de dados ao qual as permissões nesse TABLE_NAME foram concedidas pelo GRANTOR listado. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna sempre inclui um usuário de banco de dados do modo de exibição sys.database_principalssystem. Esse campo sempre retorna um valor.|  
|PRIVILEGE|**sysname**|Uma das permissões de tabela disponíveis. As permissões de tabela podem ter um dos seguintes valores (ou outros valores que tenham suporte na fonte de dados quando a implementação for definida):<br /><br /> SELECT = GRANTEE pode recuperar dados para uma ou mais colunas.<br /><br /> INSERT = GRANTEE pode fornecer dados a novas linhas para uma ou mais colunas.<br /><br /> UPDATE = GRANTEE pode modificar dados existentes para uma ou mais colunas.<br /><br /> DELETE = GRANTEE pode remover linhas da tabela.<br /><br /> REFERENCES = GRANTEE pode referenciar uma coluna em uma tabela estrangeira em uma relação de chave primária/chave estrangeira. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as relações de chave primária/chave estrangeira são definidas com restrições de tabela.<br /><br /> O escopo de ação dado ao GRANTEE por um determinado privilégio de tabela é dependente da fonte de dados. Por exemplo, o privilégio UPDATE pode permitir que o GRANTEE atualize todas as colunas de uma tabela em uma fonte de dados e somente aquelas colunas para as quais o GRANTOR possui o privilégio UPDATE em outra fonte de dados.|  
|IS_GRANTABLE|**sysname**|Indica se o GRANTEE tem ou não permissão para conceder permissões a outros usuários (em geral referida como permissão "concessão com concessão"). Pode ser YES, NO ou NULL. Um valor desconhecido (ou NULL) refere-se a uma fonte de dados para a qual a "concessão com concessão" não é aplicável.|  
  
## <a name="remarks"></a>Comentários  
 O procedimento armazenado sp_table_privileges é equivalente a SQLTablePrivileges no ODBC. Os resultados retornados são ordenados por TABLE_QUALIFIER, TABLE_OWNER, TABLE_NAME e PRIVILEGE.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão SELECT no esquema.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações de privilégio sobre todas as tabelas com nomes que iniciem com a palavra `Contact`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_table_privileges   
   @table_name = 'Contact%';  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados &#40; do catálogo Transact-SQL &#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
