---
title: sp_help_publication_access (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_help_publication_access
- sp_help_publication_access_TSQL
helpviewer_keywords:
- sp_help_publication_access
ms.assetid: 9408fa13-54a0-4cb1-8fb0-845e5536ef50
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2b9fb4ee142f179c4570fb24516a891e41045fd8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sphelppublicationaccess-transact-sql"></a>sp_help_publication_access (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma lista de todos os logons concedidos para uma publicação. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_publication_access [ @publication = ] 'publication'  
    [ , [ @return_granted = ] 'return_granted' ]   
    [ , [ @login = ] 'login' ]  
    [ , [ @initial_list = ] initial_list ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'***publicação***'**  
 É o nome da publicação a ser acessada. *publicação* é **sysname**, sem padrão.  
  
 [  **@return_granted=**] **'***return_granted***'**  
 É a ID do logon. *return_granted* é **bit**, com um padrão de 1. Se **0** for especificado e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação é usada, os logons disponíveis que aparecem no publicador mas não no distribuidor serão retornados. Se **0** é especificado e autenticação do Windows é usada, os logons que não foram especificamente negados acessarem em um editor ou distribuidor serão retornados.  
  
 [  **@login=**] **'***login***'**  
 É a ID do logon de segurança padrão. *logon* é **sysname**, com um padrão de **%**.  
  
 [  **@initial_list =**] *initial_list*  
 Especifica se devem ou não ser retornados todos os membros com acesso à publicação ou apenas aqueles que tinham acesso antes que novos membros fossem adicionados à lista. *initial_list* é bit, com um padrão de **0**.  
  
 **1** retorna informações de todos os membros de **sysadmin** a função de servidor fixa com logons válidos no distribuidor que existiu quando a publicação foi criada, bem como o logon atual.  
  
 **0** retorna informações de todos os membros de **sysadmin** a função de servidor fixa com logons válidos no distribuidor que existiu quando a publicação foi criada, bem como todos os usuários na lista de acesso da publicação que não pertence ao **sysadmin** função de servidor fixa.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**LoginName**|**nvarchar(256)**|Nome de logon atual.|  
|**Isntname**|**Int**|**0** = logon não é um usuário do Windows.<br /><br /> **1** = logon é um usuário do Windows.|  
|**Isntgroup**|**Int**|**0** = logon não é um grupo do Windows.<br /><br /> **1** = logon é um grupo do Windows.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_help_publication_access** é usado em todos os tipos de replicação.  
  
 Quando ambos **Isntname** e **Isntgroup** no resultado do conjunto são **0**, presume-se que o logon é um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_help_publication_access**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_grant_publication_access &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql.md)   
 [sp_revoke_publication_access &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-publication-access-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
