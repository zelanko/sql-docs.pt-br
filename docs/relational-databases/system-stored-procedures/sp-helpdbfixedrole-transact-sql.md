---
title: sp_helpdbfixedrole (Transact-SQL) | Microsoft Docs
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
- sp_helpdbfixedrole
- sp_helpdbfixedrole_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_helpdbfixedrole
ms.assetid: ad87e9a0-b901-4e37-9950-aa517d680fc3
caps.latest.revision: "24"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3d42fd08cb784ff13433bc906c19cbbeb04c18c3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpdbfixedrole-transact-sql"></a>sp_helpdbfixedrole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma lista das funções de banco de dados fixas.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpdbfixedrole [ [ @rolename = ] 'role' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@rolename =** ] **'***função***'**  
 É o nome de uma função de banco de dados fixa. *função* é **sysname**, com um padrão NULL. Se *função* for especificado, serão retornadas somente as informações sobre essa função; caso contrário, uma lista e descrição de todas as funções de banco de dados fixa é retornado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**DbFixedRole**|**sysname**|Nome da função de banco de dados fixa.|  
|**Description**|**nvarchar (70)**|Descrição do **DbFixedRole.**|  
  
## <a name="remarks"></a>Comentários  
 As funções de banco de dados fixas, conforme mostrado na tabela a seguir, são definidas no nível de banco de dados e possuem permissões para executar atividades administrativas específicas no nível de banco de dados. As funções de banco de dados fixas não podem ser adicionadas ou removidas. As permissões concedidas a uma função de banco de dados fixa não podem ser alteradas.  
  
|Função de banco de dados fixa|Description|  
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
  
## <a name="see-also"></a>Consulte também  
 [Segurança armazenados procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_dbfixedrolepermission &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dbfixedrolepermission-transact-sql.md)   
 [sp_droprolemember &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [sp_helprole &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [sp_helprolemember &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
