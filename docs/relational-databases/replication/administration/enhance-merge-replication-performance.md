---
title: Aprimorar o desempenho de replicação de mesclagem | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publications [SQL Server replication], design and performance
- designing databases [SQL Server], replication performance
- Merge Agent, performance
- snapshots [SQL Server replication], performance considerations
- merge replication performance [SQL Server replication]
- subscriptions [SQL Server replication], performance considerations
- performance [SQL Server replication], merge replication
- agents [SQL Server replication], performance
ms.assetid: f929226f-b83d-4900-a07c-a62f64527c7f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 261f22847c8b397d57ff5f732ea4d97091895daa
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67939209"
---
# <a name="enhance-merge-replication-performance"></a>Aprimorar o desempenho de replicação de mesclagem
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Após considerar as dicas para o desempenho geral descritas em [Aprimorando o Desempenho Geral da Replicação](../../../relational-databases/replication/administration/enhance-general-replication-performance.md), considere estas áreas adicionais específicas da replicação de mesclagem.  
  
## <a name="database-design"></a>Design de banco de dados  
  
-   Colunas de índice usadas em filtros de linha e filtros de junção.  
  
     Quando usar um filtro de linha em um artigo publicado, crie um índice em cada uma das colunas usadas na cláusula WHERE do filtro. Sem um índice, o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] precisa ler cada linha da tabela para determinar se a linha deve ser incluída na partição. Com um índice, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] consegue localizar rapidamente quais as linhas que deverão ser incluídas. O processamento mais rápido ocorre se a replicação conseguir resolver inteiramente a cláusula WHERE do filtro do índice de modo autônomo.  
  
     Indexar todas as colunas usadas em filtros de junção também é importante. Cada vez que o Merge Agent é executado, ele pesquisa a tabela base para determinar quais as linhas da tabela pai e quais as linhas nas tabelas relacionadas estão incluídas na partição. Criar um índice em colunas unidas evita que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] precise ler cada linha da tabela todas as vezes que o Merge Agent for executado.  
  
     Para mais informações sobre filtragem, consulte [Filtrar dados publicados para replicação de mesclagem](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md).  
  
-   Considere tabelas supernormalizadas que incluam tipos de dados LOB (Large Object).  
  
     Quando a sincronização ocorre, o Merge Agent poderá precisar ler e transferir a linha de dados inteira de um Publicador ou Assinante. Se a linha contiver colunas que usam LOBs, esse processo poderá precisar alocar memória adicional e comprometer o desempenho negativamente, embora essas colunas possam não ter sido atualizadas. Para reduzir a probabilidade de ocorrer esse comprometimento no desempenho, considere colocar colunas LOB em uma tabela separada, usando uma relação um para um no resto dos dados de linha. Os tipos de dados **text**, **ntext**e **image** são preteridos. Se incluir LOBs, recomendamos o uso dos tipos de dados **varchar(max)** , **nvarchar(max)** , **varbinary(max)** , respectivamente.  
  
## <a name="publication-design"></a>Design de publicação  
  
-   Use um nível de compatibilidade de publicação de 90RTM ([!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou uma versão posterior).  
  
     Exceto se um ou mais Assinantes usarem uma versão diferente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], especifique que a publicação deve oferecer suporte somente para o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou para uma versão posterior. Isso permite à publicação beneficiar-se de novos recursos e otimizações de desempenho.  
  
-   Use as configurações de retenção da publicação apropriadas.  
  
     O período de retenção da publicação, que é a quantidade máxima de tempo antes que a assinatura tenha de ser sincronizada, determina por quanto tempo os metadados de controle são armazenados. Um valor alto pode afetar armazenamento e o desempenho do processamento. Para obter mais informações sobre como definir o período de retenção de publicação, consulte [Subscription Expiration and Deactivation](../../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
-   Use artigos de somente download nessas tabelas que só são alteradas no Publicador. Para obter mais informações, consulte [Otimizar o desempenho da replicação de mesclagem com artigos somente para download](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
### <a name="filter-design-and-use"></a>Design e uso de filtro  
  
-   Limite a complexidade das cláusulas de filtro de linha.  
  
     Limitar a complexidade dos critérios de filtragem ajuda a melhorar o desempenho, quando o Merge Agent estiver avaliando alterações de linha para enviar aos Assinantes. Evite usar subseleções em cláusulas de filtro de linha de mesclagem. Em vez disso, considere o uso de filtros de junção, normalmente mais eficientes, quando usado para particionar dados em uma tabela baseada em uma cláusula de filtro de outra tabela. Para mais informações sobre filtragem, consulte [Filtrar dados publicados para replicação de mesclagem](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md).  
  
-   Use partições pré-computadas com filtros com parâmetros (esse recurso é usado por padrão). Para obter mais informações, consulte [Optimize Parameterized Filter Performance with Precomputed Partitions](../../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md) (Otimizar o desempenho do filtro parametrizado com partições pré-computadas).  
  
     Partições pré-computadas impõem vários limites no comportamento de filtragem. Se seu aplicativo não puder aderir a essas limitações, defina a opção **keep_partition_changes** como **True**, fornecendo um benefício de desempenho. Para obter mais informações, consulte [Filtros de linha com parâmetros](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
-   Use partições não sobrepostas se os dados forem filtrados, mas não forem compartilhados entre os usuários.  
  
     A replicação pode aperfeiçoar o desempenho para obter dados que não são compartilhados entre as partições ou assinaturas. Para obter mais informações, consulte [Filtros de linha com parâmetros](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
-   Não crie hierarquias de filtro de junção complexas.  
  
     Filtros de junção com cinco ou mais tabelas podem comprometer o desempenho significativamente durante o processamento de mesclagem. Se você estiver gerando filtros de junção de cinco ou mais tabelas, recomendamos que considere outras soluções:  
  
    -   Evite tabelas de filtragem que são, em sua maioria, tabelas de pesquisa, tabelas menores e tabelas que não estão sujeitas às alterações. Torne essas tabelas parte da publicação na sua totalidade. Recomendamos que você use filtros de junção apenas entre as tabelas que devem ser particionadas entre os Assinantes. Para obter mais informações, consulte [Join Filters](../../../relational-databases/replication/merge/join-filters.md).  
  
    -   Considere a desnormalização do design do banco de dados ou o uso de uma tabela de mapeamento, se houver um grande número de tabelas em uma junção. Por exemplo, se um vendedor necessita apenas dos dados de seus clientes, mas precisa de seis junções para associar um cliente ao vendedor, considere a adição de uma coluna à tabela do cliente, identificando o vendedor. Os dados do vendedor são redundantes, mas os custos de desnormalização de tabelas podem ser compensados pelos benefícios de desempenho para o particionamento de replicação.  
  
    -   Para melhorar o desempenho de partições pré-computadas, quando os lotes contêm muitas alterações de dados, projete seu aplicativo com atenção. Assegure-se de que as alterações de dados na tabela pai em um filtro de junção sejam feitas antes das alterações correspondentes nas tabelas filho.  
  
-   Defina a opção **join_unique_key** como **1** , se a lógica permitir.  
  
     Definir esse parâmetro como **1** indica que a relação entre tabelas pai e filho, em um filtro de junção, é de um para um ou de um para muitos. Selecione esse parâmetro como **1** , apenas se houver uma restrição na coluna de junção na tabela filho garantindo a exclusividade. Se o parâmetro for definido incorretamente como **1** , poderá ocorrer a não convergência dos dados. Para obter mais informações, consulte [Join Filters](../../../relational-databases/replication/merge/join-filters.md).  
  
-   Evite executar lotes com muitas alterações quando você usar partições pré-computadas.  
  
     Quando o Merge Agent é executado depois que você executou um lote, contendo lotes de alterações de dados, o agente tenta dividir o lote maior em lotes menores. Durante esse tempo, podem ser bloqueados outros processos do Merge Agent. Considere a redução do número de alterações em um lote e execute o Merge Agent entre os lotes. Se isso não puder ser feito, aumente o valor de **generation_leveling_threshold** para a publicação.  
  
## <a name="subscription-considerations"></a>Considerações sobre assinatura  
  
-   Divida os agendamentos de sincronização de assinatura.  
  
     Se um grande número de Assinantes sincronizarem com o Publicador, divida os agendamentos para que os Merge Agents sejam executados em momentos diferentes. Para obter mais informações, consulte [Specify Synchronization Schedules](../../../relational-databases/replication/specify-synchronization-schedules.md).  
  
## <a name="merge-agent-parameters"></a>Parâmetros do Merge Agent  
 Para obter informações sobre o Merge Agent e seus parâmetros, consulte [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md).  
  
-   Atualize todos os Assinantes com assinaturas pull do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou de uma versão posterior.  
  
     Atualizar o Assinante para o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou para uma versão posterior atualiza o Merge Agent usado pelas assinaturas do Assinante. Para se beneficiar dos muitos recursos e otimizações de desempenho, é necessário o Merge Agent do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou de uma versão posterior.  
  
-   Se uma assinatura for sincronizada em uma conexão rápida e as alterações forem enviadas do Publicador e do assinante, use o parâmetro **–ParallelUploadDownload** para o Agente de Mesclagem.  
  
     O[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] introduziu um novo parâmetro no Agente de Mesclagem: **–ParallelUploadDownload**. Definir esse parâmetro permite ao Merge Agent processar em paralelo as mudanças carregadas no Publicador e as baixadas no Assinante. É útil em ambientes com grandes volumes e largura de banda de rede alta. Os parâmetros de agente podem ser especificados em perfis de agente e na linha de comando. Para obter mais informações, consulte:  
  
    -   [Trabalhar com perfis do Agente de Replicação](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [Exibir e modificar parâmetros do prompt de comando de agentes de replicação &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Conceitos dos executáveis do Replication Agent](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
-   Considere aumentar o valor do parâmetro **-MakeGenerationInterval** , especialmente se a sincronização envolver mais carregamentos de Assinantes do que downloads para Assinantes.  
  
-   Quando sincronizar linhas de dados com um grande volume de dados, como linhas com colunas LOB, a sincronização da Web poderá necessitar de alocação de memória adicional e prejudicar o desempenho. Isso ocorre quando o Merge Agent gera uma mensagem XML contendo muitas linhas, com um grande volume de dados. Se o Merge Agent estiver consumindo muitos recursos durante a sincronização da Web, reduza o número de linhas enviadas em uma única mensagem, usando uma das seguintes opções:  
  
    -   Use o perfil do agente de vínculo lento para o Merge Agent. Para saber mais, confira [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
    -   Diminua os parâmetros **- DownloadGenerationsPerBatch** e **- UploadGenerationsPerBatch** do Agente de Mesclagem para um valor menor ou igual a 10. O valor padrão desses parâmetros é 50.  
  
## <a name="snapshot-considerations"></a>Considerações de instantâneo  
  
-   Crie uma coluna ROWGUIDCOL nas tabelas grandes, antes de gerar o instantâneo inicial.  
  
     A replicação de mesclagem requer que cada tabela publicada tenha uma coluna ROWGUIDCOL. Se a coluna ROWGUIDCOL não existir na tabela antes do Snapshot Agent criar arquivos de instantâneo inicial, o agente deve primeiro adicionar e popular a coluna ROWGUIDCOL. Para obter uma vantagem de desempenho ao gerar instantâneos, crie uma coluna ROWGUIDCOL em cada tabela antes de publicar. A coluna pode ter qualquer nome (**rowguid** é usado pelo Snapshot Agent, por padrão), mas deve ter as seguintes características de tipos de dados:  
  
    -   Dados do tipo UNIQUEIDENTIFIER.  
  
    -   Um padrão NEWSEQUENTIALID() ou NEWID(). NEWSEQUENTIALID() é o recomendado, pois pode fornecer um desempenho melhor ao fazer e controlar alterações.  
  
    -   O conjunto de propriedades ROWGUIDCOL.  
  
    -   Um índice exclusivo na coluna.  
  
-   Gere os instantâneos previamente e/ou permita que os Assinantes solicitem a geração e a aplicação de instantâneos, na primeira vez que fizerem a sincronização.  
  
     Use uma, ou ambas as opções, para fornecer instantâneos para publicações que usam filtros com parâmetros. Se você não especificar uma dessas opções, as assinaturas serão inicializadas usando uma série de instruções SELECT e INSERT, ao invés de usar o utilitário **bcp** , esse processo é muito mais lento. Para obter mais informações, consulte [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
## <a name="maintenance-and-monitoring-considerations"></a>Considerações sobre manutenção e monitoramento  
  
-   Esporadicamente, indexe novamente as tabelas do sistema de replicação de mesclagem.  
  
     Como parte da manutenção para replicação de mesclagem, verifique ocasionalmente o crescimento das tabelas do sistema associado à replicação de mesclagem: **MSmerge_contents**, **MSmerge_genhistory** e **MSmerge_tombstone**, **MSmerge_current_partition_mappings** e **MSmerge_past_partition_mappings**. Periodicamente, indexe novamente essas tabelas. Para obter mais informações, veja [Reorganizar e recriar índices](../../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
-   Monitore o desempenho de sincronização usando a guia **Histórico de Sincronização** no Replication Monitor.  
  
     Para a replicação de mesclagem, o Replication Monitor exibe as estatísticas detalhadas na guia **Histórico de Sincronizações** para cada artigo processado durante a sincronização, incluindo tempo gasto em cada fase do processamento (carregar alterações, baixar alterações e assim por diante). Ajuda a definir tabelas específicas que estão causando lentidão e é o melhor local para a solução de problemas de desempenho com assinaturas de mesclagem. Para obter mais informações sobre como exibir estatísticas detalhadas, confira [Exibir informações e executar tarefas usando o Replication Monitor](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
  
