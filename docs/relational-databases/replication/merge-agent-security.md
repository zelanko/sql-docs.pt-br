---
title: "Seguran&#231;a do Merge Agent  | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.security.MA.f1"
helpviewer_keywords: 
  - "caixa de diálogo Segurança do Merge Agent"
ms.assetid: 9b86171a-4381-4b39-869a-cdc161e7cd15
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# Seguran&#231;a do Merge Agent 
  A caixa de diálogo **Segurança do Merge Agent** permite especificar a conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows na qual o Merge Agent é executado. O Merge Agent é executado no Distribuidor para assinaturas push e no Assinante para assinaturas pull. A conta do Windows é também referida como *conta do processo*, porque o processo do agente é executado nessa conta. Opções adicionais disponíveis na caixa de diálogo dependem de como você a acessa:  
  
-   Se a caixa de diálogo for acessada do Assistente para Nova Assinatura, também permitirá que você especifique o contexto no qual o Merge Agent fará conexões com o Assinante (para assinaturas push) ou com o Publicador e o Distribuidor (para assinaturas pull). A conexão pode ser feita usando a conta Windows ou no contexto de uma conta [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificada.  
  
-   Se a caixa de diálogo for acessada do **Propriedades de assinatura** caixa de diálogo, especifique o contexto no qual o Merge Agent faz conexões clicando no botão Propriedades (**...**) na **conexão do assinante** ou **conexão do publicador** linha da caixa de diálogo. Para obter mais informações sobre como acessar o **Propriedades de assinatura** caixa de diálogo, consulte [Exibir e modificar propriedades de assinatura Push](../../relational-databases/replication/view-and-modify-push-subscription-properties.md) e como: [Exibir e modificar propriedades de assinatura Pull](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
 Todas as contas devem ser válidas, com a senha correta especificada para cada conta. Contas e senhas não são validadas até que um agente seja executado.  
  
## Opções  
 **Conta do processo**  
 Insira uma conta Windows na qual o Merge Agent é executado.  
  
-   Para assinaturas push, a conta deve:  
  
    -   No mínimo ser um membro do **db_owner** função de banco de dados fixa no banco de dados de distribuição.  
  
    -   Ser um membro da PAL.  
  
    -   Ser um logon associado a um usuário no banco de dados de publicação.  
  
    -   Ter permissões de leitura no compartilhamento de instantâneo.  
  
-   Para assinaturas pull, a conta deve no mínimo ser um membro do **db_owner** função de banco de dados fixa no banco de dados de assinatura.  
  
 Serão requeridas permissões adicionais se a conta do processo for representada quando as conexões forem feitas. Consulte as seções **Conectar ao Publicador e ao Distribuidor** e **Conectar ao Assinante** a seguir.  
  
 **Process Account** não pode ser especificada para assinaturas pull para o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], porque o Merge Agent não é executado em instâncias do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)].  
  
 **Senha** e **Confirmar senha**  
 Insira a senha para a conta do Windows.  
  
 **Conectar ao Publicador e ao Distribuidor**  
 Para assinaturas push, conexões com o Editor e o distribuidor são sempre feitas representando a conta especificada no **conta de processo** caixa de texto.  
  
 Para assinaturas pull, selecione se o Merge Agent deve fazer conexões com o Publicador e o Distribuidor representando a conta especificada na caixa de texto **Conta do processo** ou usando uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se você optar por usar uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , insira um logon e uma senha [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que você selecionar para representar a conta do Windows em vez de usar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta.  
  
 A conta do Windows ou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usada para a conexão deve:  
  
-   Ser um membro da PAL.  
  
-   Ser um logon associado a um usuário no banco de dados de publicação.  
  
-   Ser um logon associado a um usuário no banco de dados de distribuição (o usuário pode ser o usuário Convidado).  
  
-   Ter permissões de leitura no compartilhamento de instantâneo.  
  
 **Conectar ao Assinante**  
 Para assinaturas pull, conexões com o assinante são sempre feitas representando a conta especificada no **conta de processo** caixa de texto.  
  
 Para assinaturas push, selecione se o Merge Agent deve fazer conexões com o Publicador e o Distribuidor representando a conta especificada na caixa de texto **Conta do processo** ou usando uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se você optar por usar uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , insira um logon e uma senha [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  É recomendável a seleção para representar a conta do Windows em vez de usar uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A conta do Windows ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta usada para a conexão com o assinante deve no mínimo ser um membro do **db_owner** função de banco de dados fixa no banco de dados de assinatura.  
  
## Consulte também  
 [Gerenciar logons e senhas na replicação](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Modelo de segurança do agente de replicação](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Visão geral dos agentes de replicação.](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Práticas recomendadas em relação à segurança de replicação](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  
  