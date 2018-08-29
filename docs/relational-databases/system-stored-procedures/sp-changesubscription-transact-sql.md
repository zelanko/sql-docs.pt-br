---
title: sp_changesubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- changesubscription
- sp_changesubscription
- changesubscription_TSQL
- sp_changesubscription_TSQL
helpviewer_keywords:
- sp_changesubscription
ms.assetid: f9d91fe3-47cf-4915-b6bf-14c9c3d8a029
caps.latest.revision: 40
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 64a34ed640dc9efac57d948475071690ed266d2e
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43023327"
---
# <a name="spchangesubscription-transact-sql"></a>sp_changesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as propriedades de uma assinatura push transacional ou de instantâneo ou uma assinatura pull envolvidas em uma replicação transacional de atualização em fila. Para alterar as propriedades de todos os outros tipos de assinaturas pull, use [sp_change_subscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md). **sp_changesubscription** é executado no publicador do banco de dados de publicação.  
  
> [!IMPORTANT]  
>  Quando um Publicador é configurado com um Distribuidor remoto, os valores fornecidos para todos os parâmetros, inclusive *job_login* e *job_password*, são enviados ao Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changesubscription [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
        , [ @subscriber = ] 'subscriber'  
        , [ @destination_db = ] 'destination_db'  
        , [ @property = ] 'property'  
        , [ @value = ] 'value'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publication**=] **'***publicação***'**  
 É o nome da publicação a ser alterada. *publicação*está **sysname**, sem padrão  
  
 [ **@article** =] **'***artigo***'**  
 É o nome do artigo a ser alterado. *artigo* está **sysname**, sem padrão.  
  
 [ **@subscriber** =] **'***assinante***'**  
 É o nome do Assinante. *assinante* está **sysname**, sem padrão.  
  
 [ **@destination_db** =] **'***destination_db***'**  
 É o nome do banco de dados de assinatura. *destination_db* está **sysname**, sem padrão.  
  
 [  **@property=**] **'***propriedade***'**  
 É a propriedade a ser alterada para a assinatura determinado. *propriedade* está **nvarchar (30)**, e pode ser um dos valores na tabela.  
  
 [  **@value=**] **'***valor***'**  
 É o novo valor especificado *propriedade*. *valor* está **nvarchar (4000)**, e pode ser um dos valores na tabela.  
  
|Propriedade|Valor|Description|  
|--------------|-----------|-----------------|  
|**distrib_job_login**||Logon para a conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows na qual o agente é executado.|  
|**distrib_job_password**||Senha para a conta do Windows na qual o agente é executado.|  
|**subscriber_catalog**||Catálogo a ser usado ao fazer uma conexão com o provedor OLE DB. Essa propriedade só é válida para não -[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes.|  
|**subscriber_datasource**||Nome da fonte de dados conforme entendido pelo provedor OLE DB. *Essa propriedade só é válida para não -* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *assinantes.*|  
|**subscriber_location**||Local do banco de dados conforme entendido pelo provedor OLE DB. *Essa propriedade só é válida para não -* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *assinantes.*|  
|**subscriber_login**||Nome de logon no Assinante.|  
|**subscriber_password**||Senha forte para o logon fornecido.|  
|**subscriber_security_mode**|**1**|Use a Autenticação do Windows ao se conectar ao Assinante.|  
||**0**|Use Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao se conectar ao Assinante.|  
|**subscriber_provider**||PROGID (identificador programático) exclusivo com o qual o provedor OLE DB para fonte de dados não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é registrado. *Essa propriedade só é válida para não -* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *assinantes.*|  
|**subscriber_providerstring**||Cadeia de conexão específica de provedor OLE DB que identifica a fonte de dados. *Essa propriedade só é válida para não -* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *assinantes.*|  
|**fluxos de assinatura**||É o número de conexões permitido por Agente de Distribuição para aplicar lotes de alterações em paralelo a um Assinante. Um intervalo de valores de **1** à **64** há suporte para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicadores. Esta propriedade deve ser **0** para não -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes, Publicadores Oracle ou assinaturas ponto a ponto.|  
|**subscriber_type**|**1**|Servidor de fontes de dados ODBC|  
||**3**|Provedor OLE DB|  
|**memory_optimized**|**bit**|Indica que a assinatura dá suporte a tabelas com otimização de memória. *memory_optimized* está **bit**, onde 1 é igual a true (a assinatura dá suporte a tabelas com otimização de memória).|  
  
 [  **@publisher =** ] **'***publisher***'**  
 Especifica um Publicador que não é do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *Publisher* está **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  *Publisher* não deve ser especificado para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_changesubscription** é usado em replicação de instantâneo e transacional.  
  
 **sp_changesubscription** só pode ser usado para modificar as propriedades de assinaturas push ou pull envolvidas em replicação transacional de atualização enfileirada. Para alterar as propriedades de todos os outros tipos de assinaturas pull, use [sp_change_subscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md).  
  
 Depois de alterar o logon ou a senha de um agente, você deve parar e reiniciar o agente antes que as alterações entrem em vigor.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_changesubscription**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)  
  
  
