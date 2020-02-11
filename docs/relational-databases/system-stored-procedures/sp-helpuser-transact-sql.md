---
title: sp_helpuser (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpuser
- sp_helpuser_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpuser
ms.assetid: 9c70b41d-ef4c-43df-92da-bd534c287ca1
author: stevestein
ms.author: sstein
ms.openlocfilehash: a170c5e43329d90a4977db12a98bd9d2e556e91d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68048166"
---
# <a name="sp_helpuser-transact-sql"></a>sp_helpuser (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Relata informações sobre principais em nível de banco de dados no banco de dados atual.  
  
> [!IMPORTANT]  
>  **sp_helpuser** não retorna informações sobre protegíveis que foram introduzidos no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Em vez disso, use [Sys. database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md) .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpuser [ [ @name_in_db = ] 'security_account' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @name_in_db = ] 'security_account'`É o nome do usuário de banco de dados ou da função de banco de dados no banco de dados atual. *security_account* deve existir no banco de dados atual. *security_account* é **sysname**, com um padrão de NULL. Se *security_account* não for especificado, **sp_helpuser** retornará informações sobre todas as entidades de banco de dados.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 A tabela a seguir mostra o conjunto de resultados quando nem uma conta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usuário nem um usuário do Windows é especificado para *security_account*.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**Usu**|**sysname**|Usuários no banco de dados atual.|  
|**RoleName**|**sysname**|Funções às quais o **nome de usuário** pertence.|  
|**LoginName**|**sysname**|Logon de **nome de usuário**.|  
|**DefDBName**|**sysname**|Banco de dados padrão de **nome de usuário**.|  
|**DefSchemaName**|**sysname**|Esquema padrão do usuário de banco de dados.|  
|**ID**|**smallint**|ID de **nome de usuário** no banco de dados atual.|  
|**SID**|**smallint**|Número de identificação de segurança (SID) do usuário.|  
  
 A tabela a seguir mostra o conjunto de resultados quando nenhum usuário é especificado e existem aliases no banco de dados atual.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|Logons com aliases para usuários no banco de dados atual.|  
|**UserNameAliasedTo**|**sysname**|Nome de usuário no banco de dados atual para o qual o logon possui alias.|  
  
 A tabela a seguir mostra o conjunto de resultados quando uma função é especificada para *security_account*.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**Role_name**|**sysname**|Nome da função no banco de dados atual.|  
|**Role_id**|**smallint**|ID de função para a função no banco de dados atual.|  
|**Users_in_role**|**sysname**|Membro da função no banco de dados atual.|  
|**ID**|**smallint**|ID de usuário do membro da função.|  
  
## <a name="remarks"></a>Comentários  
 Para ver informações sobre a associação de funções de banco de dados, use [Sys. database_role_members](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md). Para ver informações sobre membros da função de servidor, use [Sys. server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)e para ver informações sobre entidades de segurança no nível do servidor, use [Sys. server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
 As informações retornadas estão sujeitas a restrições no acesso para metadados. Entidades em que o principal não tem nenhuma permissão não aparecem. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-listing-all-users"></a>a. Listando todos os usuários  
 O exemplo a seguir lista todos os usuários no banco de dados atual.  
  
```  
EXEC sp_helpuser;  
```  
  
### <a name="b-listing-information-for-a-single-user"></a>B. Listando informações para um único usuário  
 O exemplo a seguir lista informações sobre o proprietário banco de dados de usuário (`dbo`).  
  
```  
EXEC sp_helpuser 'dbo';  
```  
  
### <a name="c-listing-information-for-a-database-role"></a>C. Listando informações para uma função de banco de dados  
 O exemplo a seguir lista informações sobre a função de banco de dados fixa `db_securityadmin`.  
  
```  
EXEC sp_helpuser 'db_securityadmin';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.server_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
  
