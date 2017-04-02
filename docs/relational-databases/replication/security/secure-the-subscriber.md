---
title: "Proteger o Assinante | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "assinaturas [replicação do SQL Server], segurança"
  - "Assinantes [replicação do SQL Server], segurança"
  - "segurança [replicação do SQL Server], Assinantes"
ms.assetid: c8f0d62a-8b5d-4a21-9aec-223da52bb708
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# Proteger o Assinante
  Agentes de mesclagem e agentes de distribuição que conectam ao assinante. Essas conexões podem ser feitas no contexto de um logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou de um logon do Windows. É importante fornecer um logon adequado para cada um desses agentes e seguir o princípio de conceder o mínimo possível de direitos, e, também proteger o armazenamento de todas as senhas. Para obter informações sobre as permissões necessárias para cada agente, consulte [modelo de segurança do agente de replicação](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
## Agente de Distribuição  
 Há um Agente de Distribuição por assinatura (um agente independente, o padrão para publicações criadas no Assistente para Nova Publicação) ou um Agente de Distribuição por par composto por banco de dados de publicação e banco de dados de assinatura (um agente compartilhado). T  
  
 Para especificar informações de conexão para assinaturas push, consulte [criar uma assinatura Push](../../../relational-databases/replication/create-a-push-subscription.md).  
  
 Para especificar informações de conexão para assinaturas pull, consulte [criar uma inscrição de recepção](../../../relational-databases/replication/create-a-pull-subscription.md)  
  
## Merge Agent  
 Cada assinatura de mesclagem possui seu próprio Agente de Mesclagem que se conecta e atualiza ambos, o Publicador e o Assinante.  
  
 Para especificar informações de conexão para assinaturas push, consulte [criar uma assinatura Push](../../../relational-databases/replication/create-a-push-subscription.md).  
  
 Para especificar informações de conexão para assinaturas pull, consulte [criar uma assinatura Pull](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
## Assinaturas de atualização imediata  
 Quando configurar uma assinatura de atualização imediata, especifique uma conta no Assinante na qual as conexões com o Publicador são realizadas. Conexões são usadas pelos gatilhos acionados no Assinante e que propagam as alterações no Publicador. Há três opções disponíveis para o tipo de conexão:  
  
-   Um servidor vinculado que a replicação cria; a conexão é feita com as credenciais que você especifica durante a configuração.  
  
-   Um servidor vinculado que a replicação cria; a conexão é feita com as credenciais do usuário que faz a alteração no Assinante.  
  
-   Um servidor vinculado ou remoto que você já definiu.  
  
> [!IMPORTANT]  
>  Para especificar informações de conexão, use o procedimento armazenado [sp_link_publication & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md). Você também pode usar o **logon para assinaturas atualizáveis** página do Assistente de assinatura novo chama **sp_link_publication**. Em certas condições, esse procedimento armazenado pode falhar se o Assinante estiver executando o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Service Pack 1(SP1) ou versão posterior e o Publicador estiver executando uma versão anterior. Se o procedimento armazenado falhar nesse cenário, atualize o Publicador para o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] SP1 ou posterior.  
  
 Para obter mais informações, consulte [criar uma assinatura atualizável em uma publicação transacional](../../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md) e [Exibir e modificar as configurações de segurança de replicação](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
> [!IMPORTANT]  
>  A conta especificada para a conexão só deve receber permissão para inserir, atualizar e excluir dados nas exibições criadas pela replicação no banco de dados de publicação; nenhuma permissão adicional será dada. Conceder permissões de exibições no banco de dados que são nomeadas no formato **syncobj _***\< Número_hexadecimal>* para a conta configurada em cada assinante.  
  
## Assinaturas de atualização em fila  
 Quando você configurar assinatura de atualização em fila, há duas áreas a considerar relacionadas a segurança:  
  
-   Há só um Agente de Leitor de Fila para cada Distribuidor. Recomenda-se que para cada Distribuidor, você configure, no máximo uma publicação que esteja habilitada para assinaturas de atualização em fila.  
  
-   O agente do Queue Reader faz conexões com o Distribuidor, Publicador e cada Assinante:  
  
    -   A conta na qual o agente executa e faz as conexões para o Distribuidor é especificada quando você criar o agente (se usar o Assistente para Nova Publicação, o agente é criado quando você criar uma publicação habilitada para assinaturas de atualização ).  
  
    -   A conta na qual o agente faz as conexões com o Publicador é especificada quando você configura a distribuição para o Publicador. Especifique a conta de Windows na qual o agente executará ou uma conta [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
    -   A conta na qual o agente faz conexões com o Assinante é especificada quando você cria a assinatura.  
  
    > [!IMPORTANT]  
    >  Use a Autenticação [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para conexões com os Assinantes e especifique uma conta diferente para a conexão com cada Assinante. Se usar uma assinatura pull, a replicação sempre define a conexão a ser usada com a Autenticação do Windows (em assinaturas pull, a replicação não pode acessar metadados no Assinante com a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]). Nesse caso, altere a conexão para usar a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] depois que a assinatura for configurada.  
  
     Para obter mais informações, consulte como: criar uma assinatura de atualização para uma publicação transacional (SQL Server Management Studio) e [Exibir e modificar as configurações de segurança de replicação](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
## Consulte também  
 [Habilitar conexões criptografadas para o mecanismo de banco de dados e 40; SQL Server Configuration Manager & 41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)   
 [Práticas recomendadas em relação à segurança de replicação](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Segurança e proteção e 40; Replicação e 41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  