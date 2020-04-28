---
title: sp_changesubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- changesubscription
- sp_changesubscription
- changesubscription_TSQL
- sp_changesubscription_TSQL
helpviewer_keywords:
- sp_changesubscription
ms.assetid: f9d91fe3-47cf-4915-b6bf-14c9c3d8a029
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5684d80bc63fe543e54aa4c38d9f0a516b6334ff
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68770674"
---
# <a name="sp_changesubscription-transact-sql"></a>sp_changesubscription (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Altera as propriedades de uma assinatura push transacional ou de instantâneo ou uma assinatura pull envolvidas em uma replicação transacional de atualização em fila. Para alterar as propriedades de todos os outros tipos de assinaturas pull, use [sp_change_subscription_properties &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md). **sp_changesubscription** é executado no Publicador do banco de dados de publicação.  
  
> [!IMPORTANT]  
>  Quando um Publicador é configurado com um Distribuidor remoto, os valores fornecidos para todos os parâmetros, inclusive *job_login* e *job_password*, são enviados ao Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @publication = ] 'publication'`É o nome da publicação a ser alterada. a *publicação*é **sysname**, sem padrão  
  
`[ @article = ] 'article'`É o nome do artigo a ser alterado. o *artigo* é **sysname**, sem padrão.  
  
`[ @subscriber = ] 'subscriber'`É o nome do Assinante. o *assinante* é **sysname**, sem padrão.  
  
`[ @destination_db = ] 'destination_db'`É o nome do banco de dados de assinatura. *destination_db* é **sysname**, sem padrão.  
  
`[ @property = ] 'property'`É a propriedade a ser alterada para a assinatura fornecida. a *Propriedade* é **nvarchar (30)** e pode ser um dos valores na tabela.  
  
`[ @value = ] 'value'`É o novo valor para a *Propriedade*especificada. o *valor* é **nvarchar (4000)** e pode ser um dos valores na tabela.  
  
|Propriedade|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**distrib_job_login**||Logon para a conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows na qual o agente é executado.|  
|**distrib_job_password**||Senha para a conta do Windows na qual o agente é executado.|  
|**subscriber_catalog**||Catálogo a ser usado ao fazer uma conexão com o provedor OLE DB. Esta propriedade só é válida para[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes não.|  
|**subscriber_datasource**||Nome da fonte de dados conforme entendido pelo provedor OLE DB. *Esta propriedade só é válida para* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *assinantes não.*|  
|**subscriber_location**||Local do banco de dados conforme entendido pelo provedor OLE DB. *Esta propriedade só é válida para* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *assinantes não.*|  
|**subscriber_login**||Nome de logon no Assinante.|  
|**subscriber_password**||Senha forte para o logon fornecido.|  
|**subscriber_security_mode**|**1**|Use a Autenticação do Windows ao se conectar ao Assinante.|  
||**0**|Use Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao se conectar ao Assinante.|  
|**subscriber_provider**||PROGID (identificador programático) exclusivo com o qual o provedor OLE DB para fonte de dados não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é registrado. *Esta propriedade só é válida para* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *assinantes não.*|  
|**subscriber_providerstring**||Cadeia de conexão específica de provedor OLE DB que identifica a fonte de dados. *Esta propriedade só é válida para* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *assinantes não.*|  
|**SubscriptionStreams**||É o número de conexões permitido por Agente de Distribuição para aplicar lotes de alterações em paralelo a um Assinante. Há suporte para um intervalo de valores de **1** a **64** para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicadores. Essa propriedade deve ser **0** para[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes não, Publicadores Oracle ou assinaturas ponto a ponto.|  
|**subscriber_type**|**1**|Servidor de fontes de dados ODBC|  
||**3**|Provedor OLE DB|  
|**memory_optimized**|**bit**|Indica que a assinatura dá suporte a tabelas com otimização de memória. *memory_optimized* é **bit**, em que 1 é igual a true (a assinatura dá suporte a tabelas com otimização de memória).|  
  
`[ @publisher = ] 'publisher'`Especifica um não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador. o *Publicador* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  o *Publicador* não deve ser especificado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para um Publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_changesubscription** é usado em instantâneo e replicação transacional.  
  
 **sp_changesubscription** só pode ser usada para modificar as propriedades de assinaturas push ou assinaturas pull envolvidas na replicação transacional de atualização enfileirada. Para alterar as propriedades de todos os outros tipos de assinaturas pull, use [sp_change_subscription_properties &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md).  
  
 Depois de alterar o logon ou a senha de um agente, você deve parar e reiniciar o agente antes que as alterações entrem em vigor.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_changesubscription**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropsubscription](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)  
  
  
