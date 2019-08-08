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
ms.openlocfilehash: a47a81b2b19ceccf76a031e298ab60cf4a6f8c9a
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770947"
---
# <a name="sp_helpdistpublisher-transact-sql"></a>sp_helpdistpublisher (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Retorna propriedades de Publicadores usando um Distribuidor. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpdistpublisher [ [ @publisher=] 'publisher']   
    [ , [ @check_user = ] check_user  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'`É o Publicador para o qual as propriedades são retornadas. o Publicador é **sysname**, com um **%** padrão de.  
  
`[ @check_user = ] check_user` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome de Publicador.|  
|**distribution_db**|**sysname**|Banco de dados de distribuição do Publicador especificado.|  
|**security_mode**|**int**|Modo de segurança usado pelos agentes de replicação ao se conectar ao Publicador para assinaturas de atualização enfileirada ou com um Editor não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> **0**  =  autenticação[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> **1** = autenticação do Windows|  
|**login**|**sysname**|Nome de logon usado pelos agentes de replicação ao se conectar ao Publicador para assinaturas de atualização enfileirada ou com um Editor não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**password**|**nvarchar(524)**|Senha retornada (em formulário criptografado simples). A senha é nula para usuários que não sejam **sysadmin**.|  
|**activo**|**bit**|Se um Publicador remoto está usando o servidor local como um Distribuidor:<br /><br /> **0** = Não<br /><br /> **1** = Sim|  
|**working_directory**|**nvarchar(255)**|Nome do diretório de trabalho.|  
|**confiável**|**bit**|Se a senha é necessária quando o Publicador se conecta com o Distribuidor. Para [!INCLUDE[msCoName](../../includes/msconame-md.md)] o[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores, isso sempre deve retornar **0**, o que significa que a senha é necessária.|  
|**thirdparty_flag**|**bit**|Se a publicação está habilitada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou por um aplicativo de terceiro:<br /><br /> **0, Oracle ou** = Publicador de gateway Oracle.[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> **1** = o Publicador foi integrado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao uso de um aplicativo de terceiros.|  
|**publisher_type**|**sysname**|Tipo de Publicador, que pode ser um dos seguintes:<br /><br /> **MSSQLSERVER**<br /><br /> **ORACLE**<br /><br /> **GATEWAY ORACLE**|  
|**publisher_data_source**|**nvarchar(4000)**|Nome da fonte de dados OLE DB no Publicador.|  
|**storage_connection_string**|**nvarchar(4000)**|Chave de acesso de armazenamento para o diretório de trabalho quando o distribuidor ou Publicador no banco de dados SQL do Azure.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpdistpublisher** é usado em todos os tipos de replicação.  
  
 o **sp_helpdistpublisher** não exibirá o logon ou a senha do Publicador no conjunto de resultados para logons não-**sysadmin** .  
  
## <a name="permissions"></a>Permissões  
 Os membros da função de servidor fixa **sysadmin** podem executar **Sp_helpdistpublisher** para qualquer Publicador usando o servidor local como distribuidor. Os membros da função de banco de dados fixa **db_owner** ou a função **replmonitor** em um banco de dados de distribuição podem executar **sp_helpdistpublisher** para qualquer Publicador que use esse banco de dados de distribuição. Os usuários na lista de acesso à publicação de uma publicação no *Publicador* especificado podem executar **sp_helpdistpublisher**. Se o Publicador não for especificado, as informações serão retornadas para todos os Publicadores aos quais o usuário tem direitos de acesso.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar propriedades de Publicador e Distribuidor](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_changedistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)  
  
  
