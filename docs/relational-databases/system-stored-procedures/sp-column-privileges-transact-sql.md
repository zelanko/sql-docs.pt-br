---
title: sp_column_privileges (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_column_privileges_TSQL
- sp_column_privileges
dev_langs:
- TSQL
helpviewer_keywords:
- sp_column_privileges
ms.assetid: a3784301-2517-4b1d-bbd9-47404483fad0
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c9f8ded0dfc540ab695342fc1765bf53e880ec0e
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52538060"
---
# <a name="spcolumnprivileges-transact-sql"></a>sp_column_privileges (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna informações de privilégio de coluna para uma única tabela no ambiente atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_column_privileges [ @table_name = ] 'table_name'   
     [ , [ @table_owner = ] 'table_owner' ]   
     [ , [ @table_qualifier = ] 'table_qualifier' ]   
     [ , [ @column_name = ] 'column' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @table_name=] '*table_name*'  
 É a tabela usada para retornar informações do catálogo. *table_name* está **sysname**, sem padrão. Não há suporte para a correspondência de padrão curinga.  
  
 [ @table_owner=] '*table_owner*'  
 É o proprietário da tabela usada para retornar informações do catálogo. *table_owner* está **sysname**, com um padrão NULL. Não há suporte para a correspondência de padrão curinga. Se *table_owner* não for especificado, as regras de visibilidade de tabela padrão do sistema de gerenciamento de banco de dados (DBMS) subjacente se aplicam.  
  
 Se o usuário atual possuir uma tabela com o nome especificado, as colunas dessa tabela serão retornadas. Se *table_owner* não for especificado e o usuário atual não possuir uma tabela com especificado *table_name*, procurará uma tabela com os privilégios de sp_column *table_name* pertencente ao proprietário do banco de dados. Se ela existir, as colunas dessa tabela serão retornadas.  
  
 [ @table_qualifier=] '*table_qualifier*'  
 É o nome do qualificador da tabela. *table_qualifier* está *sysname*, com um padrão NULL. Vários produtos DBMS dão suporte à nomenclatura de três partes para tabelas (_qualificador_**.** _proprietário_**.** _nome_). No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna representa o nome do banco de dados. Em alguns produtos, ele representa o nome do servidor do ambiente de banco de dados da tabela.  
  
 [ @column_name=] '*coluna*'  
 É uma única coluna usada quando somente uma coluna de informações do catálogo é obtida. *coluna* está **nvarchar (** 384 **)**, com um padrão NULL. Se *coluna* não é especificado, todas as colunas são retornadas. Na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], *coluna* representa o nome da coluna conforme listado na tabela sys. Columns. *coluna* pode incluir caracteres curinga usando padrões do DBMS subjacente de correspondência de curinga. Para obter a interoperabilidade máxima, o cliente de gateway deve pressupor correspondência apenas do padrão ISO (curingas com % e _).  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 sp_column_privileges é equivalente a SQLColumnPrivileges no ODBC. Os resultados retornados são ordenados por TABLE_QUALIFIER, TABLE_OWNER, TABLE_NAME, COLUMN_NAME e PRIVILEGE.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|TABLE_QUALIFIER|**sysname**|Nome do qualificador de tabela. Esse campo pode ser NULL.|  
|TABLE_OWNER|**sysname**|Nome do proprietário de tabela. Esse campo sempre retorna um valor.|  
|TABLE_NAME|**sysname**|Nome da tabela. Esse campo sempre retorna um valor.|  
|COLUMN_NAME|**sysname**|Nome de cada coluna do TABLE_NAME retornado. Esse campo sempre retorna um valor.|  
|GRANTOR|**sysname**|Nome de usuário do banco de dados que concedeu permissões neste COLUMN_NAME para o GRANTEE listado. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna é sempre igual a TABLE_OWNER. Esse campo sempre retorna um valor.<br /><br /> A coluna GRANTOR pode ser o proprietário do banco de dados (TABLE_OWNER) ou um usuário ao qual o proprietário do banco de dados concedeu permissões usando a cláusula WITH GRANT OPTION na instrução GRANT.|  
|GRANTEE|**sysname**|O nome de usuário do banco de dados ao qual as permissões neste COLUMN_NAME foram concedidas pelo GRANTEE listado. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta coluna sempre inclui um usuário de banco de dados da tabela sysusers. Esse campo sempre retorna um valor.|  
|PRIVILEGE|**varchar(** 32 **)**|Uma das permissões de coluna disponíveis. As permissões de coluna podem ter um dos seguintes valores (ou outros valores que tenham suporte na fonte de dados quando a implementação é definida):<br /><br /> SELECT = GRANTEE pode recuperar dados para as colunas.<br /><br /> INSERT = GRANTEE pode fornecer dados para esta coluna quando novas linhas são inseridas (pelo GRANTEE) na tabela.<br /><br /> UPDATE = GRANTEE pode modificar os dados existentes na coluna.<br /><br /> REFERENCES = GRANTEE pode referenciar uma coluna em uma tabela estrangeira em uma relação de chave primária/chave estrangeira. As relações de chave primária/chave estrangeira são definidas usando restrições de tabela.|  
|IS_GRANTABLE|**varchar (** 3 **)**|Indica se GRANTEE tem permissão para conceder permissões a outros usuários (em geral, referenciada como permissão de "concessão com concessão"). Pode ser YES, NO ou NULL. Um valor desconhecido ou NULL refere-se a uma fonte de dados para a qual a "concessão com concessão" não é aplicável.|  
  
## <a name="remarks"></a>Comentários  
 Com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as permissões são concedidas com a instrução GRANT e retiradas com a instrução REVOKE.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão SELECT no esquema.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna as informações de privilégio de coluna para uma coluna específica.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_column_privileges @table_name = 'Employee'   
    ,@table_owner = 'HumanResources'  
    ,@table_qualifier = 'AdventureWorks2012'  
    ,@column_name = 'SalariedFlag';  
```  
  
## <a name="see-also"></a>Consulte também  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
