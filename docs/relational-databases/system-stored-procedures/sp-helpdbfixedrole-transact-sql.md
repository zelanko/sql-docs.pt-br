---
title: sp_helpdbfixedrole (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpdbfixedrole
- sp_helpdbfixedrole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpdbfixedrole
ms.assetid: ad87e9a0-b901-4e37-9950-aa517d680fc3
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8b029430388e1f58a725e5eb15795fa47380eda7
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85899547"
---
# <a name="sp_helpdbfixedrole-transact-sql"></a>sp_helpdbfixedrole (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma lista das funções de banco de dados fixas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpdbfixedrole [ [ @rolename = ] 'role' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @rolename = ] 'role'`É o nome de uma função de banco de dados fixa. *role* é **sysname**, com um padrão de NULL. Se a *função* for especificada, somente as informações sobre essa função serão retornadas; caso contrário, uma lista e uma descrição de todas as funções de banco de dados fixas são retornadas.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**DbFixedRole**|**sysname**|Nome da função de banco de dados fixa.|  
|**Descrição**|**nvarchar (70)**|Descrição de **DbFixedRole.**|  
  
## <a name="remarks"></a>Comentários  
 As funções de banco de dados fixas, conforme mostrado na tabela a seguir, são definidas no nível de banco de dados e possuem permissões para executar atividades administrativas específicas no nível de banco de dados. As funções de banco de dados fixas não podem ser adicionadas ou removidas. As permissões concedidas a uma função de banco de dados fixa não podem ser alteradas.  
  
|Função de banco de dados fixa|Descrição|  
|-------------------------|-----------------|  
|**db_owner**|Proprietários de banco de dados|  
|**db_accessadmin**|Administradores de acesso de banco de dados|  
|**db_securityadmin**|Administradores de segurança de banco de dados|  
|**db_ddladmin**|Administradores DDL de banco de dados|  
|**db_backupoperator**|Operadores de backup de banco de dados|  
|**db_datareader**|Leitores dos dados de banco de dados|  
|**db_datawriter**|Gravadores dos dados de banco de dados|  
|**db_denydatareader**|Leitores de negação dos dados de banco de dados|  
|**db_denydatawriter**|Gravadores de negação dos dados de banco de dados|  
  
 A tabela a seguir mostra os procedimentos armazenados usados para modificar as funções de banco de dados.  
  
|Procedimento armazenado|Ação|  
|----------------------|------------|  
|**sp_addrolemember**|Adiciona um usuário de banco de dados a uma função de banco de dados fixa.|  
|**sp_helprole**|Exibe uma lista dos membros de uma função de banco de dados fixa.|  
|**sp_droprolemember**|Remove um membro de uma função de banco de dados fixa.|  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
 As informações retornadas estão sujeitas a restrições no acesso para metadados. Entidades em que o principal não tem nenhuma permissão não aparecem. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra uma lista de todas as funções de banco de dados fixas.  
  
```  
EXEC sp_helpdbfixedrole;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addrolemember](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dbfixedrolepermission](../../relational-databases/system-stored-procedures/sp-dbfixedrolepermission-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_droprolemember](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helprole](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helprolemember](../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
