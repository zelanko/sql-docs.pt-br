---
title: sp_changemergesubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changemergesubscription_TSQL
- sp_changemergesubscription
helpviewer_keywords:
- sp_changemergesubscription
ms.assetid: fd820f35-c189-4e2d-884d-b60c1c469f58
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3b37e09147652e856ac0c4c8160c1d7d3caf6f6d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62993117"
---
# <a name="spchangemergesubscription-transact-sql"></a>sp_changemergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as propriedades selecionadas de uma assinatura push de mesclagem. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
> [!IMPORTANT]  
>  Quando um Publicador é configurado com um Distribuidor remoto, os valores fornecidos para todos os parâmetros, inclusive *job_login* e *job_password*, são enviados ao Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changemergesubscription [ [ @publication= ] 'publication' ]  
    [ , [ @subscriber= ] 'subscriber'  
    [ , [ @subscriber_db= ] 'subscriber_db' ]  
    [ , [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação a ser alterada. *publicação* está **sysname**, com um padrão NULL. A publicação já deve existir e ser adequada às regras para identificadores.  
  
`[ @subscriber = ] 'subscriber'` É o nome do assinante. *assinante* está **sysname**, com um padrão NULL.  
  
`[ @subscriber_db = ] 'subscriber_db'` É o nome do banco de dados de assinatura. *subscriber_db*está **sysname**, com um padrão NULL.  
  
`[ @property = ] 'property'` É a propriedade a ser alterada para a publicação determinada. *propriedade* está **sysname**, e pode ser um dos valores na tabela.  
  
`[ @value = ] 'value'` É o novo valor especificado *propriedade*. *valor* está **nvarchar (255)**, e pode ser um dos valores na tabela.  
  
|Propriedade|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**description**||Descrição da assinatura de mesclagem.|  
|**priority**||É a prioridade da assinatura. A prioridade é usada pelo resolvedor padrão para escolher um vencedor quando são detectados conflitos.|  
|**merge_job_login**||Logon para a conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows na qual o agente é executado.|  
|**merge_job_password**||Senha para a conta do Windows na qual o agente é executado.|  
|**publisher_security_mode**|**1**|Use a Autenticação do Windows ao se conectar ao Publicador.|  
||**0**|Use a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao se conectar ao Publicador.|  
|**publisher_login**||Nome de logon no Publicador.|  
|**publisher_password**||Senha forte para o logon do Publicador fornecido.|  
|**subscriber_security_mode**|**1**|Use a Autenticação do Windows ao se conectar ao Assinante.|  
||**0**|Use Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao se conectar ao Assinante.|  
|**subscriber_login**||Nome de logon no Assinante.|  
|**subscriber_password**||Senha forte para o logon de Assinante fornecido.|  
|**sync_type**|**automatic**|Esquema e dados iniciais de tabelas publicadas são transferidos ao Assinante primeiro.|  
||**None**|O Assinante já tem o esquema e os dados iniciais para as tabelas publicadas; tabelas de sistema e dados são sempre transferidos.|  
|**use_interactive_resolver**|**true**|Permite resolver conflitos interativamente para todos os artigos que permitem resolução interativa.|  
||**false**|Conflitos são resolvidos automaticamente usando um resolvedor padrão ou resolvedor personalizado.|  
|NULL (padrão)|NULL (padrão)||  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_changemergesubscription** é usado em replicação de mesclagem.  
  
 Depois de alterar o logon ou a senha de um agente, você deve parar e reiniciar o agente antes que as alterações entrem em vigor.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_changemergesubscription**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_addmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [sp_helpmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
