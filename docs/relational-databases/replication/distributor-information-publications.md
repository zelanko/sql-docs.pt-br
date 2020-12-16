---
description: Informações do distribuidor, publicações
title: Informações sobre o distribuidor, publicações | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.Distributor.Publications.f1
- sql13.rep.monitor.Distributor.commonjobs..f1
- sql13.rep.monitor.Distributor.SubscriptionSummary.merge.f1
- sql13.rep.monitor.Distributor.SubscriptionSummary.snapshot.f1
- sql13.rep.monitor.Distributor.SubscriptionSummary.tran.f1
ms.assetid: 1f499277-7f12-42ba-8cf4-52b683434944
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: b5fb4f1788ed3812490ca0e730f854b18c64e6ad
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464787"
---
# <a name="distributor-information-publications"></a>Informações do distribuidor, publicações
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  A guia **Publicações** fornece informações resumidas sobre todas as publicações no Distribuidor selecionado no painel esquerdo.  
  
As informações que são exibidas sobre as publicações com suporte do Distribuidor incluem uma coluna que contém a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do Publicador. Caso contrário, as informações de publicação serão iguais às informações de publicação fornecidas quando você exibe publicações na exibição Publicador do Replication Monitor. Para obter mais informações sobre as colunas da guia **Publicações** , consulte [Publisher Information, Publications](../../relational-databases/replication/publisher-information-publications.md).  

## <a name="subscription-watch-list"></a>Lista de Observação da Assinatura

### <a name="transactional-replication"></a>Replicação transacional
  As informações de assinaturas transacionais incluem o nome do Publicador. Caso contrário, a funcionalidade e as informações fornecidas nesta caixa de diálogo serão iguais as da exibição Publicador. Para mais informações sobre como usar essa caixa de diálogo, consulte [Informações do publicador, lista de inspeção da assinatura &#40;publicação transacional, SQL Server 2005 e posterior&#41;](../../relational-databases/replication/publisher-information-subscription-watch-list-transactional.md). 

### <a name="merge-replication"></a>Replicação de mesclagem
  As informações de assinaturas de publicação de mesclagem incluem o nome do Publicador. Caso contrário, a funcionalidade e as informações fornecidas nesta caixa de diálogo serão iguais as da exibição Publicador. Para mais informações sobre como usar essa caixa de diálogo, consulte [Informações do publicador, lista de inspeção da assinatura &#40;publicação de mesclagem, SQL Server 2005 e posterior&#41;](../../relational-databases/replication/publisher-information-subscription-watch-list-merge-publication.md).  

### <a name="snapshot-replication"></a>Replicação de instantâneo 
  As informações de assinaturas de publicação de instantâneo incluem o nome do Publicador. Caso contrário, a funcionalidade e as informações fornecidas nesta caixa de diálogo serão iguais as da exibição Publicador. Para mais informações sobre como usar essa caixa de diálogo, consulte [Informações do publicador, lista de inspeção da assinatura &#40;publicação de instantâneo, SQL Server 2005 e posterior&#41;](../../relational-databases/replication/publisher-information-subscription-watch-list-snapshot.md).  

## <a name="agents"></a>Agentes
 A guia **Agentes** exibe informações sobre os agentes e trabalhos de manutenção associados com o Publicador e o Assinante.  
  
 Os agentes disponíveis na guia **Agentes** de uma exibição Distribuidor no Distribuidor incluem todos os agentes disponíveis na guia **Agentes** de um Publicador. No entanto, a guia **Agentes** de uma exibição Distribuidor no Distribuidor também inclui um Agente Distribuidor e um Merge Agent.  
  
 Para obter mais informações sobre os agentes Snapshot, Log Reader e Queue Reader, e os trabalhos de manutenção, consulte [Publisher Information, Agents](../../relational-databases/replication/publisher-information-agents.md). Observe que, quando você exibe informações de agente na guia **Agentes** de um Distribuidor, as informações do Publicador estão presentes para os agentes Snapshot e Log Reader. No entanto, na guia **Agentes** de uma exibição Distribuidor no Distribuidor, ainda é possível selecionar **Agente Distribuidor** e **Merge Agent**.  
  
### <a name="options"></a>Opções  
 As seções a seguir descrevem os dados exibidos nesta guia do Agente Distribuidor e do Merge Agent.  
  
### <a name="distributor-agent"></a>Agente Distribuidor  
 **Status**  
 O status do agente. A seguinte lista mostra os possíveis valores de status:  
  
-   Erro    
-   Repetir    
-   Executando    
-   Não está em execução   
-   Nunca iniciado  
  
 **Publicador**  
 A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do Publicador.  
  
 **Publicação**  
 O nome da publicação com a qual o agente está associado.  
  
 **Assinatura**  
 O nome da assinatura, no formato: [*SubscriberName*].[*Database*].  
  
 **Tipo**  
 Tipo de replicação: push, pull ou Anônima.  
  
 **Última Hora de Início**  
 A última hora de início do agente.  
  
 **Duration**  
 O tempo de execução do agente. O tempo representa o tempo decorrido, se o agente estiver sendo executado no momento, e o tempo total, se o agente foi executado anteriormente.  
  
 **Última Ação**  
 A última ação executada durante a execução mais recente do agente.  
  
 **Taxa de Entrega**  
 A taxa, em comandos por segundo, com a qual os comandos de inicialização são confirmados no banco de dados de distribuição durante a execução mais recente do agente.  
  
 **Latência**  
 É o tempo, em segundos, que decorreu entre a alteração mais recente sendo confirmada no banco de dados de publicação e o comando correspondente sendo confirmado no banco de dados de distribuição.  
  
 **#Trans**  
 O número de transações confirmado no banco de dados de distribuição durante a execução mais recente do agente.  
  
 **#Cmds**  
 O número de comandos confirmado no banco de dados de distribuição durante a execução mais recente do agente. Um comando é igual a uma alteração de dados, como uma atualização.  
  
 **Avg. #Cmds**  
 O número médio de comandos por transação durante a execução mais recente do agente.  
  
### <a name="merge-agent"></a>Merge Agent  
 **Status**  
 O status do agente. A seguinte lista mostra os possíveis valores de status:  
  
-   Erro  
  
-   Repetir  
  
-   Executando  
  
-   Não está em execução  
  
-   Nunca iniciado  
  
 **Publicador**  
 A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do Publicador.  
  
 **Publicação**  
 O nome da publicação com a qual o agente está associado.  
  
 **Assinatura**  
 O nome da assinatura, no formato: [*SubscriberName*].[*Database*].  
  
 **Tipo**  
 Tipo de replicação: push, pull ou Anônima.  
  
 **Última Hora de Início**  
 A última hora de início do agente.  
  
 **Duration**  
 O tempo de execução do agente. O tempo representa o tempo decorrido, se o agente estiver sendo executado no momento, e o tempo total, se o agente foi executado anteriormente.  
  
 **Última Ação**  
 A última ação executada durante a execução mais recente do agente.  
  
 **Taxa de Entrega**  
 A taxa, em comandos por segundo, com a qual as alterações são confirmadas no banco de dados de distribuição.  
  
 **Inserções do Publicador**  
 Número de comandos INSERT aplicados no Publicador.  
  
 **Atualizações do Publicador**  
 Número de comandos UPDATE aplicados no Publicador.  
  
 **Exclusões do Publicador**  
 Número de comandos DELETE aplicados no Publicador.  
  
 **Conflitos do Publicador**  
 O número de conflitos por segundo que ocorrem no Publicador durante o processo de mesclagem.  
  
 **Inserções do Assinante**  
 Número de comandos INSERT aplicados no Assinante.  
  
 **Atualizações do Assinante**  
 Número de comandos UPDATE aplicados no Assinante.  
  
 **Exclusões do Assinante**  
 Número de comandos DELETE aplicados no Assinante.  
  
 **Conflitos do Assinante**  
 O número de conflitos por segundo que ocorrem no Assinante durante o processo de mesclagem.  

  
## <a name="see-also"></a>Consulte Também  
 [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Monitorando a Replicação](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)  
  
  
