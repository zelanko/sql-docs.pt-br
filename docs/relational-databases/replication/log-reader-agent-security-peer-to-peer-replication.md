---
title: "Seguran&#231;a do Agente de Leitor de Log (replica&#231;&#227;o ponto a ponto) | Microsoft Docs"
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
  - "sql13.rep.p2pwizard.LRA.f1"
ms.assetid: 6575e2a8-16bb-449c-bdca-4a4202d0972f
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# Seguran&#231;a do Agente de Leitor de Log (replica&#231;&#227;o ponto a ponto)
  O **Log Reader Agent Security** página permite que você especifique as contas sob a qual o Log Reader Agent em cada ponto executa e faz conexões. Para obter informações sobre permissões requeridas por agentes e práticas recomendadas de segurança de replicação, consulte [modelo de segurança do agente de replicação](../../relational-databases/replication/security/replication-agent-security-model.md) e [práticas recomendadas de segurança de replicação](../../relational-databases/replication/security/replication-security-best-practices.md).  
  
> [!NOTE]  
>  Há um Agente de Leitor de Log para cada banco de dados publicado que usa a replicação transacional. Se o Agente de Leitor de Log de um banco de dados já foi configurado (para uma publicação em uma execução anterior desse assistente ou para outra publicação transacional no mesmo banco de dados), você não poderá trocar as credenciais que ele usa nesse assistente. Se você especificar credenciais novas, elas serão ignoradas. Para alterar as credenciais, use o **Propriedades de publicação** caixa de diálogo. Para obter mais informações, consulte [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
## Opções  
 Clique no botão Propriedades (**...**) na linha para cada ponto acessar o **Log Reader Agent Security** caixa de diálogo. Clique em **Ajuda** sobre o **segurança do Log Reader Agent** caixa de diálogo que é iniciada para obter mais informações sobre as permissões necessárias para as contas usadas pelos agentes.  
  
 Depois que as configurações forem inseridas na caixa de diálogo, serão exibidas informações de conexão para o Assinante na grade.  
  
 **Agentes para o Publicador**  
 O nome de cada instância de servidor de computador par.  
  
 **Banco de dados par**  
 O banco de dados que serve como banco de dados de publicação e banco de dados de assinatura em cada nível.  
  
 **Conexão com o Distribuidor**  
 O contexto no qual a conexão com o Distribuidor é feita. A conexão com o distribuidor local sempre é feita usando o contexto do [!INCLUDE[msCoName](../../includes/msconame-md.md)] conta do Windows sob a qual o agente é executado, portanto esse campo sempre exibirá **representar ' \< domínio>\\< logon\>'** ou **representar ' \< computador>\\< logon\>'**.  
  
 **Conexão com o Publicador**  
 O contexto no qual a conexão com o Publicador é feita. A conexão com o publicador pode ser feita usando um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon ou usando o contexto da conta do Windows sob a qual o agente é executado. O campo exibe um dos seguintes: **usar logon ' \< logon>'**, **representar ' \< domínio>\\< logon\>'** ou **representar ' \< computador>\\< logon\>'**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que todas as conexões sejam feitas com o uso do contexto da conta do Windows.  
  
## Consulte também  
 [Administrar uma topologia ponto a ponto e 40; Programação Transact-SQL de replicação e 41;](../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Replicação transacional ponto a ponto](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  