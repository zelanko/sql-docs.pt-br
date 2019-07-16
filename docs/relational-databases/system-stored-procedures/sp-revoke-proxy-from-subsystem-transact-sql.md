---
title: sp_revoke_proxy_from_subsystem (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_revoke_login_from_subsystem
- sp_revoke_login_from_subsystem_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_revoke_proxy_from_subsystem
ms.assetid: b87bc8ba-3ea8-4aed-b54b-32c3d82d9d2a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 8901c46c5654b6c633e03d62e8eaec2a3e903e02
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022274"
---
# <a name="sprevokeproxyfromsubsystem-transact-sql"></a>sp_revoke_proxy_from_subsystem (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Revoga o acesso a um subsistema de um proxy.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_revoke_proxy_from_subsystem   
    [ @proxy_id = ] proxy_id,  
    [ @proxy_name = ] 'proxy_name',  
    [ @subsystem_id = ] subsystem_id,  
    [ @subsystem_name = ] 'subsystem_name'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @proxy_id = ] id` O número de identificação de proxy do proxy acesso será revogado. O *proxy_id* é **int**, com um padrão NULL. Qualquer um dos *proxy_id* ou *proxy_name* deve ser especificado, mas não podem ser especificados.  
  
`[ @proxy_name = ] 'proxy_name'` O nome do proxy acesso será revogado. O *proxy_name* é **sysname**, com um padrão NULL. Qualquer um dos *proxy_id* ou *proxy_name* deve ser especificado, mas não podem ser especificados.  
  
`[ @subsystem_id = ] id` O número de identificação do subsistema para revogar o acesso para o. O *subsystem_id* é **int**, com um padrão NULL. Qualquer um dos *subsystem_id* ou *subsystem_name* deve ser especificado, mas não podem ser especificados. A tabela a seguir lista os valores padrão para cada subsistema.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**2**|Script do ActiveX<br /><br /> **\*\* Importante \* \***  será removido do subsistema ActiveX Scripting [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent em uma versão futura do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam.|  
|**3**|Sistema Operacional (CmdExec)|  
|**4**|Replication Snapshot Agent|  
|**5**|Replication Agente de Leitor de Log|  
|**6**|Agente de Distribuição de Replicação|  
|**7**|Replication Merge Agent|  
|**8**|Agente de Leitor de Fila de Replicação|  
|**9**|Comando do Analysis Services|  
|**10**|Consulta do Analysis Services|  
|**11**|[!INCLUDE[ssIS](../../includes/ssis-md.md)] execução de pacotes|  
|**12**|Scripts PowerShell|  
  
`[ @subsystem_name = ] 'subsystem_name'` O nome do subsistema para revogar o acesso para o. O *subsystem_name* é **sysname**, com um padrão NULL. Qualquer um dos *subsystem_id* ou *subsystem_name* deve ser especificado, mas não podem ser especificados. A tabela a seguir lista os valores padrão para cada subsistema.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|ActiveScripting|Script do ActiveX|  
|CmdExec|Sistema Operacional (CmdExec)|  
|Instantâneo|Replication Snapshot Agent|  
|LogReader|Replication Agente de Leitor de Log|  
|Distribuição|Agente de Distribuição de Replicação|  
|Mesclagem|Replication Merge Agent|  
|QueueReader|Agente de Leitor de Fila de Replicação|  
|ANALYSISQUERY|Comando do Analysis Services|  
|ANALYSISCOMMAND|Consulta do Analysis Services|  
|Dts|[!INCLUDE[ssIS](../../includes/ssis-md.md)] execução de pacotes|  
|PowerShell|Scripts PowerShell|  
  
## <a name="remarks"></a>Comentários  
 A revogação de acesso a um subsistema não altera as permissões para o principal especificado no proxy.  
  
> [!NOTE]  
>  Para determinar quais etapas de trabalho fazem referência a um proxy, clique com botão direito do **Proxies** nó sob **SQL Server Agent** no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e, em seguida, clique em **propriedades**. No **propriedades da conta Proxy** caixa de diálogo, selecione o **referências** página para exibir todas as etapas de trabalho que fazem referência a esse proxy.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** pode executar a função de servidor fixa **sp_revoke_proxy_from_subsystem**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir revoga acesso ao subsistema [!INCLUDE[ssIS](../../includes/ssis-md.md)] para o proxy `Catalog application proxy`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_revoke_proxy_from_subsystem  
    @proxy_name = 'Catalog application proxy',  
    @subsystem_name = N'Dts';  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do SQL Server Agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [Implementar a segurança do SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md)   
 [sp_grant_proxy_to_subsystem &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-proxy-to-subsystem-transact-sql.md)  
  
  
