---
title: sp_MSchange_distribution_agent_properties (T-SQL)
description: Descreve o sp_MSchange_distribution_agent_properties procedimento armazenado usado para alterar as propriedades do Agente de Distribuição para uma topologia de Replicação do SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_MSchange_distribution_agent_properties
- sp_MSchange_distribution_agent_properties_TSQL
helpviewer_keywords:
- sp_MSchange_distribution_agent_properties
ms.assetid: 7dac5e68-bf84-433a-a531-66921f35126f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1a2e2e3c0074c3fcc53298c2556c786c9b7057db
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75322249"
---
# <a name="sp_mschange_distribution_agent_properties-transact-sql"></a>sp_MSchange_distribution_agent_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as propriedades de um trabalho agente de distribuição executado em um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] distribuidor de versão ou posterior. Esse procedimento armazenado é usado para alterar propriedades quando o Publicador é executado em uma instância do [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. Esse procedimento armazenado é executado no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_MSchange_distribution_agent_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
        , [ @subscriber = ] 'subscriber'   
        , [ @subscriber_db = ] 'subscriber_db'   
        , [ @property = ] 'property'   
        , [ @value = ] 'value' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'`É o nome do Publicador. o *Publicador* é **sysname**, sem padrão.  
  
`[ @publisher_db = ] 'publisher_db'`É o nome do banco de dados de publicação. *publisher_db* é **sysname**, sem padrão.  
  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @subscriber = ] 'subscriber'`É o nome do Assinante. o *assinante* é **sysname**, sem padrão.  
  
`[ @subscriber_db = ] 'subscriber_db'`É o nome do banco de dados de assinatura. *subscriber_db* é **sysname**, sem padrão.  
  
`[ @property = ] 'property'`É a propriedade de publicação a ser alterada. a *Propriedade* é **sysname**, sem padrão.  
  
`[ @value = ] 'value'`É o novo valor da propriedade. o *valor* é **nvarchar (524)**, com um padrão de NULL.  
  
 Esta tabela descreve as propriedades do trabalho do Agente de Distribuição que podem ser alteradas e restrições nos valores dessas propriedades.  
  
|Propriedade|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**distrib_job_login**||Logon para a conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows na qual o agente é executado.|  
|**distrib_job_password**||Senha para a conta do Windows na qual o trabalho do agente é executado.|  
|**subscriber_catalog**||Catálogo a ser usado ao fazer uma conexão com o provedor OLE DB. *Esta propriedade só é válida para* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *assinantes não.*|  
|**subscriber_datasource**||Nome da fonte de dados conforme entendido pelo provedor OLE DB. *Esta propriedade só é válida para* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *assinantes não.*|  
|**subscriber_location**||Local do banco de dados conforme entendido pelo provedor OLE DB. *Esta propriedade só é válida para* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *assinantes não.*|  
|**subscriber_login**||Logon a ser usado na conexão com um Assinante para sincronizar a assinatura.|  
|**subscriber_password**||Senha do assinante.<br /><br /> [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]|  
|**subscriber_provider**||PROGID (identificador programático) exclusivo com o qual o provedor OLE DB para fonte de dados não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é registrado. *Esta propriedade só é válida para* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *assinantes não.*|  
|**subscriber_providerstring**||Cadeia de conexão específica de provedor OLE DB que identifica a fonte de dados. *Essa propriedade só é válida para Assinantes não SQL Server.*|  
|**subscriber_security_mode**|**1**|Autenticação do Windows.<br /><br /> [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]|  
||**0**|Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**subscriber_type**|**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Farão|  
||**1**|Servidor de fontes de dados ODBC|  
||**3**|Provedor OLE DB|  
|**SubscriptionStreams**||Denota o número de conexões permitido pelo Agente de Distribuição para aplicar lotes de alterações em paralelo a um Assinante. *Sem suporte para* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *assinantes não, Publicadores Oracle ou assinaturas ponto a ponto.*|  
  
> [!NOTE]  
>  Depois de alterar o logon ou a senha de um agente, você deve parar e reiniciar o agente antes que as alterações entrem em vigor.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_MSchange_distribution_agent_properties** é usado na replicação de instantâneo e na replicação transacional.  
  
 Quando o Publicador é executado em uma [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] instância do ou versão posterior, você deve usar [sp_changesubscription](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md) para alterar as propriedades de um trabalho de agente de mesclagem que sincroniza uma assinatura push que é executada no distribuidor.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** no distribuidor podem executar **sp_MSchange_distribution_agent_properties**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)  
  
  
