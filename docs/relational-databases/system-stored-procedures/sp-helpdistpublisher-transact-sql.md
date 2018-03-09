---
title: sp_helpdistpublisher (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helpdistpublisher_TSQL
- sp_helpdistpublisher
helpviewer_keywords:
- sp_helpdistpublisher
ms.assetid: f207c22d-8fb2-4756-8a9d-6c51d6cd3470
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e01aca1558894f52f575aba642cd4079c22f21f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpdistpublisher-transact-sql"></a>sp_helpdistpublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna propriedades de Publicadores usando um Distribuidor. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpdistpublisher [ [ @publisher=] 'publisher']   
    [ , [ @check_user = ] check_user  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher=** ] **'***publicador***'**  
 É o Publicador para o qual as propriedades são retornadas. *publicador* é **sysname**, com um padrão de  **%** .  
  
 [  **@check_user=** ] *check_user*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome de Publicador.|  
|**distribution_db**|**sysname**|Banco de dados de distribuição do Publicador especificado.|  
|**security_mode**|**int**|Modo de segurança usado pelos agentes de replicação ao se conectar ao Publicador para assinaturas de atualização enfileirada ou com um Editor não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação<br /><br /> **1** = autenticação do Windows|  
|**logon**|**sysname**|Nome de logon usado pelos agentes de replicação ao se conectar ao Publicador para assinaturas de atualização enfileirada ou com um Editor não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**senha**|**nvarchar (524)**|Senha retornada (em formulário criptografado simples). Senha é diferente de NULL para usuários **sysadmin**.|  
|**ativo**|**bit**|Se um Publicador remoto está usando o servidor local como um Distribuidor:<br /><br /> **0** = não<br /><br /> **1** = Sim|  
|**working_directory**|**nvarchar(255)**|Nome do diretório de trabalho.|  
|**confiável**|**bit**|Se a senha é necessária quando o Publicador se conecta com o Distribuidor. Para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores, isso deve retornar sempre **0**, que significa que a senha é necessária.|  
|**thirdparty_flag**|**bit**|Se a publicação está habilitada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou por um aplicativo de terceiro:<br /><br /> **0** = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], oracle ou editor Oracle Gateway.<br /><br /> **1** = publicador foi integrado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um aplicativo de terceiros.|  
|**publisher_type**|**sysname**|Tipo de Publicador, que pode ser um dos seguintes:<br /><br /> **MSSQLSERVER**<br /><br /> **ORACLE**<br /><br /> **ORACLE GATEWAY**|  
|**publisher_data_source**|**nvarchar(4000)**|Nome da fonte de dados OLE DB no Publicador.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpdistpublisher** é usado em todos os tipos de replicação.  
  
 **sp_helpdistpublisher** não exibirá o logon do publicador ou senha no resultado definido para não -**sysadmin** logons.  
  
## <a name="permissions"></a>Permissões  
 Membros de **sysadmin** pode executar a função de servidor fixa **sp_helpdistpublisher** por qualquer publicador usando o servidor local como um distribuidor. Membros do **db_owner** função de banco de dados fixa ou **replmonitor** função em um banco de dados de distribuição pode executar **sp_helpdistpublisher** por qualquer publicador usando banco de dados de distribuição. Lista de usuários no acesso à publicação para uma publicação no local especificado *publicador* podem executar **sp_helpdistpublisher**. Se *publicador* não for especificado, informações são retornadas para todos os publicadores que o usuário tem direitos de acesso.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar propriedades de Publicador e Distribuidor](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_changedistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)  
  
  
