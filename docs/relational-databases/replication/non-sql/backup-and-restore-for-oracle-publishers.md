---
title: "Backup e restauração para Publicadores Oracle | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- recovery [SQL Server replication], Oracle publishing
- backups [SQL Server replication], Oracle publishing
- Oracle publishing [SQL Server replication], backup and restore
- restoring [SQL Server replication], Oracle publishing
ms.assetid: e5f181d0-cacf-442b-8b7a-202b3cfc358b
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 802d157cd886f5656513904c0b519a65b61d67b3
ms.lasthandoff: 04/11/2017

---
# <a name="backup-and-restore-for-oracle-publishers"></a>Backup e restauração para Publicadores Oracle
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Siga essas diretrizes ao realizar backup e restauração:  
  
-   Assegure-se de que o Log Reader Agent não está sendo executado e que não haja outras atividades de banco de dados nas tabelas publicadas enquanto o Publicador estiver passando por backup.  
  
-   Efetue backup do Publicador e do Distribuidor ao mesmo tempo.  
  
-   Se houver necessidade de restaurar o Publicador ou o Distribuidor, reinicialize todas as assinaturas.  
  
-   Para restaurar um Assinante de um backup (sem ter de reinicializar as assinaturas), as transações entregues ao banco de dados de distribuição após a conclusão do último backup de banco de dados de assinatura ainda devem estar disponíveis. O tempo em que as transações estão disponíveis depende das configurações de retenção de distribuição. Para obter informações sobre essas configurações, consulte [Desativação e expiração de assinatura](../../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
-   Se o Publicador ou o Distribuidor ficar fora de sincronia como resultado de uma restauração de banco de dados, os agentes de replicação registrarão mensagens de erro. Nesse ponto, você deve descartar e recriar todas as publicações e assinaturas relevantes:  
  
    1.  Faça um script da definição das publicações e assinaturas. Para obter mais informações, consulte [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
         Se a definição das publicações tiver sido alterada entre as versões presentes no Publicador e no Distribuidor, você precisará modificar os scripts.  
  
    2.  Descarte as publicações e as assinaturas.  
  
    3.  Execute os scripts criados na etapa 1.  
  
     Se houver necessidade de descartar e reconfigurar o Publicador, descarte o sinônimo público **MSSQLSERVERDISTRIBUTOR** e configure o usuário de replicação Oracle com a opção **CASCADE** para remover todos os objetos de replicação do Oracle Publisher.  
  
## <a name="see-also"></a>Consulte também  
 [Fazer backup e restaurar bancos de dados replicados](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [Configurar um Publicador Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Oracle Publishing Overview](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
