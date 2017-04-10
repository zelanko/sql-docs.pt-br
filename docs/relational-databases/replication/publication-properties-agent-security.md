---
title: "Propriedades de Publica&#231;&#227;o, Seguran&#231;a do Agente | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newpubwizard.pubproperties.agentsecurity.f1"
ms.assetid: 03945aac-66f2-4370-b5d1-c1de694bc4c1
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# Propriedades de Publica&#231;&#227;o, Seguran&#231;a do Agente
  A página **Segurança do Agente** da caixa de diálogo **Propriedades de Publicação** permite acessar as configurações das contas nas quais os seguintes agentes executam e fazem conexões com computadores em uma topologia de replicação:  
  
-   O Agente de Instantâneo para todas as publicações.  
  
-   O Agente de Leitor de Log para todas as publicações transacionais. Há um Agente de Leitor de Log para cada banco de dados publicado para replicação transacional. A alteração das configurações do Agente de Leitor de Log afeta todas as publicações transacionais em um banco de dados.  
  
-   O Agente de Leitor de Fila para publicações transacionais, que permite assinaturas de atualização enfileiradas. Há um Agente de Leitor de Fila para cada banco de dados de distribuição. A alteração das configurações do Agente de Leitor de Fila afeta todas as publicações transacionais com assinaturas de atualização em fila que usam o mesmo banco de dados de distribuição. Para obter mais informações sobre configurações de segurança do Queue Reader Agent, consulte [Exibir e modificar as configurações de segurança de replicação](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
 Para obter mais informações sobre configurações de segurança e permissões exigidas para cada agente, consulte [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
## Opções  
 **Configurações de segurança** ou **Criar agente**  
 Se um trabalho de agente tiver sido criado, clique em **as configurações de segurança** para acessar a caixa de diálogo que permite que você altere as configurações de segurança para um agente. Se um trabalho de agente não tiver sido criado, clique em **Criar Agente** para criar um e especificar as configurações de segurança.  
  
## Consulte também  
 [Crie uma publicação](../../relational-databases/replication/publish/create-a-publication.md)   
 [Visualizar e modificar as propriedades da publicação](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Práticas recomendadas em relação à segurança de replicação](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Segurança e proteção e 40; Replicação e 41;](../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  