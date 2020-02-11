---
title: sp_help_proxy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_proxy
- sp_help_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_proxy
ms.assetid: a2fce164-2b64-40c2-8f35-6eeb7844abf1
author: stevestein
ms.author: sstein
ms.openlocfilehash: 904a694d73613bb1c40c671b18ca33e5d9b5d0e6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68085286"
---
# <a name="sp_help_proxy-transact-sql"></a>sp_help_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Lista as informações para um ou mais proxies.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_proxy   
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name' ,  
    [ @subsystem_name = ] 'subsystem_name' ,  
    [ @name = ] 'name'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @proxy_id = ] id`O número de identificação de proxy do proxy para o qual listar informações. O *proxy_id* é **int**, com um padrão de NULL. A *ID* ou a *proxy_name* pode ser especificada.  
  
`[ @proxy_name = ] 'proxy_name'`O nome do proxy para o qual listar informações. O *proxy_name* é **sysname**, com um padrão de NULL. A *ID* ou a *proxy_name* pode ser especificada.  
  
`[ @subsystem_name = ] 'subsystem_name'`O nome do subsistema para o qual listar proxies. O *subsystem_name* é **sysname**, com um padrão de NULL. Quando *subsystem_name* for especificado, o *nome* também deverá ser especificado.  
  
 A tabela a seguir lista os valores padrão para cada subsistema.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|ActiveScripting|Script do ActiveX|  
|CmdExec|Sistema Operacional (CmdExec)|  
|Instantâneo|Replication Snapshot Agent|  
|LogReader|Replication Agente de Leitor de Log|  
|Distribuição|Agente de Distribuição de replicação|  
|Mesclar|Replication Merge Agent|  
|QueueReader|Agente de Leitor de Fila de Replicação|  
|ANALYSISQUERY|Comando do Analysis Services|  
|ANALYSISCOMMAND|Consulta do Analysis Services|  
|Dts|Execução de pacote SSIS|  
|PowerShell|Script do PowerShell|  
  
`[ @name = ] 'name'`O nome de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon para listar proxies para. O nome é **nvarchar (256)**, com um padrão de NULL. Quando *Name* é especificado, *subsystem_name* também deve ser especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|Número de identificação de proxy.|  
|**name**|**sysname**|O nome do proxy.|  
|**credential_identity**|**sysname**|O nome de domínio de Microsoft Windows e o nome de usuário para a credencial associada ao proxy.|  
|**habilitado**|**tinyint**|Se esse proxy está habilitado. { **0** = não habilitado, **1** = habilitado}|  
|**ndescrição**|**nvarchar(1024)**|A descrição para esse proxy.|  
|**user_sid**|**varbinary(85)**|A identificação de segurança do Windows do usuário do Windows para esse proxy.|  
|**credential_id**|**int**|O identificador para a credencial associada a esse proxy.|  
|**credential_identity_exists**|**int**|Especifica se credential_identity existe. {0 = não existe, 1 = existe}|  
  
## <a name="remarks"></a>Comentários  
 Quando nenhum parâmetro é fornecido, **sp_help_proxy** lista informações para todos os proxies na instância.  
  
 Para determinar quais proxies um logon pode usar para um determinado subsistema, especifique *nome* e *subsystem_name*. Quando esses argumentos são fornecidos, **sp_help_proxy** lista os proxies que o logon especificado pode acessar e que podem ser usados para o subsistema especificado.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar esse procedimento armazenado. Deve ser concedida a outros usuários a função de banco de dados fixa **SQLAgentOperatorRole** no banco de dados **msdb** .  
  
 Para obter detalhes sobre **SQLAgentOperatorRole**, consulte [SQL Server Agent funções de banco de dados fixas](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
> [!NOTE]  
>  As colunas **credential_identity** e **user_sid** são retornadas somente no conjunto de resultados quando os membros de **sysadmin** executam esse procedimento armazenado.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-listing-information-for-all-proxies"></a>a. Listando informações para todos os proxies  
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
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Agent procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_add_proxy](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_proxy](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)  
  
  
