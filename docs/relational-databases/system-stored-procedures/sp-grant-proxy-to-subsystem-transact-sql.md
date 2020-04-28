---
title: sp_grant_proxy_to_subsystem (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_grant_login_to_subsystem_TSQL
- sp_grant_login_to_subsystem
dev_langs:
- TSQL
helpviewer_keywords:
- sp_grant_proxy_to_subsystem
ms.assetid: 866aaa27-a1e0-453a-9b1b-af39431ad9c2
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 96e044b94244492202058d6dc2b2f048a9c1db6c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68123817"
---
# <a name="sp_grant_proxy_to_subsystem-transact-sql"></a>sp_grant_proxy_to_subsystem (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Concede um acesso de proxy a um subsistema.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_grant_proxy_to_subsystem  
     { [ @proxy_id = ] proxy_id | [ @proxy_name = ] 'proxy_name' },  
     { [ @subsystem_id = ] subsystem_id | [ @subsystem_name = ] 'subsystem_name' }  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @proxy_id = ] id`O número de identificação de proxy do proxy para o qual conceder acesso. O *proxy_id* é **int**, com um padrão de NULL. *Proxy_id* ou *proxy_name* deve ser especificado, mas ambos não podem ser especificados.  
  
`[ @proxy_name = ] 'proxy_name'`O nome do proxy para o qual conceder acesso. O *proxy_name* é **sysname**, com um padrão de NULL. *Proxy_id* ou *proxy_name* deve ser especificado, mas ambos não podem ser especificados.  
  
`[ @subsystem_id = ] id`O número de ID do subsistema ao qual conceder acesso. O *subsystem_id* é **int**, com um padrão de NULL. *Subsystem_id* ou *subsystem_name* deve ser especificado, mas ambos não podem ser especificados. A tabela a seguir lista os valores padrão para cada subsistema.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**2**|[!INCLUDE[msCoName](../../includes/msconame-md.md)]Script do ActiveX<br /><br /> ** \* Importante \* \* ** O subsistema de script do ActiveX será removido do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent em uma versão futura do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam.|  
|**3**|Sistema Operacional (**CmdExec**)|  
|**4**|Replication Snapshot Agent|  
|**5**|Replication Agente de Leitor de Log|  
|**6**|Agente de Distribuição de Replicação|  
|**7**|Replication Merge Agent|  
|**8**|Agente de Leitor de Fila de Replicação|  
|**9**|Consulta do Analysis Services|  
|**10**|Comando do Analysis Services|  
|**11**|[!INCLUDE[ssIS](../../includes/ssis-md.md)] execução de pacotes|  
|**12**|Scripts PowerShell|  
| &nbsp; | &nbsp; |
  
`[ @subsystem_name = ] 'subsystem_name'`O nome do subsistema ao qual conceder acesso. O **subsystem_name** é **sysname**, com um padrão de NULL. *Subsystem_id* ou *subsystem_name* deve ser especificado, mas ambos não podem ser especificados. A tabela a seguir lista os valores padrão para cada subsistema.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**ActiveScripting**|Script do ActiveX|  
|**CmdExec**|Sistema Operacional (**CmdExec**)|  
|**Instantâneo**|Replication Snapshot Agent|  
|**LogReader**|Replication Agente de Leitor de Log|  
|**Distribuição**|Agente de Distribuição de replicação|  
|**Mescle**|Replication Merge Agent|  
|**QueueReader**|Agente de Leitor de Fila de Replicação|  
|**ANALYSISQUERY**|Consulta do Analysis Services|  
|**ANALYSISCOMMAND**|Comando do Analysis Services|  
|**Dts**|Execução do pacote SSIS|  
|**PowerShell**|Scripts PowerShell|  
| &nbsp; | &nbsp; |
  
## <a name="remarks"></a>Comentários  
 O ato de conceder um acesso de proxy a um subsistema não altera as permissões para a entidade especificada no proxy.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_grant_proxy_to_subsystem**.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-granting-access-to-a-subsystem-by-id"></a>a. Concedendo acesso a um subsistema pela ID  
 O exemplo a seguir concede o acesso de proxy `Catalog application proxy` ao subsistema ActiveX Scripting.  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_grant_proxy_to_subsystem  
    @proxy_name = 'Catalog application proxy',  
    @subsystem_id = 2;  
GO  
```  
  
### <a name="b-granting-access-to-a-subsystem-by-name"></a>B. Concedendo acesso a um subsistema pelo nome  
 O exemplo a seguir concede ao `Catalog application proxy` do proxy acesso ao subsistema de execução de pacote SSIS.  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_grant_proxy_to_subsystem  
    @proxy_name = N'Catalog application proxy',  
    @subsystem_name = N'Dts' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Implementar segurança de SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md)   
 [&#41;&#40;Transact-SQL de sp_revoke_proxy_from_subsystem](../../relational-databases/system-stored-procedures/sp-revoke-proxy-from-subsystem-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_add_proxy](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_proxy](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_update_proxy](../../relational-databases/system-stored-procedures/sp-update-proxy-transact-sql.md)  
  
  
