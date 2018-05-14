---
title: Aprimorar o desempenho de replicação geral | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- publications [SQL Server replication], design and performance
- designing databases [SQL Server], replication performance
- Snapshot Agent, performance
- snapshots [SQL Server replication], performance considerations
- merge replication performance [SQL Server replication]
- snapshot replication [SQL Server], performance
- subscriptions [SQL Server replication], performance considerations
- agents [SQL Server replication], performance
- performance [SQL Server replication], general considerations
- transactional replication, performance
ms.assetid: 895b1ad7-ffb9-4a5c-bda6-e1dfbd56d9bf
caps.latest.revision: 45
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6fa663e269559fb2eb87d599723734639a717d2e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="enhance-general-replication-performance"></a>Aprimorar o desempenho geral da replicação
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  É possível melhorar o desempenho geral para todos os tipos de replicação no seu aplicativo e na rede, por meio das diretrizes descritas neste tópico.  
  
## <a name="server-and-network"></a>Servidor e rede  
  
-   Defina a quantidade mínima e máxima de memória alocada para [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)].  
  
     Por padrão, o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] altera seus requisitos de memória dinamicamente com base nos recursos do sistema disponíveis. Para evitar baixa disponibilidade de memória durante as atividades de replicação, use a opção **min server memory** para definir a mínima memória disponível. Para evitar que o sistema operacional busque memória no disco, você também pode definir a quantidade máxima de memória com a opção **max server memory** . Para mais informações, consulte [Opções de configuração do servidor da memória do servidor](../../../database-engine/configure-windows/server-memory-server-configuration-options.md).  
  
-   Assegure alocação adequada de arquivos de dados de banco de dados e arquivos de log. Use uma unidade de disco separada para o log de transação para todos os bancos de dados envolvidos na replicação.  
  
     É possível diminuir o tempo de gravação das transações armazenando os arquivos de log em uma unidade de disco diferente da usada para armazenar o banco de dados. É possível espelhar aquela unidade, usando um RAID (Arranjo Redundante de Discos Baratos)-1, se for necessária tolerância a falhas. Use RAID 0 ou 0+1 (dependendo de sua necessidade por tolerância a falhas) para outros arquivos de banco de dados. Essa é uma prática boa que independe do uso da replicação.  
  
-   Considere a adição de memória a servidores usados na replicação, particularmente o Distribuidor.  
  
-   Use computadores com multiprocessadores.  
  
     Os agentes de replicação podem tirar proveito de processadores adicionais no servidor. Se estiver trabalhando com alto uso de CPU, considere a instalação de uma CPU mais rápida ou de várias CPUs.  
  
-   Use uma rede rápida.  
  
     A rede pode ser um gargalo de desempenho significante, particularmente para replicação transacional. A propagação de alterações aos Assinantes pode ser melhorada significantemente por meio de uma rede rápida de 100 megabits por segundo (Mbs) ou mais rápida. Se a rede for lenta, especifique configurações de rede e parâmetros de agente apropriados.  
  
## <a name="database-design"></a>Design de banco de dados  
  
-   Siga as práticas recomendadas para design de banco de dados.  
  
     Um banco de dados replicado geralmente se beneficia das mesmas otimizações de desempenho que um banco de dados não replicado. Entretanto, os índices devem ser usados com cautela no Assinante: a coluna de chave primária no Assinante deve ser indexada, mas índices adicionais podem afetar o desempenho de inserção, atualização e exclusão.  
  
-   Considere definir a opção de banco de dados READ_COMMITTED_SNAPSHOT.  
  
     Para ajudar a reduzir a contenção entre a atividade do usuário e a atividade do agente de replicação, defina essa opção para os bancos de dados de publicação e assinatura:  
  
    ```  
    ALTER DATABASE AdventureWorks  
    SET READ_COMMITTED_SNAPSHOT ON  
    ```  
  
     Para obter mais informações, veja [ALTER DATABASE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql.md).  
  
-   Seja cauteloso com a lógica do aplicativo nos gatilhos.  
  
     A lógica corporativa nos gatilhos definidos pelo usuário no Assinante pode reduzir a velocidade da replicação de alterações no Assinante:  
  
    -   Para a replicação transacional, pode ser mais eficiente incluir essa lógica nos procedimentos armazenados personalizados usados para aplicar os comandos de replicação. Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
    -   Para replicação de mesclagem, pode ser mais eficiente usar manipuladores de lógica de negócios. Para obter mais informações, consulte [Executar lógica de negócios durante a sincronizações de mesclagem](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md).  
  
     Se gatilhos forem usados para manter a integridade referencial nas tabelas publicadas para replicação de mesclagem, especifique a ordem de processamento das tabelas para reduzir o número de repetições necessárias para o Merge Agent. Para obter mais informações, consulte [Especificar a ordem de processamento dos artigos de mesclagem](../../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md).  
  
-   Limite o uso de tipos de dados LOB (objetos grandes).  
  
     Os LOBs requerem mais espaço de armazenamento e processamento que outros tipos de dados de coluna. Não inclua essas colunas em artigos a menos que seja necessário para seu aplicativo. Os tipos de dados **text**, **ntext**e **image** são preteridos. Se incluir LOBs, recomendamos o uso dos tipos de dados **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, respectivamente.  
  
     Para replicação transacional, considere usar o perfil do Distribution Agent chamado **Perfil de distribuição para fluxo contínuo do banco de dados OLE**. Para saber mais, confira [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
## <a name="publication-design"></a>Design de publicação  
  
-   Publique somente os dados requeridos.  
  
     Porque a replicação é fácil de configurar, há uma tendência para publicar mais dados do que é, de fato, necessário. Isso pode consumir recursos adicionais dentro dos bancos de dados de distribuição e arquivos de instantâneo, e pode reduzir a taxa de transferência para os dados requeridos. Evite publicar tabelas desnecessárias e considere atualizar as publicações com menos frequência.  
  
-   Minimize conflitos por design de publicação e comportamento de aplicativo.  
  
     Os seguintes tipos de replicação permitem que os dados sejam alterados no Assinante: replicação de mesclagem, replicação transacional com assinaturas atualizáveis e replicação transacional ponto a ponto. A replicação de mesclagem e a replicação transacional com assinaturas atualizáveis oferecem suporte a conflitos de dados, se uma dada linha for atualizada em um ou mais nós entre sincronizações. A replicação ponto a ponto não oferece suporte a conflitos de dados; as alterações de dados devem ser particionadas. Independentemente do tipo de replicação usada, recomendamos que o particionamento das alterações sempre que possível, pois isso reduz o processamento necessário para detecção e resolução de conflitos.  
  
     As alterações podem ser particionadas por meio da publicação de subconjuntos de dados em cada Assinante, ou fazendo com que o aplicativo faça alterações diretas para uma determinada linha em um nó específico:  
  
    -   A replicação de mesclagem oferece suporte a subconjuntos de publicação de dados que usam filtros com parâmetros com uma única publicação. Para saber mais, confira [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
    -   A replicação transacional oferece suporte à publicação de subconjuntos de dados que usam filtros estáticos com publicações múltiplas. Para obter mais informações, consulte [Filter Published Data](../../../relational-databases/replication/publish/filter-published-data.md) (Filtrar dados publicados).  
  
-   Use filtros de linha criteriosamente.  
  
     Quando uma publicação transacional inclui um ou mais artigos que usam filtros de linha, o Log Reader Agent deve aplicar o filtro a cada linha afetada por uma atualização à tabela enquanto verifica o log de transações. Consequentemente, a taxa de transferência do Log Reader Agent é afetada.  
  
     De forma semelhante, a replicação de mesclagem deve avaliar as linhas alteradas ou excluídas para determinar quais Assinantes devem receber essas linhas. Quando os filtros de linha são empregados para reduzir os dados requeridos no Assinante, esse processamento é mais complexo e pode ser mais lento do que publicar todas as linhas em uma tabela. Considere cuidadosamente a troca entre requisitos de armazenamento reduzidos em cada Assinante e a necessidade de alcançar a taxa de transferência máxima. Para mais informações sobre filtragem, consulte [Filtrar dados publicados](../../../relational-databases/replication/publish/filter-published-data.md).  
  
## <a name="subscription-considerations"></a>Considerações sobre assinatura  
  
-   Use assinaturas pull quando houver um número grande de Assinantes.  
  
     O Distribution Agent e o Merge Agent são executados no Distribuidor para as assinaturas push e nos Assinantes para assinaturas pull. Use assinaturas pull para melhorar o desempenho movendo o processamento do agente do Distribuidor para os Assinantes. Para obter mais informações, consulte [Subscribe to Publications](../../../relational-databases/replication/subscribe-to-publications.md) (Assinar publicações).  
  
-   Considere a reinicialização da assinatura se os Assinantes estiverem muito desatualizados.  
  
     Quando grandes quantidades de alterações precisarem ser enviadas aos Assinantes, reinicializá-los com um novo instantâneo pode ser mais rápido que usar a replicação para mover as alterações individuais. Para obter mais informações, consulte [Reinicializar as assinaturas](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
     Para replicação transacional, o Replication Monitor exibe na guia **Comandos Não Distribuídos** as informações sobre: o número de transações no banco de dados de distribuição que ainda não foi distribuídas ao Assinante e o tempo estimado para distribuir essas transações. Para obter mais informações, consulte [View Information and Perform Tasks for the Agents Associated With a Subscription &#40;Replication Monitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md) [Exibir informações e executar tarefas para os agentes associados a uma assinatura (Replication Monitor)].  
  
## <a name="snapshot-considerations"></a>Considerações de instantâneo  
  
-   Execute o Snapshot Agent apenas quando necessário e em períodos de pouca atividade.  
  
     O Snapshot Agent copia em massa os dados da tabela publicada no Publicador para uma pasta de instantâneo no Distribuidor. Gerar um instantâneo pode ser um processo intensivo de recurso e é melhor ser agendado para períodos de pouca atividade.  
  
-   Use um instantâneo de modo nativo a menos que um instantâneo de modo de caractere seja requerido.  
  
     Use o instantâneo de modo nativo para todos os Assinantes exceto os Assinantes não[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e Assinantes que estão executando o [!INCLUDE[ssEW](../../../includes/ssew-md.md)], que requerem o instantâneo de modo de caractere.  
  
-   Use uma única pasta de instantâneo para a publicação.  
  
     Ao especificar as propriedades da publicação relacionadas com o local do instantâneo, é possível escolher gerar os arquivos de instantâneo na pasta de instantâneo padrão, em uma pasta alternativa de instantâneo ou em ambos. Gerar arquivos de instantâneo em ambos os locais requer espaço em disco adicional e mais processamento durante a execução do Snapshot Agent.  
  
-   Coloque a pasta de instantâneo em uma unidade local do Distribuidor que não seja usada para armazenar bancos de dados ou arquivos de log.  
  
     O Snapshot Agent executa uma gravação sequencial de dados na pasta de instantâneo. Colocar a pasta de instantâneo em uma unidade separada de qualquer banco de dados ou de arquivos de log reduz a contenção entre os discos, e faz com que o processo do instantâneo seja concluído mais rapidamente.  
  
-   Ao criar o banco de dados de assinatura no Assinante, considere especificar um modelo de recuperação de registros simples ou com log de operações em massa. Isso permite log mínimo das inserções em massa executado durante a aplicação do instantâneo no Assinante. Após o instantâneo ter sido aplicado ao banco de dados de assinatura, é possível mudar para um modelo diferente de recuperação, se necessário (os bancos de dados replicados podem usar qualquer um dos modelos de recuperação). Para mais informações sobre como selecionar um modelo de recuperação, consulte [Visão geral da recuperação e da restauração &#40;SQL Server&#41;](../../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  
  
-   Considere usar a pasta de instantâneo alternativo e instantâneos compactados em mídia removíveis para redes que não sejam de banda larga.  
  
     Os arquivos de instantâneo compactados na pasta de instantâneo alternativo podem reduzir os requisitos de armazenamento em disco, e facilitar a transferência de arquivos de instantâneo em mídia removível.  
  
     Os instantâneos compactados podem, em alguns casos, melhorar o desempenho da transferência de arquivos de instantâneo pela rede. No entanto, a compactação de instantâneos exige processamento adicional por parte do Snapshot Agent ao gerar os arquivos de instantâneo, e por parte do Distribution Agent ou Merge Agent ao aplicar os arquivos de instantâneo. Em alguns casos, isso pode reduzir a velocidade da geração de instantâneos e aumentar o tempo para se aplicar um instantâneo. Além disso, instantâneos compactados não podem ser retomados no caso de uma falha de rede; consequentemente, não são apropriados para redes não confiáveis. Considere essa possibilidade cuidadosamente ao usar instantâneos compactados por uma rede. Para obter mais informações, consulte [Alternate Snapshot Folder Locations](../../../relational-databases/replication/alternate-snapshot-folder-locations.md) e [Compressed Snapshots](../../../relational-databases/replication/compressed-snapshots.md).  
  
-   Considere inicializar uma assinatura manualmente.  
  
     Em alguns cenários, como os que envolvem grandes bancos de dados iniciais, é preferível inicializar uma assinatura usando um método diferente do que usando um instantâneo. Para obter mais informações, consulte [Initialize a Transactional Subscription Without a Snapshot](../../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
## <a name="agent-parameters"></a>Parâmetros de agente  
  
-   Reduza os níveis detalhados de agentes de replicação, exceto durante o teste inicial, a monitoração e a depuração.  
  
     Reduza os parâmetros **–HistoryVerboseLevel** e **–OutputVerboseLevel** dos Agentes de Distribuição ou dos Agentes de Mesclagem. Isso reduz o número de linhas novas inseridas para controlar o histórico de agente e saída. Em vez disso, as mensagens de histórico anteriores com o mesmo status são atualizadas para as novas informações de histórico. Aumente os níveis detalhados de teste, monitoração e depuração, de forma a obter o máximo possível de informações sobre a atividade do agente.  
  
-   Use o parâmetro **–MaxBCPThreads** do Agente de Instantâneo, Agente de Mesclagem e Agente de Distribuição (o número de threads especificado não deve exceder o número de processadores no computador). Esse parâmetro especifica o número de operações de cópia em massa que podem ser executadas em paralelo quando o instantâneo é criado e aplicado.  
  
-   Use o parâmetro **–UseInprocLoader** do Agente de Distribuição e do Agente de Mesclagem (esse parâmetro não pode ser usado se as tabelas publicadas incluírem colunas XML). Esse parâmetro faz o agente usar o comando BULK INSERT quando o instantâneo for aplicado.  
  
 Os parâmetros de agente podem ser especificados em perfis de agente e na linha de comando. Para obter mais informações, consulte:  
  
-   [Trabalhar com perfis do Agente de Replicação](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
-   [Exibir e modificar parâmetros do prompt de comando de agentes de replicação &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
-   [Replication Agent Executables Concepts](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
  
