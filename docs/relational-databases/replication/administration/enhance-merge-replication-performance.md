---
title: "Aprimorar o desempenho de replica&#231;&#227;o de mesclagem | Microsoft Docs"
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
  - "publicações [replicação do SQL Server], design e desempenho"
  - "criando bancos de dados [SQL Server], desempenho de replicação"
  - "Agente de Mesclagem, desempenho"
  - "instantâneos [replicação do SQL Server], considerações sobre desempenho"
  - "desempenho de replicação de mesclagem [replicação do SQL Server]"
  - "assinaturas [replicação do SQL Server], considerações sobre desempenho"
  - "desempenho [replicação do SQL Server], replicação de mesclagem"
  - "agentes [replicação do SQL Server], desempenho"
ms.assetid: f929226f-b83d-4900-a07c-a62f64527c7f
caps.latest.revision: 47
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 47
---
# Aprimorar o desempenho de replica&#231;&#227;o de mesclagem
  Após considerar as dicas de desempenho geral descritas em [aprimorando o desempenho de replicação geral](../../../relational-databases/replication/administration/enhance-general-replication-performance.md), considere estas áreas adicionais específicas para replicação de mesclagem.  
  
## Design de banco de dados  
  
-   Colunas de índice usadas em filtros de linha e filtros de junção.  
  
     Quando usar um filtro de linha em um artigo publicado, crie um índice em cada uma das colunas usadas na cláusula WHERE do filtro. Sem um índice, [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] precisa ler cada linha na tabela para determinar se a linha deve ser incluída na partição. Com um índice, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] consegue localizar rapidamente quais as linhas que deverão ser incluídas. O processamento mais rápido ocorre se a replicação conseguir resolver inteiramente a cláusula WHERE do filtro do índice de modo autônomo.  
  
     Indexar todas as colunas usadas em filtros de junção também é importante. Cada vez que o Merge Agent é executado, ele pesquisa a tabela base para determinar quais as linhas da tabela pai e quais as linhas nas tabelas relacionadas estão incluídas na partição. Criar um índice em colunas unidas evita que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] precise ler cada linha da tabela todas as vezes que o Merge Agent for executado.  
  
     Para obter mais informações sobre filtragem, consulte [Filtrar dados publicados para replicação de mesclagem](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md).  
  
-   Considere tabelas supernormalizadas que incluam tipos de dados LOB (Large Object).  
  
     Quando a sincronização ocorre, o Merge Agent poderá precisar ler e transferir a linha de dados inteira de um Publicador ou Assinante. Se a linha contiver colunas que usam LOBs, esse processo poderá precisar alocar memória adicional e comprometer o desempenho negativamente, embora essas colunas possam não ter sido atualizadas. Para reduzir a probabilidade de ocorrer esse comprometimento no desempenho, considere colocar colunas LOB em uma tabela separada, usando uma relação um para um no resto dos dados de linha. Os tipos de dados **text**, **ntext**e **image** são preteridos. Se você incluir LOBs, recomendamos que você use os tipos de dados **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, respectivamente.  
  
## Design de publicação  
  
-   Use um nível de compatibilidade de publicação de 90RTM ([!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou uma versão posterior).  
  
     A menos que um ou mais assinantes usam uma versão diferente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], especifica que a publicação deve oferecer suporte somente [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou uma versão posterior. Isso permite à publicação beneficiar-se de novos recursos e otimizações de desempenho.  
  
-   Use as configurações de retenção da publicação apropriadas.  
  
     O período de retenção da publicação, que é a quantidade máxima de tempo antes que a assinatura tenha de ser sincronizada, determina por quanto tempo os metadados de controle são armazenados. Um valor alto pode afetar armazenamento e o desempenho do processamento. Para obter mais informações sobre como definir o período de retenção da publicação, consulte [desativação e expiração de assinatura](../../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
-   Use artigos de somente download nessas tabelas que só são alteradas no Publicador. Para obter mais informações, consulte [otimizar o desempenho de replicação de mesclagem com artigos Download-Only](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
### Design e uso de filtro  
  
-   Limite a complexidade das cláusulas de filtro de linha.  
  
     Limitar a complexidade dos critérios de filtragem ajuda a melhorar o desempenho, quando o Merge Agent estiver avaliando alterações de linha para enviar aos Assinantes. Evite usar subseleções em cláusulas de filtro de linha de mesclagem. Em vez disso, considere o uso de filtros de junção, normalmente mais eficientes, quando usado para particionar dados em uma tabela baseada em uma cláusula de filtro de outra tabela. Para obter mais informações sobre filtragem, consulte [Filtrar dados publicados para replicação de mesclagem](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md).  
  
-   Use partições pré-computadas com filtros com parâmetros (esse recurso é usado por padrão). Para obter mais informações, consulte [otimizar desempenho de filtro parametrizado com partições pré-calculadas](../../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md).  
  
     Partições pré-computadas impõem vários limites no comportamento de filtragem. Se seu aplicativo não puder aderir a essas limitações, defina o **keep_partition_changes** opção **True**, que fornece um benefício de desempenho. Para obter mais informações, consulte [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
-   Use partições não sobrepostas se os dados forem filtrados, mas não forem compartilhados entre os usuários.  
  
     A replicação pode aperfeiçoar o desempenho para obter dados que não são compartilhados entre as partições ou assinaturas. Para obter mais informações, consulte [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
-   Não crie hierarquias de filtro de junção complexas.  
  
     Filtros de junção com cinco ou mais tabelas podem comprometer o desempenho significativamente durante o processamento de mesclagem. Se você estiver gerando filtros de junção de cinco ou mais tabelas, recomendamos que considere outras soluções:  
  
    -   Evite tabelas de filtragem que são, em sua maioria, tabelas de pesquisa, tabelas menores e tabelas que não estão sujeitas às alterações. Torne essas tabelas parte da publicação na sua totalidade. Recomendamos que você use filtros de junção apenas entre as tabelas que devem ser particionadas entre os Assinantes. Para obter mais informações, consulte [Join Filters](../../../relational-databases/replication/merge/join-filters.md).  
  
    -   Considere a desnormalização do design do banco de dados ou o uso de uma tabela de mapeamento, se houver um grande número de tabelas em uma junção. Por exemplo, se um vendedor necessita apenas dos dados de seus clientes, mas precisa de seis junções para associar um cliente ao vendedor, considere a adição de uma coluna à tabela do cliente, identificando o vendedor. Os dados do vendedor são redundantes, mas os custos de desnormalização de tabelas podem ser compensados pelos benefícios de desempenho para o particionamento de replicação.  
  
    -   Para melhorar o desempenho de partições pré-computadas, quando os lotes contêm muitas alterações de dados, projete seu aplicativo com atenção. Assegure-se de que as alterações de dados na tabela pai em um filtro de junção sejam feitas antes das alterações correspondentes nas tabelas filho.  
  
-   Definir o **join_unique_key** opção **1** se a lógica permitir.  
  
     Definir esse parâmetro para **1** indica que a relação entre as tabelas pai e filho em um filtro de associação é um para muitos ou um para um. Apenas defina esse parâmetro **1** se você tiver uma restrição na coluna de junção na tabela filho que garanta a exclusividade. Se o parâmetro for definido como **1** incorretamente, pode ocorrer não convergência de dados. Para obter mais informações, consulte [Join Filters](../../../relational-databases/replication/merge/join-filters.md).  
  
-   Evite executar lotes com muitas alterações quando você usar partições pré-computadas.  
  
     Quando o Merge Agent é executado depois que você executou um lote, contendo lotes de alterações de dados, o agente tenta dividir o lote maior em lotes menores. Durante esse tempo, podem ser bloqueados outros processos do Merge Agent. Considere a redução do número de alterações em um lote e execute o Merge Agent entre os lotes. Se isso não pode ser feito, aumente o valor de **generation_leveling_threshold** para a publicação.  
  
## Considerações sobre assinatura  
  
-   Divida os agendamentos de sincronização de assinatura.  
  
     Se um grande número de Assinantes sincronizarem com o Publicador, divida os agendamentos para que os Merge Agents sejam executados em momentos diferentes. Para obter mais informações, consulte [Specify Synchronization Schedules](../../../relational-databases/replication/specify-synchronization-schedules.md).  
  
## Parâmetros do Merge Agent  
 Para obter informações sobre o agente de mesclagem e seus parâmetros, consulte [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md).  
  
-   Atualize todos os assinantes para assinaturas pull para [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou uma versão posterior.  
  
     Atualizar o assinante para [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou uma versão posterior atualiza o Merge Agent usado pelas assinaturas do assinante. Para se beneficiar dos muitos recursos e otimizações de desempenho, é necessário o Merge Agent do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou de uma versão posterior.  
  
-   Se uma assinatura for sincronizada em uma conexão rápida e as alterações são enviadas do publicador e assinante, use o **– ParallelUploadDownload** parâmetro para o Merge Agent.  
  
     [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] introduziu um novo parâmetro de agente de mesclagem: **– ParallelUploadDownload**. Definir esse parâmetro permite ao Merge Agent processar em paralelo as mudanças carregadas no Publicador e as baixadas no Assinante. É útil em ambientes com grandes volumes e largura de banda de rede alta. Os parâmetros de agente podem ser especificados em perfis de agente e na linha de comando. Para obter mais informações, consulte:  
  
    -   [Trabalhar com perfis do agente de replicação](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [Exibir e modificar parâmetros de Prompt de comando do agente de replicação e 40; SQL Server Management Studio e 41;](../../../relational-databases/replication/agents/view and modify replication agent command prompt parameters.md)  
  
    -   [Conceitos dos executáveis do Replication Agent](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
-   Considere aumentar o valor de **- MakeGenerationInterval** parâmetro, especialmente se a sincronização envolver mais carregamentos de assinantes que downloads para assinantes.  
  
-   Quando sincronizar linhas de dados com um grande volume de dados, como linhas com colunas LOB, a sincronização da Web poderá necessitar de alocação de memória adicional e prejudicar o desempenho. Isso ocorre quando o Merge Agent gera uma mensagem XML contendo muitas linhas, com um grande volume de dados. Se o Merge Agent estiver consumindo muitos recursos durante a sincronização da Web, reduza o número de linhas enviadas em uma única mensagem, usando uma das seguintes opções:  
  
    -   Use o perfil do agente de vínculo lento para o Merge Agent. Para saber mais, confira [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
    -   Diminuir o **- DownloadGenerationsPerBatch** e **- UploadGenerationsPerBatch** parâmetros para o Merge Agent para um valor de 10 ou menos. O valor padrão desses parâmetros é 50.  
  
## Considerações de instantâneo  
  
-   Crie uma coluna ROWGUIDCOL nas tabelas grandes, antes de gerar o instantâneo inicial.  
  
     A replicação de mesclagem requer que cada tabela publicada tenha uma coluna ROWGUIDCOL. Se a coluna ROWGUIDCOL não existir na tabela antes do Snapshot Agent criar arquivos de instantâneo inicial, o agente deve primeiro adicionar e popular a coluna ROWGUIDCOL. Para obter uma vantagem de desempenho ao gerar instantâneos, crie uma coluna ROWGUIDCOL em cada tabela antes de publicar. A coluna pode ter qualquer nome (**rowguid** é usado pelo agente de instantâneo por padrão), mas deve ter os seguintes dados do tipo características:  
  
    -   Dados do tipo UNIQUEIDENTIFIER.  
  
    -   Um padrão NEWSEQUENTIALID() ou NEWID(). NEWSEQUENTIALID() é o recomendado, pois pode fornecer um desempenho melhor ao fazer e controlar alterações.  
  
    -   O conjunto de propriedades ROWGUIDCOL.  
  
    -   Um índice exclusivo na coluna.  
  
-   Gere os instantâneos previamente e/ou permita que os Assinantes solicitem a geração e a aplicação de instantâneos, na primeira vez que fizerem a sincronização.  
  
     Use uma, ou ambas as opções, para fornecer instantâneos para publicações que usam filtros com parâmetros. Se você não especificar uma dessas opções, as assinaturas serão inicializadas usando uma série de instruções SELECT e INSERT, ao invés de usar o utilitário **bcp** , esse processo é muito mais lento. Para obter mais informações, consulte [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
## Considerações sobre manutenção e monitoramento  
  
-   Esporadicamente, indexe novamente as tabelas do sistema de replicação de mesclagem.  
  
     Como parte da manutenção de replicação de mesclagem, verifique periodicamente o crescimento das tabelas do sistema associados com a replicação de mesclagem: **MSmerge_contents**, **MSmerge_genhistory**, e **MSmerge_tombstone**, **MSmerge_current_partition_mappings**, e **MSmerge_past_partition_mappings**. Periodicamente, indexe novamente essas tabelas. Para obter mais informações, consulte [reorganizar e recriar índices](../../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
-   Monitorar desempenho de sincronização usando o **histórico de sincronização** guia no Replication Monitor.  
  
     Para replicação de mesclagem, o Replication Monitor exibe as estatísticas detalhadas no **histórico de sincronização** guia para cada artigo processado durante a sincronização, incluindo a quantidade de tempo gasto em cada fase de processamento (carregar alterações, baixar alterações e assim por diante). Ajuda a definir tabelas específicas que estão causando lentidão e é o melhor local para a solução de problemas de desempenho com assinaturas de mesclagem. Para obter mais informações sobre como exibir estatísticas detalhadas, consulte [Exibir informações e executar tarefas para os agentes associados a uma assinatura & #40. Monitor de replicação e 41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
  