---
title: Aprimorar o desempenho da replicação transacional | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
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
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 8ed18a3ea7ce4804146d448765d9f18e8b2a7f73
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "76288171"
---
# <a name="enhance-transactional-replication-performance"></a>Aprimorar o desempenho da replicação transacional
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Após considerar as dicas para o de desempenho geral descritas em [Aprimorando o Desempenho Geral da Replicação](../../../relational-databases/replication/administration/enhance-general-replication-performance.md), considere essas áreas adicionais específicas da replicação transacional.  
  
## <a name="database-design"></a>Design de banco de dados  
  
-   Minimize o tamanho de transação em seu design de aplicativo.  
  
     Por padrão, a replicação transacional propaga as alterações de acordo com limites da transação. Se as transações são menores, é menos provável que o agente de distribuição reenvie a transação devido a problemas de rede. Se for necessário que o agente reenvie uma transação, a quantidade de dados enviada será menor. 

  
## <a name="distributor-configuration"></a>Configuração do Distribuidor  
  
-   Configure o Distribuidor em um servidor dedicado.  
  
     Você pode reduzir a sobrecarga de processamento no Publicador configurando um Distribuidor remoto. Para obter mais informações, consulte [Configure Distribution](../../../relational-databases/replication/configure-distribution.md).  
  
-   Dimensione adequadamente o banco de dados de distribuição.  
  
     Teste a replicação com uma carga típica para seu sistema para determinar a quantidade de espaço necessária para armazenar comandos. Certifique-se de que o banco de dados seja amplo o suficiente para armazenar comandos, sem ter que aumentá-lo frequentemente. Para obter mais informações sobre como alterar o tamanho de um banco de dados, consulte [ALTER DATABASE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql.md).  
  
## <a name="publication-design"></a>Design de publicação  
  
-   Replique a execução de procedimento armazenado ao fazer atualizações em lote em tabelas publicadas.  
  
     Se tiver atualizações em lote que afetem ocasionalmente um grande número de linhas no Assinante, você deve considerar a atualização da tabela publicada usando um procedimento armazenado, e publicar a execução desse procedimento. Ao invés de enviar uma atualização ou excluir cada linha afetada, o Distribution Agent executa o mesmo procedimento no Assinante, com os mesmos valores de parâmetros. Para obter mais informações, consulte [Publicando execução de procedimento armazenado em replicação transacional](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
-   Espalhe os artigos por várias publicações.  
  
     Se não puder usar o parâmetro [ **-SubscriptionStreams**](#subscriptionstreams), considere a criação de várias publicações. Espalhar os artigos por essas publicações permite à replicação aplicar alterações em paralelo aos Assinantes.  
  
## <a name="subscription-considerations"></a>Considerações sobre assinatura  
  
-   Use agentes independentes ao invés de agentes compartilhados se tiver várias publicações no mesmo Publicador (esse é o padrão para o Assistente para Nova Publicação).  
  
-   Execute os agentes continuamente em vez de em horários muito frequentes.  
  
     Definir que os agentes executem continuamente, em vez de criar agendamentos frequentes (como a cada minuto), melhora o desempenho da replicação, eliminando as interrupções do agente. Quando você define que o Distribution Agent execute continuamente, as alterações são propagadas com uma baixa latência para os demais servidores conectados na topologia. Para obter mais informações, consulte:  
  
    -   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [Especificar agendamentos de sincronização](../../../relational-databases/replication/specify-synchronization-schedules.md)  
  
## <a name="distribution-agent-and-log-reader-agent-parameters"></a>Parâmetros do Distribution Agent e do Log Reader Agent  
Parâmetros de perfil de agente geralmente são ajustados para aumentar a produtividade do Leitor de Log e do Agente de Distribuição com sistemas OLTP de alto tráfego. 

Testes foram realizados para determinar os valores ideais para melhorar o desempenho para o Leitor de Log e o Agente de Distribuição. Esses testes concluíram que cargas de trabalho foi um fator determinante para quais valores funcionaram em qual situação. Assim, não existe um ajuste de valor único que melhora o desempenho em todas as situações. 

As conclusões: 
- Para um *Agente de Leitor de Log* com cargas de trabalho de transações menores (menos de 500 comandos), um valor mais alto de **ReadBatchSize** pode beneficiar a taxa de transferência. No entanto, para cargas de trabalho com grandes quantidades de transações, a alteração desse valor não melhorará o desempenho. 
    - Quando há vários Agentes de Leitor de Log e vários Agentes de Distribuição em execução em paralelo no mesmo servidor, um valor mais alto de **ReadBatchSize** causa a contenção de banco de dados de distribuição. 
- Para o *Agente de Distribuição*
    - Aumentar **CommitBatchSize** pode melhorar a taxa de transferência. A desvantagem é que, se ocorrer uma falha, o agente de distribuição deve voltar atrás e começar novamente a reaplicar um grande número de transações. 
    - Aumentar o valor **SubscriptionStreams** ajuda na produtividade geral do Agente de Distribuição, já que várias conexões com o assinante aplicam lotes de alterações em paralelo. No entanto, dependendo do número de processadores e outras condições de metadados (como chave primária, chaves estrangeiras, restrições exclusivas e índices), na verdade o valor mais alto de SubscriptionStreams pode ter um efeito adverso. Além disso, se um fluxo não for executado ou confirmado, o Agente de Distribuição voltará a usar um único fluxo para repetir os lotes com falha.


Para saber mais sobre esse teste, confira a postagem de blog [Otimizando os parâmetros de perfil de agente de replicação para melhorar o desempenho](https://blogs.msdn.microsoft.com/sql_server_team/optimizing-replication-agent-profile-parameters-for-better-performance/).


### <a name="log-reader-agent"></a>Agente de Leitor de Log

#### <a name="readbatchsize"></a>ReadBatchSize
- Aumente o valor do parâmetro **-ReadBatchSize** para o Agente de Leitor de Log.  
  
O Log Reader Agent e o Distribution Agent dão suporte ao tamanho dos lotes para as operações de leitura e confirmação de transações. O tamanho padrão dos lotes é de 500 transações. O Log Reader Agent lê o número específico de transações do log, mesmo essas estando marcadas ou não, para a replicação. Quando um grande número de transações é gravado em um banco de dados de publicação, mas somente um pequeno subconjunto for marcado para replicação, você deverá usar o parâmetro **-ReadBatchSize** para aumentar o tamanho do lote de leitura do Agente de Leitor de Log. Esse parâmetro não se aplica aos Editores Oracle.  

   - Cargas de trabalho de transações menores (menos de 500 comandos) têm um aumento no número de comandos que são processados por segundo quando **ReadBatchSize** é aumentado para até 5000. 
   - Para cargas de trabalho maiores (transações com 500 a 1000 comandos), o aumento de **ReadBatchSize** oferece poucas melhorias de desempenho. Aumentar **ReadBatchSize** resulta em um número maior de transações gravadas no banco de dados de distribuição em uma viagem de ida e volta. Isso aumenta as transações de tempo, os comandos são visíveis para o Agente de Distribuição e é introduzida latência no processo de replicação.  

#### <a name="pollinginterval"></a>PollingInterval
- Reduza o valor do parâmetro **-PollingInterval** para o Agente de Leitor de Log.  
  
O parâmetro **-PollingInterval** especifica com que frequência o log de transações de um banco de dados publicado é consultado sobre transações a serem replicadas. O padrão é 5 segundos. Se reduzir esse valor, o log é sondado com mais frequentemente, o que pode resultar em uma menor latência na entrega de transações de um banco de dados de publicação, para o banco de dados de distribuição. Porém, você deve equilibrar a necessidade por uma latência menor com uma carga maior no servidor, devido a uma sondagem mais frequente.   
  
#### <a name="maxcmdsintran"></a>MaxCmdsInTran
- Para resolver gargalos esporádicos e acidentais, use o parâmetro **–MaxCmdsInTran** para o Agente de Leitor de Log.  
  
O parâmetro **–MaxCmdsInTran** especifica o número máximo de instruções agrupadas em uma transação à medida que o Log Reader grava comandos no banco de dados de distribuição. O uso desse parâmetro permite que o Log Reader Agent e o Distribution Agent dividam transações volumosas (consistindo em muitos comandos) no Publicador em várias transações menores, ao aplicar os comandos no Assinante. A especificação desse parâmetro pode reduzir a contenção no Distribuidor e pode reduzir a latência entre o Publicador e o Assinante. Como a transação original é aplicada em unidades menores, o Assinante pode acessar linhas de uma transação lógica de Publicador antes do fim da transação original, O padrão é **0**, que preserva os limites de transação do Publicador. Esse parâmetro não se aplica aos Editores Oracle.  
  
   > [!WARNING]  
   >  O**MaxCmdsInTran** não foi criado para estar sempre ativado. Ele existe para solucionar casos em que alguém acidentalmente realizou um número grande de operações DML em uma única transação (causando atraso na distribuição de comandos até que a transação inteira esteja no banco de dados de distribuição, os bloqueios sejam mantidos etc.). Se você rotineiramente enfrentar essa situação, examine seus aplicativos e descubra maneiras de reduzir o tamanho da transação.  
  
### <a name="distribution-agent"></a>Agente de Distribuição

#### <a name="subscriptionstreams"></a>SubscriptionStreams
- Aumente o parâmetro **–SubscriptionStreams** para o Agente de Distribuição.  
  
O parâmetro **–SubscriptionStreams** pode melhorar significativamente a taxa de transferência da replicação de agregação. Ele permite várias conexões a um Assinante para aplicar lotes de alterações em paralelo, mantendo presentes, ao mesmo tempo, várias características transacionais, quando for usar um thread único. Se uma das conexões falhar na execução ou na confirmação, todas as conexões abortarão o lote atual, e o agente usará um fluxo único para repetir os lotes com falha. Antes de concluir a fase de repetição pode haver inconsistências transacionais temporárias no Assinante. Depois que os lotes com falha são confirmados com êxito, o Assinante é levado de volta a um estado de consistência transacional.  
  
Um valor para esse parâmetro de agente pode ser especificado usando o `@subscriptionstreams` de [sp_addsubscription &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md).  

Para saber mais sobre como implementar fluxos de assinatura, confira [Navegando pela configuração subscriptionStream de replicação do SQL](https://blogs.msdn.microsoft.com/repltalk/2010/03/01/navigating-sql-replication-subscriptionstreams-setting).
  
### <a name="blocking-monitor-thread"></a>Thread de monitor de bloqueio

O Agente de Distribuição mantém um thread do monitor de bloqueio que detecta o bloqueio entre sessões. Se o thread do monitor de bloqueio detectar um bloqueio entre as sessões, o Agente de Distribuição alternará para usar uma sessão a fim de reaplicar o lote atual de comandos que não puderam ser aplicados anteriormente.

O thread do monitor de bloqueio pode detectar o bloqueio entre sessões do Agente de Distribuição. No entanto, o thread do monitor de bloqueio não pode detectar o bloqueio nas seguintes situações:
- Uma das sessões em que o bloqueio ocorre não é uma sessão do Agente de Distribuição.
- Um deadlock de sessão congela as atividades do Agente de Distribuição.

Nessa situação, o Agente de Distribuição coordena todas as sessões para serem confirmadas juntas assim que os comandos são executados. Ocorrerá um deadlock entre as sessões se as seguintes condições forem verdadeiras:

- Ocorre um bloqueio entre as sessões do Agente de Distribuição e uma sessão que não é uma sessão do Agente de Distribuição.
- O Agente de Distribuição está aguardando todas as sessões concluírem a execução de seus comandos antes que o Agente de Distribuição coordene todas as sessões para serem confirmadas juntas.

Por exemplo, configure o parâmetro *SubscriptionStreams* como 8. A sessão 10 até a sessão 17 são sessões do Agente de Distribuição. A sessão 18 não é uma sessão do Agente de Distribuição. A sessão 10 está bloqueada pela sessão 18, e a sessão 18 está bloqueada pela sessão 11. Além disso, as sessões 10 e 11 da sessão devem ser confirmadas juntas. No entanto, o Agente de Distribuição não pode confirmar as sessões 10 e 11 juntas devido ao bloqueio. Portanto, o Agente de Distribuição não pode coordenar essas oito sessões para serem confirmadas juntas até que as sessões 10 e 11 concluam a execução dos seus comandos.

Este exemplo resulta em um estado no qual nenhuma sessão está executando seus comandos. Quando o tempo especificado na propriedade **QueryTimeout** é atingido, o Agente de Distribuição cancela todas as sessões.

> [!Note]
> Por padrão, o valor da propriedade **QueryTimeout** é de 5 minutos.

Você pode observar as seguintes tendências dos contadores de desempenho do Agente de Distribuição durante esse período de tempo limite de consulta: 

- O valor do contador de desempenho **Dist: Delivered Cmds/sec** é sempre 0.
- O valor do contador de desempenho **Dist: Delivered Trans/sec** é sempre 0.
- O contador de desempenho **Dist: Delivery Latency** reporta um aumento no valor até que o deadlock do thread seja resolvido.

O tópico "Agente de Distribuição de Replicação" nos Manuais Online do SQL Server contém a seguinte descrição do parâmetro *SubscriptionStreams*: "Se uma das conexões não for executada nem for confirmada, todas as conexões anularão o lote atual, e o agente usará um fluxo único para repetir os lotes com falha."

O Agente de Distribuição usa uma sessão para repetir o lote que não pôde ser aplicado. Depois que o Agente de Distribuição aplicar com êxito o lote, ele retomará o uso de várias sessões sem reiniciar.

#### <a name="commitbatchsize"></a>CommitBatchSize
- Aumente o valor do parâmetro **-CommitBatchSize** para o Agente de Leitor de Log.  
  
A confirmação de um conjunto de transações tem uma sobrecarga fixa. Ao confirmar um número maior de transações com menor frequência, a sobrecarga será espalhada em um volume de dados maior.  Aumentar CommitBatchSize (até 200) pode melhorar o desempenho, conforme mais transações são confirmadas para o assinante. Porém, o benefício em aumentar esse parâmetro é anulado, pois, o custo para aplicar alterações é retido por outros fatores, como o E/S máximo do disco que contém o log. Além disso, existe uma compensação a ser considerada: qualquer falha que faz com que o Distribution Agent se reinicie deverá ser revertida e reaplicar um grande número de transações. Para as redes não confiáveis, um valor inferior pode resultar em menos falhas e em um número menor de transações a serem revertidas e reaplicadas em caso de falha.  
  

## <a name="see-more"></a>Ver mais
  
[Trabalhar com perfis do Agente de Replicação](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
[Exibir e modificar parâmetros do prompt de comando de agentes de replicação &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
[Conceitos dos executáveis do Replication Agent](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
  
