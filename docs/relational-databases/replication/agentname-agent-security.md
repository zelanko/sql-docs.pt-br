---
title: "Seguran&#231;a do Agente &lt;Nome_do_Agente&gt; | Microsoft Docs"
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
  - "sql13.rep.newsubwizard.agentnameagentsecurity.f1"
ms.assetid: d34c7ef8-cf77-4ffd-887f-3c4214dfd71e
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# Seguran&#231;a do Agente &lt;Nome_do_Agente&gt;
  O **\< Nome_do_agente> segurança do agente** página permite que você especifique as contas nas quais o Distribution Agent (para replicação transacional e de instantâneo) ou o agente de mesclagem (para replicação de mesclagem) executam e fazem conexões com computadores em uma topologia de replicação. Para obter informações sobre permissões requeridas por agentes e práticas recomendadas de segurança de replicação, consulte [modelo de segurança do agente de replicação](../../relational-databases/replication/security/replication-agent-security-model.md) e [práticas recomendadas de segurança de replicação](../../relational-databases/replication/security/replication-security-best-practices.md).  
  
## Opções  
 Clique no botão Propriedades (**...**) na linha para cada assinante para acessar o **segurança do Distribution Agent** ou **segurança do Merge Agent** caixa de diálogo. Clique em **Ajuda** na caixa de diálogo que é iniciada para obter mais informações sobre as permissões requeridas para contas usadas pelos agentes.  
  
 Depois que as configurações forem inseridas em uma das caixas de diálogo, as informações de conexão para o Assinante serão exibidas na grade.  
  
 **Agente para Assinante**  
 O nome de cada Assinante.  
  
 **Conexão com o Distribuidor**  
 Exibido para replicação de instantâneo e transacional. O contexto no qual a conexão com o Distribuidor é feita. Conexões locais sempre são feitas usando o contexto de conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows no qual o agente executa:  
  
-   Para assinaturas push, a conexão local é a conexão com o distribuidor, portanto esse campo sempre exibirá: **representar ' \< domínio>\\< logon\>'** ou **representar ' \< computador>\\< logon\>'** para assinaturas push.  
  
-   Para assinaturas pull, a conexão pode ser feita também no contexto de um logon [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O campo exibe um dos seguintes: **usar logon ' \< logon>'**, **representar ' \< domínio>\\< logon\>'** ou **representar ' \< computador>\\< logon\>'**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que todas as conexões sejam feitas com o uso do contexto da conta do Windows.  
  
 **Conexão com o Publicador e Distribuidor**  
 Exibido para replicação de mesclagem. O contexto no qual as conexões com o Publicador e o Distribuidor são feitas. Conexões locais sempre são feitas usando o contexto da conta do Windows na qual o agente é executado:  
  
-   Para assinaturas push, a conexão local é a conexão com o Editor e distribuidor, portanto esse campo sempre exibirá: **representar ' \< domínio>\\< logon\>'** ou **representar ' \< computador>\\< logon\>'** para assinaturas push.  
  
-   Para assinaturas pull, a conexão pode ser feita também no contexto de um logon [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O campo exibe um dos seguintes: **usar logon ' \< logon>'**, **representar ' \< domínio>\\< logon\>'** ou **representar ' \< computador>\\< logon\>'**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que todas as conexões sejam feitas com o uso do contexto da conta do Windows.  
  
 **Conexão com o Assinante**  
 O contexto no qual a conexão com o Assinante é feita. Conexões locais sempre são feitas usando o contexto da conta do Windows na qual o agente é executado:  
  
-   Para assinaturas pull, a conexão local é a conexão com o assinante, portanto esse campo sempre exibirá: **representar ' \< domínio>\\< logon\>'** ou **representar ' \< computador>\\< logon\>'** para assinaturas push.  
  
-   Para assinaturas push, a conexão pode ser feita também no contexto de um logon [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O campo exibe um dos seguintes: **usar logon ' \< logon>'**, **representar ' \< domínio>\\< logon\>'** ou **representar ' \< computador>\\< logon\>'**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que todas as conexões sejam feitas com o uso do contexto da conta do Windows.  
  
## Consulte também  
 [Exibir e modificar propriedades de assinatura pull](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [View and Modify Push Subscription Properties](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [Gerenciar logons e senhas na replicação](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Modelo de segurança do agente de replicação](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Segurança e proteção e 40; Replicação e 41;](../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  