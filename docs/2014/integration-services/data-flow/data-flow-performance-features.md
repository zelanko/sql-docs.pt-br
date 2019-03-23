---
title: Recursos de desempenho de fluxo de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Aggregate transformation [Integration Services]
- Integration Services packages, performance
- performance [Integration Services]
- data flow [Integration Services], troubleshooting
- SQL Server Integration Services packages, performance
- loading data
- control flow [Integration Services], troubleshooting
- SSIS packages, performance
- packages [Integration Services], performance
- queries [Integration Services], troubleshooting
- sorting data [Integration Services]
- aggregations [Integration Services]
ms.assetid: c4bbefa6-172b-4547-99a1-a0b38e3e2b05
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 030318d65d469546f946679e9c9173bfdb1a3f36
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58392774"
---
# <a name="data-flow-performance-features"></a>Recursos de desempenho de fluxo de dados
  Este tópico fornece sugestões sobre como projetar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para evitar problemas comuns de desempenho. Este tópico também provê informações sobre recursos e ferramentas que podem ser usados para diagnosticar o desempenho de pacotes.  
  
## <a name="configuring-the-data-flow"></a>Configurando o Fluxo de Dados  
 Para configurar a tarefa Fluxo de Dados para um melhor desempenho, você pode configurar as propriedades da tarefa, ajustar o tamanho do buffer e configurar o pacote para execução paralela.  
  
### <a name="configure-the-properties-of-the-data-flow-task"></a>Configurar Propriedades da Tarefa Fluxo de Dados  
  
> [!NOTE]  
>  As propriedades discutidas nesta seção devem ser definidas separadamente para cada tarefa Fluxo de Dados em um pacote.  
  
 Todas as propriedades a seguir da tarefa Fluxo de Dados podem ser configuradas com relação ao desempenho:  
  
-   Especifique os locais para armazenamento temporário dos dados do buffer (propriedade BufferTempStoragePath) e das colunas que contêm dados BLOB (objeto binário grande) (propriedade BLOBTempStoragePath). Por padrão, essas propriedades contêm os valores das variáveis de ambiente TEMP e TMP. Talvez você queira especificar outras pastas para colocar os arquivos temporários em um disco rígido mais rápido ou diferente ou para espalhá-los por várias unidades. Você pode especificar vários diretórios delimitando os nomes de diretório com ponto-e-vírgula.  
  
-   Define o tamanho padrão do buffer usado pela tarefa, definindo a propriedade DefaultBufferSize, e defina o número máximo de linhas em cada buffer, definindo a propriedade DefaultBufferMaxRows. O tamanho padrão do buffer é 10 megabytes; o tamanho máximo é de 100 megabytes. O número de máximo padrão de linhas é 10.000.  
  
-   Defina o número de threads que a tarefa pode usar durante a execução, definindo a propriedade EngineThreads. Esta propriedade fornece uma sugestão ao mecanismo de fluxo de dados com relação ao número de threads que será usado. O padrão é 10, com um valor mínimo de 3. Entretanto, o mecanismo não utilizará mais threads do que o necessário, independente do valor desta propriedade. O mecanismo também pode usar mais threads que o especificado nesta propriedade, se necessário, para evitar assuntos de simultaneidade.  
  
-   Indique se a tarefa Fluxo de Dados executa em modo otimizado (propriedade RunInOptimizedMode). O modo otimizado melhora o desempenho removendo colunas, saídas e componentes não utilizados do fluxo de dados.  
  
    > [!NOTE]  
    >  Uma propriedade com o mesmo nome, RunInOptimizedMode, pode ser definida no nível do projeto em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para indicar que a tarefa Fluxo de Dados é executada no modo otimizado durante a depuração. Esta propriedade de projeto substitui a propriedade RunInOptimizedMode das tarefas Fluxo de Dados no momento da criação.  
  
### <a name="adjust-the-sizing-of-buffers"></a>Ajustar o tamanho dos buffers  
 O mecanismo de fluxo de dados inicia a tarefa de dimensionamento de seus buffers, calculando o tamanho estimado de uma única linha de dados. Em seguida, ele multiplica o tamanho estimado de uma linha pelo valor de DefaultBufferMaxRows para obter um valor de trabalho preliminar para o tamanho do buffer.  
  
-   Se o resultado for maior que o valor de DefaultBufferSize, o mecanismo reduzirá o número de linhas.  
  
-   Se o resultado for menor que o tamanho do buffer mínimo calculado interiormente, o mecanismo aumentará o número de linhas.  
  
-   Se o resultado estiver entre o tamanho do buffer mínimo e o valor de DefaultBufferSize, o mecanismo dimensionará o buffer o mais próximo possível do tamanho da linha estimado vezes o valor de DefaultBufferMaxRows.  
  
 Quando você começa a testar o desempenho das suas tarefas de fluxo de dados, use os valores padrão para DefaultBufferSize e DefaultBufferMaxRows. Habilite o registro em cada tarefa de fluxo de dados e selecione o evento BufferSizeTuning para ver quantas linhas estão em cada buffer.  
  
 Antes de começar a ajustar o tamanho dos buffers, o aprimoramento mais importante que pode ser feito é reduzir o tamanho de cada linha de dados, removendo colunas desnecessárias e configurando os tipos de dados corretamente.  
  
 Para determinar o número adequado de buffers e seus respectivos tamanhos, use os valores de DefaultBufferSize e DefaultBufferMaxRows durante o desempenho de monitoramento e as informações reportadas pelo evento BufferSizeTuning.  
  
 Não aumente o tamanho do buffer para o ponto em que a paginação para o disco começa a acontecer. A paginação para o disco impede mais o desempenho do que o tamanho do buffer não otimizado. Para determinar se a paginação está ocorrendo, monitore o contador de desempenho "Buffers em spool" no snap-in Desempenho do MMC (Console de Gerenciamento [!INCLUDE[msCoName](../../includes/msconame-md.md)] ).  
  
### <a name="configure-the-package-for-parallel-execution"></a>Configurar o pacote para execução paralela  
 A execução paralela melhora desempenho em computadores com vários processadores lógicos ou físicos. Para suportar a execução paralela de diferentes tarefas no pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa duas propriedades: `MaxConcurrentExecutables` e `EngineThreads`.  
  
#### <a name="the-maxconcurrentexcecutables-property"></a>Propriedade MaxConcurrentExcecutables  
 A propriedade `MaxConcurrentExecutables` é uma propriedade do próprio pacote. Esta propriedade define quantas tarefas podem ser executadas simultaneamente. O valor padrão é -1, que significa o número de processadores físicos ou lógicos mais 2.  
  
 Para compreender como esta propriedade trabalha, considere um pacote de exemplo que tenha três tarefas Fluxo de Dados. Se você definir `MaxConcurrentExecutables` como 3, todas as três tarefas Fluxo de Dados poderão ser executadas simultaneamente. Entretanto, assuma que cada tarefa Fluxo de Dados tenha 10 árvores de execução de origem para destino. Se você definir `MaxConcurrentExecutables` como 3, não será possível garantir que a execução das árvores dentro de cada Fluxo de Dados será executada na forma paralela.  
  
#### <a name="the-enginethreads-property"></a>Propriedade EngineThreads  
 A propriedade `EngineThreads` é uma propriedade de cada tarefa Fluxo de Dados. Esta propriedade define quantos threads o mecanismo de fluxo de dados poderá criar e executar na forma paralela. A propriedade `EngineThreads` se aplica igualmente a ambos os threads de origem que o mecanismo de fluxo de dados cria para origens e os threads de trabalho que o mecanismo cria para transformações e destinos. Portanto, definir `EngineThreads` como 10 significa que o mecanismo pode criar até dez threads de origem e até dez threads de trabalho.  
  
 Para compreender como esta propriedade trabalha, considere o pacote de exemplo com três tarefas Fluxo de Dados. Cada tarefa Fluxo de Dados contém dez árvores de execução de origem para destino. Se você definir EngineThreads como 10 em cada tarefa Fluxo de Dados, todas as 30 árvores de execução poderão ser executadas simultaneamente.  
  
> [!NOTE]  
>  Existe uma discussão sobre threading que traz mais informações. Entretanto, a regra geral indica para não executar mais threads na forma paralela que o número de processadores disponíveis. Executar mais threads que o número de processadores disponíveis pode impedir o desempenho devido à alternância de contexto frequente entre os threads.  
  
## <a name="configuring-individual-data-flow-components"></a>Configurando componentes individuais de Fluxo de Dados  
 Para configurar componentes individuais de fluxo de dados para um melhor desempenho, existem algumas instruções gerais que podem ser consideradas. Também há instruções específicas para cada tipo de componente de fluxo de dados: origem, transformação e destino.  
  
### <a name="general-guidelines"></a>Instruções gerais  
 Independente do componente de fluxo de dados, existem duas instruções gerais que devem ser seguidas para melhorar o desempenho: otimizar consultas e evitar cadeias de caracteres desnecessárias.  
  
#### <a name="optimize-queries"></a>Otimizar Consultas  
 Um determinado número de componentes de fluxo de dados usa consultas, tanto quando extraem dados das origens quanto em operações de pesquisa para criar tabelas de referências. A consulta padrão usa a sintaxe SELECT * FROM \<tableName>. Este tipo de consulta retorna todas as colunas na tabela de origem. Considerando que você tenha todas as colunas disponíveis no momento da criação, é possível escolher qualquer coluna como uma coluna de pesquisa, passagem ou origem. No entanto, depois de selecionar as colunas que serão usadas, será preciso revisar a consulta para incluir somente as colunas selecionadas. Remover as colunas supérfluas faz com que o fluxo de dados torne-se mais eficaz, pois quanto menor for o número de colunas, menor será a linha criada. Uma linha pequena significa que mais linhas podem ser ajustadas no buffer e o trabalho para processar todas as linhas no conjunto de dados é menor.  
  
 Para construir uma consulta, é preciso inseri-la ou usar o Construtor de Consultas.  
  
> [!NOTE]  
>  Ao executar um pacote no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], a guia Progresso do Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] indicará alguns avisos. Esses avisos incluem a identificação da coluna de dados que uma origem disponibiliza para o fluxo de dados, mas que não é usada de forma subsequente pelos componentes de fluxo de dados do downstream. Você pode usar a propriedade `RunInOptimizedMode` para remover essas colunas automaticamente.  
  
#### <a name="avoid-unnecessary-sorting"></a>Evitar classificação desnecessária  
 A classificação é inerentemente uma operação lenta e, evitando uma classificação desnecessária, você aumenta o desempenho do fluxo de dados do pacote.  
  
 Algumas vezes os dados de origem já foram classificados antes de serem usados por um componente do downstream. Essa pré-classificação pode ocorrer quando a consulta SELECT usar uma cláusula ORDER BY ou quando os dados forem inseridos na origem na ordem classificada. Para os dados de origem pré-classificados, é possível mencionar uma dica de que a classificação dos dados é viável, evitando, assim, o uso de uma transformação Classificar para atender aos requisitos de classificação de determinadas transformações de downstream. (Por exemplo, as transformações Mesclar e Mesclar Junção exigem entradas classificadas.) Para fornecer uma dica de que os dados são classificados, execute as seguintes tarefas:  
  
-   Defina a propriedade `IsSorted` na saída de um componente de fluxo de dados de upstream como `True`.  
  
-   Especifique as colunas de chave de classificação nas quais os dados serão classificados.  
  
 Para obter mais informações, consulte [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
 Se precisar classificar os dados no fluxo de dados, melhore o desempenho fazendo com que o fluxo de dados use o menor número possível de operações de classificação. Por exemplo, o fluxo de dados usa uma transformação Multicast para copiar o conjunto de dados. Classifique o conjunto de dados uma vez antes de a transformação Multicast ser executada em vez de classificar as diversas saídas após a transformação.  
  
 Para obter mais informações, consulte [Sort Transformation](transformations/sort-transformation.md), [Merge Transformation](transformations/merge-transformation.md), [Merge Join Transformation](transformations/merge-join-transformation.md)e [Multicast Transformation](transformations/multicast-transformation.md).  
  
### <a name="sources"></a>Origens  
  
#### <a name="ole-db-source"></a>Origem de OLE DB  
 Ao usar uma origem de OLE DB para recuperar os dados de uma exibição, selecione "Comando SQL" como o modo de acesso aos dados e insira uma instrução SELECT. Acessar os dados usando uma instrução SELECT faz com que a "Tabela ou Exibição" selecionada seja executada melhor no modo de acesso de dados.  
  
### <a name="transformations"></a>Transformações  
 Nesta seção, use as sugestões para melhorar o desempenho das transformações Agregação, Pesquisa Difusa, Agrupamento Difuso, Pesquisa, Mesclar Junção e Dimensão de Alteração Lenta.  
  
#### <a name="aggregate-transformation"></a>Transformação Agregação  
 A transformação Agregação inclui as propriedades `Keys`, `KeysScale`, `CountDistinctKeys` e `CountDistinctScale`. Essas propriedades melhoram o desempenho permitindo que transformação pré-aloque a quantidade de memória necessária para os dados armazenados em cache pela transformação. Se você souber o número exato ou aproximado de grupos que são esperados como resultado de uma **Group by** operação, defina as `Keys` e `KeysScale` propriedades, respectivamente. Se você souber o número exato ou aproximado de valores distintos que são esperados como resultado de uma **contagem distinta** operação, defina as `CountDistinctKeys` e `CountDistinctScale` propriedades, respectivamente.  
  
 Se tiver criado várias agregações em um fluxo de dados, considere a criação de várias agregações que usam uma transformação Agregação em vez de criar várias transformações. Esse procedimento melhora o desempenho quando uma agregação for um subconjunto de outra agregação porque a transformação pode otimizar o armazenamento interno e analisar os dados de entrada apenas uma vez. Por exemplo, se uma agregação usa uma cláusula GROUP BY e uma agregação AVG, combiná-las em uma transformação pode melhorar o desempenho. Entretanto, executar várias agregações dentro de uma transformação Agregação serializa as operações de agregação e pode não melhorar o desempenho quando várias agregações devem ser computadas de forma independente.  
  
#### <a name="fuzzy-lookup-and-fuzzy-grouping-transformations"></a>Transformações Pesquisa Difusa e Agrupamento Difuso  
 Para obter informações mais detalhadas sobre as transformações Pesquisa Difusa e Agrupamento Difuso, consulte a documentação [Fuzzy Lookup and Fuzzy Grouping in SQL Server Integration Services 2005](https://go.microsoft.com/fwlink/?LinkId=96604)(em inglês).  
  
#### <a name="lookup-transformation"></a>transformação Pesquisa  
 Minimize o tamanho dos dados de referência na memória usando uma instrução SELECT que seja capaz de pesquisar somente as colunas necessárias. Esta é uma opção melhor do que selecionar uma tabela ou exibição inteira, que retorna uma quantidade grande de dados desnecessários.  
  
#### <a name="merge-join-transformation"></a>Merge Join Transformation  
 Não é mais preciso configurar o valor da propriedade `MaxBuffersPerInput`, pois a Microsoft fez alterações que reduzem o risco de a transformação Junção de Mesclagem consumir memória excessiva. Esse problema algumas vezes ocorria quando as várias entradas da Junção de Mesclagem geravam dados a taxas irregulares.  
  
#### <a name="slowly-changing-dimension-transformation"></a>transformação Dimensão de Alteração Lenta  
 O Assistente para Dimensão Alteração Lenta e a transformação Dimensão Alteração Lenta são ferramentas de uso geral que atendem às necessidades da maioria dos usuários. Entretanto, o fluxo de dados gerado pelo assistente não é otimizado para o desempenho.  
  
 Normalmente, os componentes mais lentos na transformação Dimensão Alteração Lenta são as transformações Comando de OLE DB que executam UPDATEs (atualizações) em apenas uma linha por vez. Portanto, a forma mais eficaz de melhorar o desempenho da transformação Dimensão Alteração Lenta é substituir as transformações Comando de OLE DB. Essas transformações podem ser substituídas por componentes de destino que salvam todas as linhas que serão atualizadas para uma tabela de preparação. Por isso, é possível adicionar uma tarefa Executar SQL que desenvolva uma única instrução UPDATE Transact-SQL com base no conjunto em todas as linhas ao mesmo tempo.  
  
 Usuários avançados podem criar um fluxo de dados personalizado para alterar o processamento da dimensão que é otimizada lentamente em dimensões maiores. Para uma discussão e exemplo dessa abordagem, consulte a seção "cenário de dimensão exclusiva" no white paper, [Project REAL: Business Intelligence ETL Design Practices](https://go.microsoft.com/fwlink/?LinkId=96602).  
  
### <a name="destinations"></a>Destinos  
 Para atingir um melhor desempenho com destinos, considere o uso de um destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e teste o desempenho do destino.  
  
#### <a name="sql-server-destination"></a>destino do SQL Server  
 Quando um pacote carregar dados para uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no mesmo computador, use um destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Este destino é otimizado para carregamento em massa de alta velocidade.  
  
#### <a name="testing-the-performance-of-destinations"></a>Testando o desempenho de destinos  
 Você pode achar que salvar os dados em destinos leva mais tempo que o esperado. Para identificar se a lentidão é causada por uma incapacidade do destino em processar dados rápido o suficiente, você pode substituir temporariamente o destino por uma transformação Contagem de Linhas. Se a taxa de transferência melhorar significativamente, é provável que o destino que está carregando os dados esteja causando a lentidão.  
  
### <a name="review-the-information-on-the-progress-tab"></a>Analisar as informações na guia Progresso  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] fornece informações adicionais sobre o fluxo de controle e o fluxo de dados quando você executa um pacote no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. A guia **Progresso** lista as tarefas e os contêineres em ordem de execução e inclui horários de início e término, avisos e mensagens de erro para cada tarefa e contêiner, inclusive do próprio pacote. Ela também lista os componentes de fluxo de dados em ordem de execução e inclui informações sobre o progresso exibidas como um percentual completo, e o número de linhas processadas.  
  
 Para habilitar ou desabilitar a exibição de mensagens na guia **Progresso** , marque ou desmarque a opção **Depurar Relatório do Progresso** no menu **SSIS** . Desabilitar o relatório do progresso pode ajudar a melhorar o desempenho durante a execução de um pacote complexo no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
 **Artigos e postagens de blog**  
  
-   Artigo técnico, [SQL Server 2005 Integration Services: A Strategy for Performance](https://go.microsoft.com/fwlink/?LinkId=98899), em technet.microsoft.com  
  
-   Artigo técnico, [Integration Services: Performance Tuning Techniques](https://go.microsoft.com/fwlink/?LinkId=98900), em technet.microsoft.com  
  
-   Artigo técnico sobre como [aumentar o rendimento dos pipelines dividindo transformações síncronas em várias tarefas](http://sqlcat.com/technicalnotes/archive/2010/08/18/increasing-throughput-of-pipelines-by-splitting-synchronous-transformations-into-multiple-tasks.aspx), em sqlcat.com  
  
-   Artigo técnico, [The Data Loading Performance Guide](https://go.microsoft.com/fwlink/?LinkId=220816), em msdn.microsoft.com.  
  
-   Artigo técnico, [We Loaded 1TB in 30 Minutes with SSIS, and So Can You](https://go.microsoft.com/fwlink/?LinkId=220817), em msdn.microsoft.com.  
  
-   Artigo técnico, [Top 10 SQL Server Integration Services Best Practices](https://go.microsoft.com/fwlink/?LinkId=220818), em sqlcat.com.  
  
-   Artigo técnico e exemplo, [O "Distribuidor de Dados Equilibrado" para SSIS](https://go.microsoft.com/fwlink/?LinkId=220822), em sqlcat.com.  
  
-   Postagem do blog, [Solução de problemas de desempenho do pacote SSIS](https://go.microsoft.com/fwlink/?LinkId=238156), no blogs.msdn.com.  
  
 **Vídeos**  
  
-   Série de vídeos, [Design e ajuste para desempenho dos seus pacotes SSIS no Enterprise (Série de vídeo do SQL)](https://go.microsoft.com/fwlink/?LinkId=400878)  
  
-   Vídeo, [Ajustando seu fluxo de dados de pacotes SSIS na empresa (vídeo do SQL Server)](https://technet.microsoft.com/sqlserver/ff686901.aspx), em technet.microsoft.com  
  
-   Vídeo, [Noções básicas sobre buffers de fluxo de dados SSIS (vídeo do SQL Server)](https://technet.microsoft.com/sqlserver/ff686905.aspx), em technet.microsoft.com  
  
-   Vídeo, [Padrões de design de desempenho do Microsoft SQL Server Integration Services](https://go.microsoft.com/fwlink/?LinkID=233698&clcid=0x409), em channel9.msdn.com.  
  
-   Apresentação, [Como a TI da Microsoft aproveita os aprimoramentos do mecanismo de fluxo de dados SSIS do SQL Server 2008](https://go.microsoft.com/fwlink/?LinkId=217660), em sqlcat.com.  
  
-   Vídeo, [Balanced Data Distributor](https://go.microsoft.com/fwlink/?LinkID=226278&clcid=0x409), em technet.microsoft.com  
  
## <a name="see-also"></a>Consulte também  
 [Solucionando problemas de ferramentas para desenvolvimento de pacotes](../troubleshooting/troubleshooting-tools-for-package-development.md)   
 [Solucionando problemas de ferramentas para execução de pacotes](../troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
  
