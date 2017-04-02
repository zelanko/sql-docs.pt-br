---
title: "MSSQL_ENG014157 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "erro MSSQL_ENG014157"
ms.assetid: 1a0890cf-d977-43e0-a2ba-9c5ff1a8f856
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# MSSQL_ENG014157
    
## Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|14157|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|A assinatura criada pelo Assinante '%s' para a publicação '%s' expirou e foi descartada.|  
  
## Explicação  
 Um Assinante deve fazer a sincronização com o Publicador no momento especificado no período de retenção de publicação. Se um Assinante não fizer a sincronização nesse período, a assinatura será expirada. Para obter mais informações, consulte [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
## Ação do usuário  
 É necessário recriar e inicializar a assinatura para que o Assinante comece a receber novamente as alterações de dados:  
  
-   Para obter informações sobre a criação de assinaturas, consulte [assinar publicações](../../relational-databases/replication/subscribe-to-publications.md).  
  
-   Para obter informações sobre inicialização de assinaturas, consulte [inicializar uma assinatura](../../relational-databases/replication/initialize-a-subscription.md).  
  
 Se o banco de dados de assinatura contém alterações que não foram sincronizadas com o publicador, você pode usar o [utilitário tablediff](../../tools/tablediff-utility.md) para determinar quais linhas são diferentes dos bancos de dados de publicação e assinatura.  
  
 É possível aumentar o período de retenção de publicação para que a assinatura não expire. Tome cuidado ao definir um valor alto, já que isso pode resultar no armazenamento de mais dados e metadados, o que afeta o desempenho. Para obter mais informações, consulte [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
## Consulte também  
 [Erros e eventos referência & #40. Replicação e 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  