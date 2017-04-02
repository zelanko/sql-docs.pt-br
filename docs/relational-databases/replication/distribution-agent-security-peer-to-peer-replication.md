---
title: "Seguran&#231;a do Agente de Distribui&#231;&#227;o (replica&#231;&#227;o ponto a ponto) | Microsoft Docs"
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
  - "sql13.rep.p2pwizard.DA.f1"
ms.assetid: def6bf26-c640-4caf-ad30-05d1e649541d
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# Seguran&#231;a do Agente de Distribui&#231;&#227;o (replica&#231;&#227;o ponto a ponto)
  O **segurança do Distribution Agent** página permite que você especifique as contas sob as quais o Distribution Agent executa e faz conexões com computadores em uma topologia ponto a ponto. Para obter informações sobre permissões requeridas por agentes e práticas recomendadas de segurança de replicação, consulte [modelo de segurança do agente de replicação](../../relational-databases/replication/security/replication-agent-security-model.md) e [práticas recomendadas de segurança de replicação](../../relational-databases/replication/security/replication-security-best-practices.md).  
  
> [!NOTE]  
>  Se o Agente de Distribuição de uma assinatura já foi configurado em uma execução anterior deste assistente, você não poderá alterar as credenciais que ele usa neste assistente. Se você especificar credenciais novas, elas serão ignoradas. Para alterar as credenciais, use o **Propriedades de assinatura** caixa de diálogo. Para obter mais informações, consulte [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
## Opções  
 Clique no botão Propriedades (**...**) na linha para cada assinante para acessar o **segurança do Distribution Agent** caixa de diálogo. Clique em **Ajuda** sobre o **segurança do Distribution Agent** caixa de diálogo que é iniciada para obter mais informações sobre as permissões necessárias para as contas usadas pelos agentes.  
  
 Depois que as configurações forem inseridas em uma das caixas de diálogo, as informações de conexão para o Assinante serão exibidas na grade.  
  
 **Agente para Assinante**  
 O nome de cada computador par.  
  
 **Banco de dados par**  
 O banco de dados no mesmo nível que funciona como um banco de dados de publicação e um banco de dados de assinatura.  
  
 **Conexão com o Distribuidor**  
 O contexto no qual a conexão com o Distribuidor é feita. Conexões locais sempre são feitas usando o contexto da conta do Windows na qual o agente é executado. Este assistente cria assinaturas push (a conexão local é a conexão ao distribuidor), portanto esse campo sempre exibirá: **representar ' \< domínio>\\< logon\>'** ou **representar ' \< computador>\\< logon\>'**.  
  
 **Conexão com o Assinante**  
 O contexto no qual a conexão com o Assinante é feita. A conexão pode ser feita usando o contexto da conta do Windows na qual o agente é executado ou no contexto de um logon no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O campo exibe um dos seguintes: **usar logon ' \< logon>'**, **representar ' \< domínio>\\< logon\>'** ou **representar ' \< computador>\\< logon\>'**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que todas as conexões sejam feitas com o uso do contexto da conta do Windows.  
  
## Consulte também  
 [Administrar uma topologia ponto a ponto e 40; Programação Transact-SQL de replicação e 41;](../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Replicação transacional ponto a ponto](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  