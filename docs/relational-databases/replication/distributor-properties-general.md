---
title: "Propriedades do Distribuidor, Geral | Microsoft Docs"
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
  - "sql13.rep.configdistwizard.distproperties.general.f1"
helpviewer_keywords: 
  - "caixa de diálogo Propriedades do Distribuidor"
ms.assetid: ab4120ec-e524-4c0c-8b48-f2f40adb1a3b
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# Propriedades do Distribuidor, Geral
  A página **Geral** da caixa de diálogo **Propriedades do Distribuidor** permite adicionar e excluir bancos de dados de distribuição e definir propriedades do banco de dados de distribuição.  
  
 O banco de dados de distribuição armazena metadados e dados de histórico para todos os tipos de replicação e transações para replicação transacional. Em muitos casos, um único banco de dados de distribuição é suficiente. Porém, se vários Publicadores usarem um único Distribuidor, considere criar um banco de dados de distribuição para cada Publicador. Fazer isso assegura que os dados que fluem por cada banco de dados de distribuição são distintos.  
  
## Opções  
 **Bancos de dados**  
 O **bancos de dados** grade de propriedades mostra as propriedades name e retenção dos bancos de dados de distribuição no distribuidor. **Retenção de transação** é o comprimento das transações de hora são armazenados para replicação transacional (retenção de transação também é conhecido como retenção de distribuição). **Retenção de Histórico** é o período de tempo em que os metadados de histórico são armazenados para todos os tipos de replicação. Para obter mais informações sobre retenção de distribuição, consulte [desativação e expiração de assinatura](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
 Clique no botão Propriedades (**...**) no **bancos de dados** grade de propriedade para iniciar o **Propriedades de banco de dados de distribuição** caixa de diálogo.  
  
 **Nova**  
 Clique para criar um novo banco de dados de distribuição.  
  
 **Delete (excluir)**  
 Selecione um banco de dados de distribuição existente no **bancos de dados** grade de propriedade e clique em **Excluir** para excluir o banco de dados. O banco de dados de distribuição não poderá ser excluído se houver apenas esse banco de dados; cada distribuidor deve ter pelo menos um banco de dados de distribuição. Para excluir todos os bancos de dados de distribuição, você deve desabilitar a distribuição no computador. Para obter mais informações, consulte [Desabilitar publicação e distribuição](../../relational-databases/replication/disable-publishing-and-distribution.md).  
  
 **Padrões de Perfil**  
 Clique para acesso a perfis do replication agent no **perfis de agente** caixa de diálogo. Para obter mais informações sobre perfis, consulte [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
## Consulte também  
 [Configurar a distribuição](../../relational-databases/replication/configure-distribution.md)   
 [View and Modify Distributor and Publisher Properties](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)  
  
  