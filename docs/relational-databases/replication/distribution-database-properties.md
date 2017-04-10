---
title: "Propriedades do Banco de Dados de Distribui&#231;&#227;o | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.configdistwizard.distdbproperties.f1"
helpviewer_keywords: 
  - "caixa de diálogo Propriedades do Banco de Dados de Distribuição"
ms.assetid: 0f404ab9-1237-4936-8df5-888baab6a245
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# Propriedades do Banco de Dados de Distribui&#231;&#227;o
  A caixa de diálogo **Propriedades do Banco de Dados de Distribuição** permite a exibição de várias propriedades e a definição do período de retenção da transação e do período de retenção do histórico para o banco de dados.  
  
## Opções  
 **Nome**  
 O nome do banco de dados de distribuição, que assume o padrão “distribuição” (somente leitura).  
  
 **Locais de arquivo**  
 O local do arquivo de banco de dados e do arquivo de log (somente leitura).  
  
 **Período de retenção de transação**  
 Também conhecido como o período de retenção de distribuição. O tempo de armazenamento das transações para replicação transacional. Para obter mais informações, consulte [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
 **Período de retenção de histórico**  
 O período de armazenamento dos metadados de histórico para todos os tipos de replicação.  
  
 **Segurança do Queue Reader Agent**  
 O Queue Reader Agent é usado pela replicação transacional com assinaturas de atualização enfileiradas. Um Agente de Leitor de Fila será criado automaticamente se você selecionar **Publicação transacional com assinaturas de atualização** na página **Tipo de Publicação** do Assistente para Nova Publicação. Clique em **Configurações de Segurança…** para alterar a conta na qual o agente é executado e efetua conexões com o Distribuidor.  
  
 Um Queue Reader Agent também pode ser criado selecionando **criar Queue Reader Agent** nesta página (essa opção será desabilitada se o agente já foi criado).  
  
 Informações de conexão adicionais para o Queue Reader Agent são especificadas em dois lugares:  
  
-   O agente se conecta ao Publicador usando as credenciais especificadas na caixa de diálogo **Propriedades do Publicador** , disponível na página **Publicadores** da caixa de diálogo **Propriedades do Distribuidor** .  
  
-   O agente se conecta ao Assinante usando as credenciais especificadas para o Agente de Distribuição no Assistente para Nova Assinatura.  
  
 Para obter mais informações, consulte  \\[o modelo de segurança do agente de replicação](../Topic/Replication%20Agent%20Security%20Model.md).  
  
## Consulte também  
 [Configurar a distribuição](../../relational-databases/replication/configure-distribution.md)   
 [Criar uma assinatura pull](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [View and Modify Distributor and Publisher Properties](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)  
  
  