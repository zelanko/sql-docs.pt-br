---
title: Sincronizar dados | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- synchronization [SQL Server replication], about synchronization
- merge replication synchronization [SQL Server replication]
- scripts [SQL Server replication], synchronization and
- synchronization [SQL Server replication]
- snapshot replication [SQL Server], synchronization
- transactional replication, synchronization
- subscriptions [SQL Server replication], synchronizing
- on demand script execution
- replication [SQL Server], synchronization
- scripts [SQL Server replication]
ms.assetid: 724802f7-7d69-46d3-a330-bd8aa7f53114
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: aa4bf39868593b7d43d54b90774ef4a40060d02d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67927894"
---
# <a name="synchronize-data"></a>Sincronizar dados
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Sincronizando dados se refere ao processo de alterações de dados e esquemas sendo propagadas entre o Publicador e os Assinantes após o instantâneo inicial ter sido aplicado ao Assinante. A sincronização pode acontecer:  
  
-   Continuamente, o que é típico para replicação transacional.  
  
-   Sob demanda, o que é típico para replicação de mesclagem.  
  
-   Em um agendamento, o que é típico para replicação de instantâneo.  
  
 Quando uma assinatura é sincronizada, diferentes processos acontecem baseados no tipo de replicação que você está usando:  
  
-   Replicação de instantâneo A sincronização significa que o Agente de Distribuição reaplicou o instantâneo ao Assinante para que o esquema e os dados no banco de dados da assinatura sejam consistentes com o bando de dados da publicação.  
  
     Se alterações nos dados ou no esquema tiverem sido feitas no Publicador, um novo instantâneo deve ser gerado para propagar as modificações ao Assinante.  
  
-   Replicação transacional. A sincronização significa que o Agente de Distribuição transfere atualizações, inserções, exclusões e quaisquer outras modificações do banco de dados de distribuição ao Assinante.  
  
-   Replicação de mesclagem. A sincronização significa que o Agente de Mesclagem carrega alterações do Assinante ao Publicador e depois baixa as alterações do Publicador ao Assinante. Conflitos, se houver, são detectados e resolvidos. Os dados são convergidos e o Publicador e todos os Assinantes eventualmente acabam com os mesmos valores de dados. Se os conflitos forem detectados e resolvidos, o trabalho que foi confirmado por alguns usuários é alterado para resolver o conflito de acordo com a política que você definir.  
  
 Publicações de instantâneo atualizam completamente o esquema no Assinante cada vez que ocorrer uma sincronização, assim todas as alterações de esquema são aplicadas ao Assinante. Replicação transacional e replicação de mesclagem também oferecem suporte às alterações de esquema mais comuns. Para obter mais informações, consulte [Make Schema Changes on Publication Databases](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md) (Fazer alterações de esquema em bancos de dados de publicação).  
  
 Para sincronizar uma assinatura push, consulte [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
 Para sincronizar uma assinatura pull, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
 Para definir agendas de sincronização, consulte [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md).  
  
 **Para exibir e resolver conflitos de sincronização**  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Exibir e resolver conflitos de dados em publicações de mesclagem &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view-and-resolve-data-conflicts-for-merge-publications.md)  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Exibir conflitos de dados em publicações transacionais &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
## <a name="executing-code-during-synchronization"></a>Executando código durante sincronização  
 A replicação suporta dois métodos de execução de código durante a sincronização  
  
-   A execução de script sob demanda tem suporte para replicação transacional e replicação de mesclagem. Usando em execução de script sob demanda, você pode especificar um script SQL para ser executado durante a sincronização. O script é copiado ao Assinante e executado usando **sqlcmd** no começo do processo de sincronização. O script não tem acesso às alterações replicadas enquanto elas são aplicadas ao Assinante. Para obter mais informações, consulte [Executar scripts durante a sincronização &#40;Programação do Transact-SQL de Replicação&#41;](../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md).  
  
-   Manipuladores de lógica de negócios possuem suporte para replicação de mesclagem. Usando a estrutura dos manipuladores de lógica de negócios, você pode escrever um assembly de código gerenciado durante o processo de sincronização de mesclagem. O assembly inclui lógica comercial que pode responder a uma série de condições durante a sincronização: alterações de dados, conflitos e erros. Para obter mais informações, consulte [Executar lógica de negócios durante a sincronizações de mesclagem](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Detectar e resolver conflitos de replicação de mesclagem](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
