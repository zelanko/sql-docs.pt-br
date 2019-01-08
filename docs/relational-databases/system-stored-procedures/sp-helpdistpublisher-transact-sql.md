---
title: sp_helpdistpublisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdistpublisher_TSQL
- sp_helpdistpublisher
helpviewer_keywords:
- sp_helpdistpublisher
ms.assetid: f207c22d-8fb2-4756-8a9d-6c51d6cd3470
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 85a6eaf76497b1fa763047a255cdb7784316541e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52802738"
---
# <a name="sphelpdistpublisher-transact-sql"></a>sp_helpdistpublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna propriedades de Publicadores usando um Distribuidor. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpdistpublisher [ [ @publisher=] 'publisher']   
    [ , [ @check_user = ] check_user  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher=** ] **'***publisher***'**  
 É o Publicador para o qual as propriedades são retornadas. *Publisher* está **sysname**, com um padrão de **%**.  
  
 [  **@check_user=** ] *check_user*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome de Publicador.|  
|**distribution_db**|**sysname**|Banco de dados de distribuição do Publicador especificado.|  
|**security_mode**|**int**|Modo de segurança usado pelos agentes de replicação ao se conectar ao Publicador para assinaturas de atualização enfileirada ou com um Editor não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação<br /><br /> **1** = autenticação do Windows|  
|**login**|**sysname**|Nome de logon usado pelos agentes de replicação ao se conectar ao Publicador para assinaturas de atualização enfileirada ou com um Editor não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**password**|**nvarchar(524)**|Senha retornada (em formulário criptografado simples). Senha é diferente de NULL para usuários **sysadmin**.|  
|**Active Directory**|**bit**|Se um Publicador remoto está usando o servidor local como um Distribuidor:<br /><br /> **0** = Não<br /><br /> **1** = Sim|  
|**working_directory**|**nvarchar(255)**|Nome do diretório de trabalho.|  
|**confiável**|**bit**|Se a senha é necessária quando o Publicador se conecta com o Distribuidor. Para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e em versões posteriores, isso deve retornar sempre **0**, que significa que a senha é necessária.|  
|**thirdparty_flag**|**bit**|Se a publicação está habilitada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou por um aplicativo de terceiro:<br /><br /> **0** = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], oracle ou editor Oracle Gateway.<br /><br /> **1** = publicador foi integrado com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um aplicativo de terceiros.|  
|**publisher_type**|**sysname**|Tipo de Publicador, que pode ser um dos seguintes:<br /><br /> **MSSQLSERVER**<br /><br /> **ORACLE**<br /><br /> **ORACLE GATEWAY**|  
|**publisher_data_source**|**nvarchar(4000)**|Nome da fonte de dados OLE DB no Publicador.|  
|**storage_connection_string**|**nvarchar(4000)**|Chave de acesso de armazenamento para o diretório de trabalho ao distribuidor ou publicador no banco de dados SQL.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpdistpublisher** é usado em todos os tipos de replicação.  
  
 **sp_helpdistpublisher** não exibirá o logon do publicador ou a senha no resultado definida para não -**sysadmin** logons.  
  
## <a name="permissions"></a>Permissões  
 Os membros de **sysadmin** pode ser executada a função de servidor fixa **sp_helpdistpublisher** por qualquer publicador usando o servidor local como um distribuidor. Os membros a **db_owner** função de banco de dados fixa ou o **replmonitor** função em um banco de dados de distribuição pode executar **sp_helpdistpublisher** por qualquer publicador usando o que banco de dados de distribuição. Listam de usuários no acesso à publicação para uma publicação no especificado *publisher* pode ser executada **sp_helpdistpublisher**. Se *publicador* não for especificado, informações serão retornadas para todos os publicadores que o usuário tem direitos de acesso.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar propriedades de Publicador e Distribuidor](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_changedistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)  
  
  
