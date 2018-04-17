---
title: sp_help_proxy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_proxy
- sp_help_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_proxy
ms.assetid: a2fce164-2b64-40c2-8f35-6eeb7844abf1
caps.latest.revision: 38
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 314eeb6365afafce64ff85aa822e9b2be8c64770
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpproxy-transact-sql"></a>sp_help_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Lista as informações para um ou mais proxies.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_proxy   
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name' ,  
    [ @subsystem_name = ] 'subsystem_name' ,  
    [ @name = ] 'name'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@proxy_id** = ] *id*  
 O número de identificação de proxy do proxy para o qual listar informações. O *proxy_id* é **int**, com um padrão NULL. Ambos o *id* ou *proxy_name* pode ser especificado.  
  
 [ **@proxy_name** =] **'***proxy_name***'**  
 O nome do proxy para o qual listar informações. O *proxy_name* é **sysname**, com um padrão NULL. Ambos o *id* ou *proxy_name* pode ser especificado.  
  
 [ **@subsystem_name** =] '*subsystem_name*'  
 O nome do subsistema para o qual listar proxies. O *subsystem_name* é **sysname**, com um padrão NULL. Quando *subsystem_name* for especificado, *nome* também deve ser especificado.  
  
 A tabela a seguir lista os valores padrão para cada subsistema.  
  
|Value|Description|  
|-----------|-----------------|  
|ActiveScripting|Script do ActiveX|  
|CmdExec|Sistema Operacional (CmdExec)|  
|Instantâneo|Replication Snapshot Agent|  
|LogReader|Replication Agente de Leitor de Log|  
|Distribuição|Agente de distribuição de replicação|  
|Mesclagem|Replication Merge Agent|  
|QueueReader|Replication Queue Reader Agent|  
|ANALYSISQUERY|Comando do Analysis Services|  
|ANALYSISCOMMAND|Consulta do Analysis Services|  
|Dts|Execução do pacote SSIS|  
|PowerShell|Scripts PowerShell|  
  
 [ **@name** =] '*nome*'  
 O nome de um login do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o qual listar proxies. O nome é **nvarchar (256)**, com um padrão NULL. Quando *nome* for especificado, *subsystem_name* também deve ser especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**Int**|Número de identificação de proxy.|  
|**name**|**sysname**|O nome do proxy.|  
|**credential_identity**|**sysname**|O nome de domínio de Microsoft Windows e o nome de usuário para a credencial associada ao proxy.|  
|**Habilitado**|**tinyint**|Se o proxy está habilitado. { **0** = não habilitado, **1** = habilitado}|  
|**Descrição**|**nvarchar(1024)**|A descrição para esse proxy.|  
|**user_sid**|**varbinary(85)**|A identificação de segurança do Windows do usuário do Windows para esse proxy.|  
|**credential_id**|**Int**|O identificador para a credencial associada a esse proxy.|  
|**credential_identity_exists**|**Int**|Especifica se credential_identity existe. {0 = não existe, 1 = existe}|  
  
## <a name="remarks"></a>Remarks  
 Quando nenhum parâmetro for fornecido, **sp_help_proxy** lista informações para todos os proxies na instância.  
  
 Para determinar quais proxies um login podem usar para um determinado subsistema, especifique *nome* e *subsystem_name*. Quando esses argumentos são fornecidos, **sp_help_proxy** lista os proxies que o logon especificado pode acessar e que pode ser usado para o subsistema especificado.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários a função de banco de dados fixa **SQLAgentOperatorRole** no banco de dados **msdb** .  
  
 Para obter detalhes sobre **SQLAgentOperatorRole**, consulte [funções de banco de dados fixa do SQL Server Agent](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
> [!NOTE]  
>  O **credential_identity** e **user_sid** colunas são retornadas apenas no conjunto de resultados quando os membros de **sysadmin** executar esse procedimento armazenado.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-listing-information-for-all-proxies"></a>A. Listando informações para todos os proxies  
 O exemplo a seguir lista as informações para todos os proxies na instância.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_proxy ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-proxy"></a>B. Listando informações para um proxy específico  
 O exemplo a seguir lista as informações para o proxy chamado `Catalog application proxy`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_proxy  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do SQL Server Agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)  
  
  
