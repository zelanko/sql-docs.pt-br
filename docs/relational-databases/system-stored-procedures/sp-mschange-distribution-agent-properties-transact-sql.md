---
title: sp_MSchange_distribution_agent_properties (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_MSchange_distribution_agent_properties
- sp_MSchange_distribution_agent_properties_TSQL
helpviewer_keywords: sp_MSchange_distribution_agent_properties
ms.assetid: 7dac5e68-bf84-433a-a531-66921f35126f
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0a08ef7bb0fbbfcdfffd676c63bc2f1396fed4e5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spmschangedistributionagentproperties-transact-sql"></a>sp_MSchange_distribution_agent_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as propriedades de um trabalho do Distribution Agent que é executado em um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou versão posterior do distribuidor. Esse procedimento armazenado é usado para alterar propriedades quando o Publicador é executado em uma instância do [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. Esse procedimento armazenado é executado no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@publisher**  =] **'***publicador***'**  
 É o nome do Publicador. *publicador* é **sysname**, sem padrão.  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 É o nome do banco de dados de publicação. *publisher_db* é **sysname**, sem padrão.  
  
 [  **@publication =** ] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, sem padrão.  
  
 [  **@subscriber=** ] **'***assinante***'**  
 É o nome do Assinante. *assinante* é **sysname**, sem padrão.  
  
 [  **@subscriber_db=** ] **'***subscriber_db***'**  
 É o nome do banco de dados de assinatura. *subscriber_db* é **sysname**, sem padrão.  
  
 [  **@property =** ] **'***propriedade***'**  
 É a propriedade da publicação a ser alterada. *propriedade* é **sysname**, sem padrão.  
  
 [  **@value =** ] **'***valor***'**  
 É o novo valor da propriedade. *valor* é **nvarchar (524)**, com um padrão NULL.  
  
 Esta tabela descreve as propriedades do trabalho do Agente de Distribuição que podem ser alteradas e restrições nos valores dessas propriedades.  
  
|Propriedade|Valor|Description|  
|--------------|-----------|-----------------|  
|**distrib_job_login**||Logon para a conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows na qual o agente é executado.|  
|**distrib_job_password**||Senha para a conta do Windows na qual o trabalho do agente é executado.|  
|**subscriber_catalog**||Catálogo a ser usado ao fazer uma conexão com o provedor OLE DB. *Essa propriedade só é válida para não -* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *assinantes.*|  
|**subscriber_datasource**||Nome da fonte de dados conforme entendido pelo provedor OLE DB. *Essa propriedade só é válida para não -* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *assinantes.*|  
|**subscriber_location**||Local do banco de dados conforme entendido pelo provedor OLE DB. *Essa propriedade só é válida para não -* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *assinantes.*|  
|**subscriber_login**||Logon a ser usado na conexão com um Assinante para sincronizar a assinatura.|  
|**subscriber_password**||Senha do assinante.<br /><br /> [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]|  
|**subscriber_provider**||PROGID (identificador programático) exclusivo com o qual o provedor OLE DB para fonte de dados não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é registrado. *Essa propriedade só é válida para não -* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *assinantes.*|  
|**subscriber_providerstring**||Cadeia de conexão específica de provedor OLE DB que identifica a fonte de dados. *Essa propriedade só é válida para assinantes não SQL Server.*|  
|**subscriber_security_mode**|**1**|Autenticação do Windows.<br /><br /> [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]|  
||**0**|Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**subscriber_type**|**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Assinante|  
||**1**|Servidor de fontes de dados ODBC|  
||**3**|Provedor OLE DB|  
|**fluxos de assinatura**||Denota o número de conexões permitido pelo Agente de Distribuição para aplicar lotes de alterações em paralelo a um Assinante. *Não há suportada para não -* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *assinantes, Publicadores Oracle ou assinaturas ponto a ponto.*|  
  
> [!NOTE]  
>  Depois de alterar o logon ou a senha de um agente, você deve parar e reiniciar o agente antes que as alterações entrem em vigor.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_MSchange_distribution_agent_properties** é usado em replicação de instantâneo e replicação transacional.  
  
 Quando o publicador é executado em uma instância do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou versão posterior, você deve usar [sp_changesubscription](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md) para alterar as propriedades de um trabalho do agente de mesclagem que sincroniza uma assinatura push executa no distribuidor.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** pode executar a função de servidor fixa no distribuidor **sp_MSchange_distribution_agent_properties**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_addpushsubscription_agent &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)   
 [sp_addsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)  
  
  
