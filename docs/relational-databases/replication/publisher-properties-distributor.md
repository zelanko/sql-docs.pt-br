---
title: "Propriedades do Publicador - Distribuidor | Microsoft Docs"
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
  - "sql13.rep.configdistwizard.distpubproperties.f1"
helpviewer_keywords: 
  - "caixa de diálogo Propriedades do Publicador"
ms.assetid: ab6ada76-0f99-43fe-b524-baac7b1bc483
caps.latest.revision: 19
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 19
---
# Propriedades do Publicador - Distribuidor
  A caixa de diálogo **Propriedades do Publicador** permite exibir e modificar propriedades associadas com a relação entre o Publicador e seu Distribuidor.  
  
## Opções  
 **Conexão do Agente com o Publicador**  
 Especifique o contexto no qual os agentes seguintes fazem conexões do Distribuidor com o Publicador:  
  
-   O Agente de Leitor de Fila para publicações transacionais, que permite assinaturas de atualização enfileiradas.  
  
-   O Agente de Instantâneo e Agente de Leitor de Log para publicações Oracle.  
  
 Selecione **Representar conta de processo do agente** para efetuar conexões com o Publicador usando o contexto de conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows na qual esses agentes executam ou especifique **Autenticação do SQL Server**e insira um valor para **Logon** e **Senha**. É recomendado que você selecione **Representar conta de processo do agente**. Para obter mais informações sobre segurança do agente, consulte [modelo de segurança do agente de replicação](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
 As contas do Windows nas quais esses agentes executam são especificadas no Assistente para Nova Publicação. Essas contas podem ser alteradas:  
  
-   Na caixa de diálogo **Propriedades do Distribuidor** para o Agente de Leitor de Fila.  
  
-   Na caixa de diálogo **Propriedades de Publicação** para o Agente de Instantâneo e Agente de Leitor de Log.  
  
 **Diversos**  
 As propriedades **tipo de editor** e **nome do banco de dados de distribuição** são somente leitura. A propriedade **Pasta Padrão de Instantâneo** pode ser alterada. Para obter mais informações sobre a pasta de instantâneo, consulte [proteger a pasta de instantâneo](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
## Consulte também  
 [Crie uma publicação](../../relational-databases/replication/publish/create-a-publication.md)   
 [View and Modify Distributor and Publisher Properties](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Referência de propriedades de & #40. Replicação e 41;](../../relational-databases/replication/properties-reference-replication.md)  
  
  