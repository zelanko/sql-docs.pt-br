---
title: "Seguran&#231;a do Agente de Leitor de Fila | Microsoft Docs"
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
  - "sql13.rep.security.QRA.f1"
helpviewer_keywords: 
  - "caixa de diálogo Segurança do Agente de Leitor de Fila"
ms.assetid: 77938da0-2afd-4455-8826-f4a6a9440cb3
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# Seguran&#231;a do Agente de Leitor de Fila
  O **segurança do Queue Reader Agent** caixa de diálogo permite que você especifique o [!INCLUDE[msCoName](../../includes/msconame-md.md)] conta do Windows sob a qual o Queue Reader Agent é executado e faz conexões locais ao distribuidor. O agente se conecta ao publicador usando a conta especificada no **Propriedades do publicador** caixa de diálogo (disponível no **Propriedades do distribuidor** caixa de diálogo); o agente se conecta ao assinante usando o mesmo contexto que o agente de distribuição para a assinatura. Para obter mais informações, consulte [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
 A conta deve ser válida, com a senha correta especificada. Contas e senhas não são validadas até que um agente seja executado.  
  
## Opções  
 **Conta do processo**  
 Insira uma conta do Windows na qual o Agente de Leitor de Fila seja executado no Distribuidor. A conta do Windows especificada deve ser pelo menos ser membro do **db_owner** função de banco de dados fixa no banco de dados de distribuição.  
  
 **Senha** e **Confirmar senha**  
 Insira a senha para a conta do Windows.  
  
## Consulte também  
 [Gerenciar logons e senhas na replicação](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Modelo de segurança do agente de replicação](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Visão geral dos agentes de replicação.](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Práticas recomendadas em relação à segurança de replicação](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  