---
title: Proteger o assinante | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [SQL Server replication], security
- Subscribers [SQL Server replication], security
- security [SQL Server replication], Subscribers
ms.assetid: c8f0d62a-8b5d-4a21-9aec-223da52bb708
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a9914246135350540b0155e61905d1e548a033fa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68051871"
---
# <a name="secure-the-subscriber"></a>Proteger o Assinante
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Agentes de mesclagem e agentes de distribuição que conectam ao assinante. Essas conexões podem ser feitas no contexto de um logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou de um logon do Windows. É importante fornecer um logon adequado para cada um desses agentes e seguir o princípio de conceder o mínimo possível de direitos, e, também proteger o armazenamento de todas as senhas. Para obter informações sobre as permissões exigidas para cada agente, consulte [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
## <a name="distribution-agent"></a>Agente de Distribuição  
 Há um Agente de Distribuição por assinatura (um agente independente, o padrão para publicações criadas no Assistente para Nova Publicação) ou um Agente de Distribuição por par composto por banco de dados de publicação e banco de dados de assinatura (um agente compartilhado). T  
  
 Para especificar informações de conexão para assinaturas push, consulte [Criar uma assinatura push](../../../relational-databases/replication/create-a-push-subscription.md).  
  
 Para especificar informações de conexão para assinaturas pull, consulte [Criar uma assinatura pull](../../../relational-databases/replication/create-a-pull-subscription.md)  
  
## <a name="merge-agent"></a>Merge Agent  
 Cada assinatura de mesclagem possui seu próprio Agente de Mesclagem que se conecta e atualiza ambos, o Publicador e o Assinante.  
  
 Para especificar informações de conexão para assinaturas push, consulte [Criar uma assinatura push](../../../relational-databases/replication/create-a-push-subscription.md).  
  
 Para especificar informações de conexão para assinaturas pull, consulte [Criar uma assinatura pull](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
## <a name="immediate-updating-subscriptions"></a>Assinaturas de atualização imediata  
 Quando configurar uma assinatura de atualização imediata, especifique uma conta no Assinante na qual as conexões com o Publicador são realizadas. Conexões são usadas pelos gatilhos acionados no Assinante e que propagam as alterações no Publicador. Há três opções disponíveis para o tipo de conexão:  
  
-   Um servidor vinculado que a replicação cria; a conexão é feita com as credenciais que você especifica durante a configuração.  
  
-   Um servidor vinculado que a replicação cria; a conexão é feita com as credenciais do usuário que faz a alteração no Assinante.  
  
-   Um servidor vinculado ou remoto que você já definiu.  
  
> [!IMPORTANT]  
>  Para especificar as informações de conexão, use o procedimento armazenado [sp_link_publication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md). Você também pode usar a página **Logon para Assinaturas Atualizáveis** do Assistente para Nova Assinatura, chamada **sp_link_publication**. Em certas condições, esse procedimento armazenado pode falhar se o Assinante estiver executando o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Service Pack 1(SP1) ou versão posterior e o Publicador estiver executando uma versão anterior. Se o procedimento armazenado falhar nesse cenário, atualize o Publicador para o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] SP1 ou posterior.  
  
 Para obter mais informações, consulte [Criar uma assinatura atualizável em uma publicação transacional](../../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md) e [Exibir e modificar as configurações de segurança de replicação](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
> [!IMPORTANT]  
>  A conta especificada para a conexão só deve receber permissão para inserir, atualizar e excluir dados nas exibições criadas pela replicação no banco de dados de publicação; nenhuma permissão adicional será dada. Conceda permissões para exibições no banco de dados de publicação que são nomeadas no formato **syncobj_***\<HexadecimalNumber>* para a conta configurada em cada Assinante.  
  
## <a name="queued-updating-subscriptions"></a>Assinaturas de atualização em fila  
 Quando você configurar assinatura de atualização em fila, há duas áreas a considerar relacionadas a segurança:  
  
-   Há só um Agente de Leitor de Fila para cada Distribuidor. Recomenda-se que para cada Distribuidor, você configure, no máximo uma publicação que esteja habilitada para assinaturas de atualização em fila.  
  
-   O agente do Queue Reader faz conexões com o Distribuidor, Publicador e cada Assinante:  
  
    -   A conta na qual o agente executa e faz as conexões para o Distribuidor é especificada quando você criar o agente (se usar o Assistente para Nova Publicação, o agente é criado quando você criar uma publicação habilitada para assinaturas de atualização ).  
  
    -   A conta na qual o agente faz as conexões com o Publicador é especificada quando você configura a distribuição para o Publicador. Especifique a conta de Windows na qual o agente executará ou uma conta [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
    -   A conta na qual o agente faz conexões com o Assinante é especificada quando você cria a assinatura.  
  
    > [!IMPORTANT]  
    >  Use a Autenticação [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para conexões com os Assinantes e especifique uma conta diferente para a conexão com cada Assinante. Se usar uma assinatura pull, a replicação sempre define a conexão a ser usada com a Autenticação do Windows (em assinaturas pull, a replicação não pode acessar metadados no Assinante com a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ). Nesse caso, altere a conexão para usar a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] depois que a assinatura for configurada.  
  
     Para obter mais informações, confira Como criar uma assinatura de atualização a uma publicação transacional (SQL Server Management Studio) e [Exibir e modificar as configurações de segurança de replicação](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)   
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Segurança e proteção &#40;Replicação&#41;](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  
