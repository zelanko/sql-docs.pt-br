---
title: Aprimorar o desempenho da replicação transacional | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- publications [SQL Server replication], design and performance
- performance [SQL Server replication], transactional replication
- designing databases [SQL Server], replication performance
- performance [SQL Server replication], snapshot replication
- snapshot replication [SQL Server], performance
- subscriptions [SQL Server replication], performance considerations
- agents [SQL Server replication], performance
- Distribution Agent, performance
- transactional replication, performance
- Log Reader Agent, performance
ms.assetid: 67084a67-43ff-4065-987a-3b16d1841565
caps.latest.revision: 39
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4e503b9cda54099a4fa283f3ef26747b9d5c9bd9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="enhance-transactional-replication-performance"></a>Aprimorar o desempenho da replicação transacional
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Após considerar as dicas para o de desempenho geral descritas em [Aprimorando o Desempenho Geral da Replicação](../../../relational-databases/replication/administration/enhance-general-replication-performance.md), considere essas áreas adicionais específicas da replicação transacional.  
  
## <a name="database-design"></a>Design de banco de dados  
  
-   Minimize o tamanho de transação em seu design de aplicativo.  
  
     Por padrão, a replicação transacional propaga as alterações de acordo com limites da transação. Em transações menores, é menos provável que o Distribution Agent tenha que reenviar a transação devido a problemas de rede. Se for necessário que o agente reenvie uma transação, a quantidade de dados enviada será menor.  
  
## <a name="distributor-configuration"></a>Configuração do Distribuidor  
  
-   Configure o Distribuidor em um servidor dedicado.  
  
     Você pode reduzir a sobrecarga de processamento no Publicador configurando um Distribuidor remoto. Para obter mais informações, consulte [Configure Distribution](../../../relational-databases/replication/configure-distribution.md).  
  
-   Dimensione adequadamente o banco de dados de distribuição.  
  
     Teste a replicação com uma carga típica para seu sistema para determinar a quantidade de espaço necessária para armazenar comandos. Certifique-se de que o banco de dados seja amplo o suficiente para armazenar comandos, sem ter que aumentá-lo frequentemente. Para obter mais informações sobre como alterar o tamanho de um banco de dados, consulte [ALTER DATABASE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql.md).  
  
## <a name="publication-design"></a>Design de publicação  
  
-   Replique a execução de procedimento armazenado ao fazer atualizações em lote em tabelas publicadas.  
  
     Se tiver atualizações em lote que afetem ocasionalmente um grande número de linhas no Assinante, você deve considerar a atualização da tabela publicada usando um procedimento armazenado, e publicar a execução desse procedimento. Ao invés de enviar uma atualização ou excluir cada linha afetada, o Distribution Agent executa o mesmo procedimento no Assinante, com os mesmos valores de parâmetros. Para saber mais, confira [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
-   Espalhe os artigos por várias publicações.  
  
     Se não puder usar o parâmetro **- SubscriptionStreams** (descrito mais adiante neste tópico), considere a criação de várias publicações. Espalhar os artigos por essas publicações permite à replicação aplicar alterações em paralelo aos Assinantes.  
  
## <a name="subscription-considerations"></a>Considerações sobre assinatura  
  
-   Use agentes independentes ao invés de agentes compartilhados se tiver várias publicações no mesmo Publicador (esse é o padrão para o Assistente para Nova Publicação).  
  
-   Execute os agentes continuamente em vez de em horários muito frequentes.  
  
     Definir que os agentes executem continuamente, em vez de criar agendamentos frequentes (como a cada minuto), melhora o desempenho da replicação, eliminando as interrupções do agente. Quando você define que o Distribution Agent execute continuamente, as alterações são propagadas com uma baixa latência para os demais servidores conectados na topologia. Para obter mais informações, consulte:  
  
    -   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [Especificar agendamentos de sincronização](../../../relational-databases/replication/specify-synchronization-schedules.md)  
  
## <a name="distribution-agent-and-log-reader-agent-parameters"></a>Parâmetros do Distribution Agent e do Log Reader Agent  
  
-   Para resolver gargalos esporádicos e acidentais, use o parâmetro **–MaxCmdsInTran** para o Agente de Leitor de Log.  
  
     O parâmetro **–MaxCmdsInTran** especifica o número máximo de instruções agrupadas em uma transação à medida que o Log Reader grava comandos no banco de dados de distribuição. O uso desse parâmetro permite que o Log Reader Agent e o Distribution Agent dividam transações volumosas (consistindo em muitos comandos) no Publicador em várias transações menores, ao aplicar os comandos no Assinante. A especificação desse parâmetro pode reduzir a contenção no Distribuidor e pode reduzir a latência entre o Publicador e o Assinante. Como a transação original é aplicada em unidades menores, o Assinante pode acessar linhas de uma transação lógica de Publicador antes do fim da transação original, O padrão é **0**, que preserva os limites de transação do Publicador. Esse parâmetro não se aplica aos Editores Oracle.  
  
    > [!WARNING]  
    >  O**MaxCmdsInTran** não foi criado para estar sempre ativado. Ele existe para solucionar casos em que alguém acidentalmente realizou um número grande de operações DML em uma única transação (causando atraso na distribuição de comandos até que a transação inteira esteja no banco de dados de distribuição, os bloqueios sejam mantidos etc.). Se você rotineiramente enfrentar essa situação, deverá revisar seus aplicativos e descobrir maneiras de reduzir o tamanho da transação.  
  
-   Use o parâmetro **–SubscriptionStreams** para o Agente de Distribuição.  
  
     O parâmetro **–SubscriptionStreams** pode melhorar significativamente a taxa de transferência da replicação de agregação. Ele permite várias conexões a um Assinante para aplicar lotes de alterações em paralelo, mantendo presentes, ao mesmo tempo, várias características transacionais, quando for usar um thread único. Se uma das conexões falhar na execução ou na confirmação, todas as conexões abortarão o lote atual, e o agente usará um fluxo único para repetir os lotes com falha. Antes de concluir a fase de repetição pode haver inconsistências transacionais temporárias no Assinante. Depois que os lotes com falha são confirmados com êxito, o Assinante é levado de volta a um estado de consistência transacional.  
  
     Um valor para esse parâmetro de agente pode ser especificado usando o **@subscriptionstreams** de [sp_addsubscription &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md).  
  
-   Aumente o valor do parâmetro **-ReadBatchSize** para o Agente de Leitor de Log.  
  
     O Log Reader Agent e o Distribution Agent dão suporte ao tamanho dos lotes para as operações de leitura e confirmação de transações. O tamanho padrão dos lotes é de 500 transações. O Log Reader Agent lê o número específico de transações do log, mesmo essas estando marcadas ou não, para a replicação. Quando um grande número de transações é gravado em um banco de dados de publicação, mas somente um pequeno subconjunto for marcado para replicação, você deverá usar o parâmetro **-ReadBatchSize** para aumentar o tamanho do lote de leitura do Agente de Leitor de Log. Esse parâmetro não se aplica aos Editores Oracle.  
  
-   Aumente o valor do parâmetro **-CommitBatchSize** para o Agente de Leitor de Log.  
  
     A confirmação de um conjunto de transações tem uma sobrecarga fixa. Ao confirmar um número maior de transações com menor frequência, a sobrecarga será espalhada em um volume de dados maior. Porém, o benefício em aumentar esse parâmetro é anulado, pois, o custo para aplicar alterações é retido por outros fatores, como o E/S máximo do disco que contém o log. Além disso, existe uma compensação a ser considerada: qualquer falha que faz com que o Distribution Agent se reinicie deverá ser revertida e reaplicar um grande número de transações. Para as redes não confiáveis, um valor inferior pode resultar em menos falhas e em um número menor de transações a serem revertidas e reaplicadas em caso de falha.  
  
-   Reduza o valor do parâmetro **-PollingInterval** para o Agente de Leitor de Log.  
  
     O parâmetro **-PollingInterval** especifica com que frequência o log de transações de um banco de dados publicado é consultado sobre transações a serem replicadas. O padrão é 5 segundos. Se reduzir esse valor, o log é sondado com mais frequentemente, o que pode resultar em uma menor latência na entrega de transações de um banco de dados de publicação, para o banco de dados de distribuição. Porém, você deve equilibrar a necessidade por uma latência menor com uma carga maior no servidor, devido a uma sondagem mais frequente.  
  
 Os parâmetros de agente podem ser especificados em perfis de agente e na linha de comando. Para obter mais informações, consulte:  
  
-   [Trabalhar com perfis do Agente de Replicação](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
-   [Exibir e modificar parâmetros do prompt de comando do agente de replicação &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
-   [Conceitos dos executáveis do Replication Agent](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
  
