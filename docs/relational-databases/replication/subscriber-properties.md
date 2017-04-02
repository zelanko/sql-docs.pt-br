---
title: "Propriedades do Assinante | Microsoft Docs"
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
  - "sql13.rep.configdistwizard.subscribers.f1"
helpviewer_keywords: 
  - "caixa de diálogo Propriedades do Assinante"
ms.assetid: 32aa0347-64e4-4aa4-ac57-6bd3e5d52070
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# Propriedades do Assinante
  O **Propriedades do assinante** caixa de diálogo contém informações relevantes para os assinantes que executam versões do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
## Opções  
 **Conexão do Agente com o Assinante**  
 O contexto no qual o Agente de Distribuição e o Agente de Mesclagem se conectam do Distribuidor ao Assinante. Isso só se aplica a versões anteriores do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 Selecione **Representar conta de processo do agente** para efetuar conexões com o Assinante usando o contexto de conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no Distribuidor ou especifique **Autenticação do SQL Server**e insira um valor para **Logon** e **Senha**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que você selecione **Representar conta de processo do agente**.  
  
 Para o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores, as informações de conexão são especificadas para cada assinatura no Assistente para Nova Assinatura e pode ser alterada na caixa de diálogo **Propriedades da Assinatura** .  
  
 **Agendamentos Padrão de Agente**  
 O agendamento padrão usado no novo Assistente de assinatura para os assinantes que executam versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
 **Diversos**  
 Inclui informações sobre o Assinante e o tipo de Assinante.  
  
## Consulte também  
 [View and Modify Distributor and Publisher Properties](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Referência de propriedades de & #40. Replicação e 41;](../../relational-databases/replication/properties-reference-replication.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  
  