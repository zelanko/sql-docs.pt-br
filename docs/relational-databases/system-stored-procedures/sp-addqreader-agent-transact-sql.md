---
title: sp_addqreader_agent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addqreader_agent_TSQL
- sp_addqreader_agent
helpviewer_keywords:
- sp_addqreader_agent
ms.assetid: dc9f591a-e67e-4ba8-bf47-defd5eda0822
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1758f6cd269c911ea582577721d29e6534910e91
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85716452"
---
# <a name="sp_addqreader_agent-transact-sql"></a>sp_addqreader_agent (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Adiciona um Queue Reader Agent para um determinado Distribuidor. Esse procedimento armazenado é executado no Distribuidor, no banco de dados de distribuição, ou no Publicador, no banco de dados de publicação.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addqreader_agent [ @job_login = ] 'job_login'  
        , [ @job_password = ] 'job_password'  
    [ , [ @job_name = ] 'job_name'  
    [ , [ @frompublisher = ] frompublisher   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_login = ] 'job_login'`É o logon da [!INCLUDE[msCoName](../../includes/msconame-md.md)] conta do Windows na qual o agente é executado. *job_login* é **nvarchar (257)**, sem padrão. Essa conta do Windows sempre é usada para conexões de agente com o Distribuidor.  
  
`[ @job_password = ] 'job_password'`É a senha para a conta do Windows na qual o agente é executado. *job_password* é **sysname**, sem padrão.  
  
> [!IMPORTANT]  
>  Não armazene informações de autenticação em arquivos de script. Para melhor segurança, nomes de logon e senhas devem ser fornecidos em runtime.  
  
`[ @job_name = ] 'job_name'`É o nome de um trabalho de agente existente. *job_name* é **sysname**, com um valor padrão de NULL. Esse parâmetro só é especificado quando o agente é criado usando um trabalho existente em vez de um trabalho recém-criado (o padrão).  
  
`[ @frompublisher = ] frompublisher`Especifica se o procedimento está sendo executado no Publicador. *frompublisher* é bit, com um valor padrão de **0**. Um valor de **1** significa que o procedimento está sendo executado do Publicador no banco de dados de publicação.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addqreader_agent** é usado na replicação transacional.  
  
 **sp_addqreader_agent** deve ser executado pelo menos uma vez em um distribuidor que dá suporte à atualização em fila após [sp_adddistributiondb](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md) , mas antes de [sp_addpublication](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md).  
  
 O trabalho de Queue Reader Agent é removido quando você executa o [sp_dropdistributiondb](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_addqreader_agent**.  
  
## <a name="see-also"></a>Consulte Também  
 [Habilitar atualização de assinaturas para publicações transacionais](../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)   
 [Atualizar scripts de replicação &#40;Programação Transact-SQL de replicação&#41;](../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)   
 [Assinaturas atualizáveis para replicação transacional](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [&#41;&#40;Transact-SQL de sp_changeqreader_agent](../../relational-databases/system-stored-procedures/sp-changeqreader-agent-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpqreader_agent](../../relational-databases/system-stored-procedures/sp-helpqreader-agent-transact-sql.md)  
  
  
