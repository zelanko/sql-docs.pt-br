---
title: sp_help_publication_access (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_help_publication_access
- sp_help_publication_access_TSQL
helpviewer_keywords:
- sp_help_publication_access
ms.assetid: 9408fa13-54a0-4cb1-8fb0-845e5536ef50
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1d1afcb1e5419e2ddd028440e1ece57f36bb3269
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47818218"
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
 É o nome da publicação a ser acessada. *publicação* está **sysname**, sem padrão.  
  
 [  **@return_granted=**] **'***return_granted***'**  
 É a ID do logon. *return_granted* está **bit**, com um padrão de 1. Se **0** for especificado e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação é usada, os logons disponíveis que aparecem no publicador, mas não no distribuidor serão retornados. Se **0** for especificado e a autenticação do Windows é usada, os logons que não foram especificamente negados acessam em um publicador ou distribuidor serão retornados.  
  
 [  **@login=**] **'***logon***'**  
 É a ID do logon de segurança padrão. *login* está **sysname**, com um padrão de **%**.  
  
 [  **@initial_list =**] *initial_list*  
 Especifica se devem ou não ser retornados todos os membros com acesso à publicação ou apenas aqueles que tinham acesso antes que novos membros fossem adicionados à lista. *initial_list* é bit, com um padrão de **0**.  
  
 **1** retorna informações para todos os membros de **sysadmin** a função de servidor fixa com logons válidos no distribuidor que existiu quando a publicação foi criada, bem como o logon atual.  
  
 **0** retorna informações para todos os membros de **sysadmin** a função de servidor fixa com logons válidos no distribuidor que existiu quando a publicação foi criada, bem como todos os usuários na lista de acesso da publicação que não pertencer à **sysadmin** função de servidor fixa.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**LoginName**|**nvarchar(256)**|Nome de logon atual.|  
|**isntname**|**int**|**0** = logon não é um usuário do Windows.<br /><br /> **1** = logon é um usuário do Windows.|  
|**isntgroup**|**int**|**0** = logon não é um grupo do Windows.<br /><br /> **1** = logon é um grupo do Windows.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_help_publication_access** é usado em todos os tipos de replicação.  
  
 Quando ambos **Isntname** e **Isntgroup** no resultado do conjunto são **0**, supõe-se que o logon é um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou o **db_owner** banco de dados fixa podem executar **sp_help_publication_access**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_grant_publication_access &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql.md)   
 [sp_revoke_publication_access &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-publication-access-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
