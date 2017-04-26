---
title: "Visão geral da publicação Oracle | Microsoft Docs"
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
- publishing [SQL Server replication], Oracle publishing
- snapshot replication [SQL Server], Oracle publishing
- Oracle publishing [SQL Server replication]
- transactional replication, Oracle publishing
- Oracle publishing [SQL Server replication], about Oracle publishing
ms.assetid: 2e013259-0022-4897-a08d-5f8deb880fa8
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b9a7e0593342073272cfe3aae01ea4c28e5e2304
ms.lasthandoff: 04/11/2017

---
# <a name="oracle-publishing-overview"></a>Visão geral da Publicação Oracle
  Desde o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], você pode incluir Publicadores Oracle em sua topologia de replicação pelo Oracle versão 9i. Os servidores de publicação podem ser implantados em todos os sistemas operacionais e de hardware com suporte pelo Oracle. O recurso é criado sob a base bem-estabelecida da replicação de instantâneo e da replicação transacional do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , fornecendo desempenho e usabilidade similares.  
  
 A publicação Oracle foi preterida. A replicação heterogênea para assinantes que não são do SQL Server foi preterida. Para mover dados, crie soluções usando a captura de dados de alterações e o [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="snapshot-replication-for-oracle"></a>Replicação de instantâneo para Oracle  
 As publicações de instantâneo Oracle são implementadas de forma similar às publicações de instantâneo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Quando o Agente de Instantâneo é executado para uma publicação Oracle, ele se conecta ao Oracle e processa cada tabela na publicação Ao processar cada tabela, o agente recupera as linhas de tabela e cria scripts de esquemas, os quais são armazenados em seguida no compartilhamento de instantâneo da publicação. Todo conjunto de dados é criado sempre que o Agente de Instantâneo for executado, de modo que os gatilhos de rastreamento de alterações não sejam adicionados a tabelas Oracle como ocorre com a replicação transacional. A replicação de instantâneo fornece uma maneira conveniente para migrar os dados com um impacto mínimo no sistema de publicação.  
  
## <a name="transactional-replication-for-oracle"></a>Replicação transacional para Oracle.  
 As publicações transacionais Oracle são implementadas com o uso da arquitetura de publicação transacional do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]; no entanto, as alterações são rastreadas com o uso de uma combinação de gatilhos de banco de dados, no banco de dados Oracle e no Agente de Leitor de Log. Os assinantes de uma publicação transacional Oracle são inicializados automaticamente com o uso da replicação de instantâneo; as alterações subsequentes são rastreadas e distribuídas aos Assinantes à medida que ocorrem por meio do Agente de Leitor de Log.  
  
 Quando uma publicação Oracle é criada, os gatilhos e as tabelas de rastreamento são criados para cada tabela publicada dentro do banco de dados Oracle. Quando as alterações são feitas nas tabelas publicadas, os gatilhos do banco de dados nas tabelas são acionados e inserem informações nas tabelas de rastreamento de replicação para cada linha modificada. O Agente de Leitor de Log do Distribuidor do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] move em seguida as informações das alterações dos dados, das tabelas de rastreamento para o banco de dados de distribuição no Distribuidor. Para concluir, como em uma replicação transacional padrão o Agente de Distribuição move as alterações do Distribuidor para os Assinantes.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar um Publicador Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Glossário de termos para publicações Oracle](../../../relational-databases/replication/non-sql/glossary-of-terms-for-oracle-publishing.md)   
 [Replicação de banco de dados heterogênea](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)  
  
  
