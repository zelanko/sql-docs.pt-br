---
title: "Seguran&#231;a do Log Reader Agent  | Microsoft Docs"
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
  - "sql13.rep.security.LRA.f1"
helpviewer_keywords: 
  - "caixa de diálogo Segurança do Log Reader Agent"
ms.assetid: d6981e74-ddb8-41b8-9ea1-56c2ece63b8a
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# Seguran&#231;a do Log Reader Agent 
  O **Log Reader Agent Security** caixa de diálogo permite que você especifique:  
  
-   A conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows na qual o Log Reader Agent é executado no Distribuidor. A conta do Windows é também referida como *conta do processo*, porque o processo do agente é executado nessa conta.  
  
-   O contexto no qual o Log Reader Agent faz conexões com o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador. A conexão pode ser feita representando a conta do Windows ou no contexto de uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificada por você.  
  
    > [!NOTE]  
    >  O Log Reader Agent fará conexões com o Publicador mesmo que o Publicador e o Distribuidor estejam no mesmo computador. O Log Reader Agent também faz conexões com o Distribuidor; essas conexões sempre são feitas representando a conta do Windows na qual o agente é executado.  
  
     Para editores Oracle, especifique o contexto no qual o Log Reader Agent se conecta ao publicador no **Propriedades do publicador** caixa de diálogo (disponível no **Propriedades do distribuidor** caixa de diálogo). Para obter mais informações, consulte [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
 Todas as contas devem ser válidas, com a senha correta especificada para cada conta. Contas e senhas não são validadas até que um agente seja executado.  
  
## Opções  
 **Conta do processo**  
 Insira uma conta do Windows na qual o Log Reader Agent é executado no Distribuidor. A conta do Windows especificada deve ser pelo menos ser membro do **db_owner** função de banco de dados fixa no banco de dados de distribuição.  
  
 **Senha** e **Confirmar senha**  
 Insira a senha para a conta do Windows.  
  
 **Conectar ao Publicador**  
 Selecione se o Log Reader Agent deve fazer conexões com o publicador representando a conta especificada no **conta de processo** caixa de texto ou usando um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta. Se você optar por usar uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , insira um logon e uma senha [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que você selecionar para representar a conta do Windows em vez de usar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta.  
  
 A conta do Windows ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta usada para a conexão deve no mínimo ser um membro do **db_owner** função de banco de dados fixa no banco de dados de publicação.  
  
## Consulte também  
 [Gerenciar logons e senhas na replicação](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Modelo de segurança do agente de replicação](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Visão geral dos agentes de replicação.](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Práticas recomendadas em relação à segurança de replicação](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  