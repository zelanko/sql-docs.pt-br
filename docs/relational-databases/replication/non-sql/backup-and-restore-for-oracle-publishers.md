---
title: "Backup e restaura&#231;&#227;o para Publicadores Oracle | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "recuperação [replicação do SQL Server], publicação Oracle"
  - "backups [replicação do SQL Server], publicação Oracle"
  - "publicação Oracle [replicação do SQL Server], backup e restauração"
  - "restaurando [replicação do SQL Server], publicação Oracle"
ms.assetid: e5f181d0-cacf-442b-8b7a-202b3cfc358b
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# Backup e restaura&#231;&#227;o para Publicadores Oracle
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Siga essas diretrizes ao realizar backup e restauração:  
  
-   Assegure-se de que o Log Reader Agent não está sendo executado e que não haja outras atividades de banco de dados nas tabelas publicadas enquanto o Publicador estiver passando por backup.  
  
-   Efetue backup do Publicador e do Distribuidor ao mesmo tempo.  
  
-   Se houver necessidade de restaurar o Publicador ou o Distribuidor, reinicialize todas as assinaturas.  
  
-   Para restaurar um Assinante de um backup (sem ter de reinicializar as assinaturas), as transações entregues ao banco de dados de distribuição após a conclusão do último backup de banco de dados de assinatura ainda devem estar disponíveis. O tempo em que as transações estão disponíveis depende das configurações de retenção de distribuição. Para obter informações sobre essas configurações, consulte [desativação e expiração de assinatura](../../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
-   Se o Publicador ou o Distribuidor ficar fora de sincronia como resultado de uma restauração de banco de dados, os agentes de replicação registrarão mensagens de erro. Nesse ponto, você deve descartar e recriar todas as publicações e assinaturas relevantes:  
  
    1.  Faça um script da definição das publicações e assinaturas. Para obter mais informações, consulte [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
         Se a definição das publicações tiver sido alterada entre as versões presentes no Publicador e no Distribuidor, você precisará modificar os scripts.  
  
    2.  Descarte as publicações e as assinaturas.  
  
    3.  Execute os scripts criados na etapa 1.  
  
     Se o publicador deve ser descartado e reconfigurado, descarte o **MSSQLSERVERDISTRIBUTOR** sinônimo público e o usuário de replicação Oracle configurado com o **CASCADE** opção para remover todos os objetos de replicação do editor Oracle.  
  
## Consulte também  
 [Fazer backup e restaurar bancos de dados replicados](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [Configurar um publicador Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Visão geral da Publicação Oracle](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  