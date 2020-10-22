---
title: Configuração para uso com R
description: Este artigo fornece diretrizes sobre a configuração de hardware e de rede do computador usado para executar o SQL Server R Services.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 03/29/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: feaa53fa47591ecdb3f1f0bc66ab390def8fbbb1
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195770"
---
# <a name="sql-server-configuration-for-use-with-r"></a>Configuração do SQL Server para uso com R
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Este artigo é o segundo de uma série que descreve a otimização de desempenho para R Services com base em dois estudos de caso.  Este artigo fornece diretrizes sobre a configuração de hardware e de rede do computador usado para executar o SQL Server R Services. Ele também contém informações sobre maneiras de configurar as tabelas, o banco de dados ou a instância do SQL Server usada em uma solução. Como o uso de NUMA no SQL Server mistura os conceitos de otimização de hardware e de banco de dados, uma terceira seção aborda o ajuste da CPU e a governança de recursos em detalhes.

> [!TIP]
> Se você não estiver familiarizado com o SQL Server, recomendamos que também leia o guia de ajuste de desempenho do SQL Server: [Monitorar e ajustar para aumentar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md).

## <a name="hardware-optimization"></a>Otimização de hardware

A otimização do computador servidor é importante para garantir que você tenha os recursos para executar scripts externos. Quando os recursos são limitados, você poderá observar sintomas como estes:

- A execução do trabalho é adiada ou cancelada para priorizar outras operações de banco de dados
- Erro de "cota excedida", fazendo com que o script R seja encerrado sem conclusão
- Dados carregados na memória de R truncados, levando a resultados incompletos

### <a name="memory"></a>Memória

A quantidade de memória disponível no computador pode ter um grande impacto sobre o desempenho de algoritmos analíticos avançados. A insuficiência de memória pode afetar o grau de paralelismo ao usar o contexto de computação do SQL. Isso também pode afetar o tamanho da parte (linhas por operação de leitura) que pode ser processada e o número de sessões simultâneas para o qual é possível dar suporte.

Um mínimo de 32 GB é altamente recomendável. Se tiver mais de 32 GB disponíveis, você poderá configurar a fonte de dados SQL para usar mais linhas em cada operação de leitura, a fim de melhorar o desempenho.

Você também pode gerenciar a memória usada pela instância. Por padrão, o SQL Server é priorizado com relação a processos de script externos quando a memória é alocada. Em uma instalação padrão do R Services, somente 20% da memória disponível é alocada para o R.

Normalmente, isso não é suficiente para tarefas de ciência de dados, mas você também não deseja privar o SQL Server de memória. Você deve experimentar e ajustar a alocação de memória entre o mecanismo de banco de dados, os serviços relacionados e os scripts externos, tendo a compreensão de que a configuração ideal varia caso a caso.

Para o modelo de correspondência de currículos, o uso de scripts externos era intensivo e não havia outros serviços de mecanismo de banco de dados em execução; portanto, os recursos alocados para os scripts externos foram aumentados para 70%, que era a melhor configuração para ter o melhor desempenho de scripts.

### <a name="power-options"></a>Opções de energia

No sistema operacional Windows, a opção de energia de **Alto desempenho** deve ser usada. Usar uma configuração de energia diferente resulta em desempenho reduzido ou inconsistente ao usar o SQL Server.

### <a name="disk-io"></a>E/S de disco

Trabalhos de treinamento e previsão usando R Services são inerentemente vinculados a E/S e dependem da velocidade dos discos nos quais o banco de dados é armazenado. Unidades mais rápidas, tais como unidades SSD (unidades de estado sólido) podem ajudar.

A E/S de disco também é afetada pelo acesso de outros aplicativos ao disco: por exemplo, operações de leitura por outros clientes em um banco de dados. O desempenho de E/S de disco também pode ser afetado pelas configurações no sistema de arquivos em uso, tais como o tamanho do bloco utilizado pelo sistema de arquivos.

Se houver várias unidades disponíveis, armazene os bancos de dados em uma unidade diferente do SQL Server, de modo que as solicitações para o mecanismo de banco de dados não atinjam o mesmo disco que as solicitações de dados armazenados no banco de dados.

A E/S de disco também pode afetar substancialmente o desempenho durante a execução de funções analíticas RevoScaleR que usam várias iterações durante o treinamento. Por exemplo, `rxLogit`, `rxDTree`, `rxDForest` e `rxBTrees` usam várias iterações. Quando a fonte de dados é o SQL Server, esses algoritmos usam arquivos temporários que são otimizados para capturar os dados. Esses arquivos são limpos automaticamente após a conclusão da sessão. Ter um disco de alto desempenho para operações de leitura/gravação pode melhorar significativamente o tempo decorrido total para esses algoritmos.

> [!NOTE]
> As versões anteriores do R Services exigiam suporte para nome de arquivo 8.3 em sistemas operacionais Windows. Essa restrição foi removida após o Service Pack 1. No entanto, você pode usar fsutil.exe para determinar se uma unidade dá suporte a nomes de arquivo 8.3 ou para habilitar o suporte, se esse não for o caso.

### <a name="paging-file"></a>Arquivo de paginação

O sistema operacional Windows usa um arquivo de paginação para gerenciar os despejos de memória e para armazenar páginas de memória virtual. Se você observar excesso de paginação, considere aumentar a memória física do computador. Ter mais memória física reduz a necessidade de paginação, embora não elimine a paginação por completo.

A velocidade do disco no qual o arquivo de paginação está armazenado também pode afetar o desempenho. Armazenar o arquivo de paginação em um SSD ou usar vários arquivos de paginação em vários SSDs pode melhorar o desempenho.

Para obter informações sobre o dimensionamento do arquivo de paginação, confira [Como determinar o tamanho do arquivo de paginação apropriado para versões de 64 bits do Windows](https://support.microsoft.com/kb/2860880).

## <a name="optimizations-at-instance-or-database-level"></a>Otimizações no nível da instância ou do banco de dados

A otimização da instância do SQL Server é a chave para a execução eficiente de scripts externos.

> [!NOTE]
> As configurações ideais variam de acordo com o tamanho e o tipo dos dados e com o número de colunas que você está usando para pontuação ou treinamento de um modelo.
> 
> Você pode examinar os resultados de otimizações específicas no artigo final: [Ajuste de desempenho – resultados do estudo de caso](../../machine-learning/r/performance-case-study-r-services.md)
> 
> Para ver exemplos de script, confira o [repositório do GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning) separado.

### <a name="table-compression"></a>Compactação de tabela

O desempenho de E/S geralmente pode ser melhorado usando compactação ou um armazenamento de dados de coluna. Em geral, muitas vezes os dados são repetidos em várias colunas dentro de uma tabela, de modo que usar um columnstore aproveita a existência dessas repetições ao compactar os dados.

Se houver muitas inserções na tabela, um columnstore poderá não ser tão eficiente; no entanto, ele será uma boa escolha se os dados forem estáticos ou alterados com pouca frequência. Se um repositório em colunas não for apropriado, a habilitação da compactação em uma tabela principal de linha poderá ser usada para melhorar a E/S.

Para obter mais informações, consulte um dos seguintes documentos:

+ [Compactação de dados](../../relational-databases/data-compression/data-compression.md)

+ [Habilitar a compactação em uma tabela ou um índice](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Guia de índices columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md)

### <a name="memory-optimized-tables"></a>Tabelas com otimização de memória

Hoje em dia, a memória não é mais um problema para os computadores modernos. À medida que as especificações de hardware continuam sendo aprimoradas, é relativamente fácil obter boas quantidades de RAM. Ao mesmo tempo, no entanto, os dados estão sendo produzidos mais rapidamente do que nunca e precisam ser processados com baixa latência.

As tabelas com otimização de memória são uma solução, pois aproveitam a grande memória disponível em computadores avançados para resolver o problema de Big Data. As tabelas com otimização de memória residem principalmente na memória, para que os dados sejam lidos e gravados nela. Para fins de durabilidade, uma segunda cópia da tabela é mantida no disco e os dados são lidos somente do disco durante a recuperação do banco de dados.

Se você precisa ler e gravar em tabelas com frequência, as tabelas com otimização de memória podem ajudar proporcionando alta escalabilidade e baixa latência.  No cenário de correspondência de currículos, o uso de tabelas com otimização de memória nos permitiu ler todos os recursos dos currículos do banco de dados e armazená-los na memória principal, para corresponder a novas vagas de trabalho. Isso reduziu significativamente a E/S de disco.

Foram obtidos ganhos de desempenho adicionais usando a tabela com otimização de memória no processo gravar as previsões de volta no banco de dados de vários lotes simultâneos. O uso de tabelas com otimização de memória no SQL Server proporcionou baixa latência em leituras e gravações de tabela.

A experiência também foi direta durante o desenvolvimento. Tabelas com otimização de memória duráveis foram criadas ao mesmo tempo em que o banco de dados. Portanto, o desenvolvimento usou o mesmo fluxo de trabalho, independentemente de onde os dados foram armazenados.

### <a name="processor"></a>Processador

O SQL Server pode executar tarefas em paralelo usando núcleos disponíveis no computador; quanto mais núcleos disponíveis, melhor o desempenho. Embora aumentar o número de núcleos possa não ajudar para operações vinculadas de E/S, algoritmos vinculados à CPU se beneficiarão de CPUs mais rápidas com vários núcleos.

Como o servidor normalmente é usado por vários usuários simultaneamente, o administrador do banco de dados deve determinar o número ideal de núcleos que são necessários para dar suporte a cálculos de carga de trabalho de pico.

### <a name="resource-governance"></a>Governança de recursos

Em edições com suporte para o Resource Governor, você pode usar pools de recursos para especificar que determinadas cargas de trabalho sejam alocadas a um número de CPUs. Você também pode gerenciar a quantidade de memória alocada para cargas de trabalho específicas.

A governança de recursos no SQL Server permite centralizar o monitoramento e o controle dos vários recursos usados pelo SQL Server e pelo R. Por exemplo, você pode alocar metade da memória disponível para o mecanismo de banco de dados, para garantir que os serviços principais sempre possam ser executados apesar de cargas de trabalho pesadas transitórias.

O valor padrão do consumo de memória por scripts externos é limitado a 20% da memória total disponível para o SQL Server em si. Esse limite é aplicado por padrão para garantir que todas as tarefas que dependem do servidor de banco de dados não sejam gravemente afetadas por trabalhos de R de execução prolongada. Entretanto, esses limites podem ser alterados pelo administrador de banco de dados. Em muitos casos, o limite de 20% não é adequado para dar suporte a cargas de trabalho de aprendizado de máquina sérias.

As opções de configuração com suporte são **MAX_CPU_PERCENT**, **MAX_MEMORY_PERCENT** e **MAX_PROCESSES**. Para exibir as configurações atuais, use esta instrução: `SELECT * FROM sys.resource_governor_external_resource_pools`

-  Se o servidor for usado principalmente para R Services, poderá ser útil aumentar MAX_CPU_PERCENT para 40% ou 60%.

-  Se muitas sessões de R precisarem usar o mesmo servidor ao mesmo tempo, as três configurações deverão ser aumentadas.

Para alterar os valores dos recursos alocados, use instruções T-SQL.

+ Esta instrução configura o uso de memória como 40%: `ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)`

+ Esta instrução define os três valores configuráveis: `ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`

+ Se você alterar uma configuração de memória, CPU ou processamento máximo e quiser aplicar as configurações imediatamente, execute esta instrução: `ALTER RESOURCE GOVERNOR RECONFIGURE`

## <a name="soft-numa-hardware-numa-and-cpu-affinity"></a>Soft-NUMA, NUMA de hardware e afinidade de CPU

Ao usar o SQL Server como o contexto de computação, às vezes você pode obter o melhor desempenho ajustando as configurações relacionadas ao NUMA e à afinidade de processador. 

Sistemas com _NUMA de hardware_ têm mais de um barramento de sistema, cada um atendendo a um conjunto pequenos de processadores. Cada CPU pode acessar a memória associada aos outros grupos de um modo coerente. Cada grupo é chamado de nó NUMA. Se você tiver NUMA de hardware, poderá configurá-lo para usar memória intercalada em vez de NUMA. Neste caso, o Windows e, consequentemente, o SQL Server não o reconhecerão como NUMA. 

Execute a consulta a seguir para localizar o número de nós de memória disponíveis para o SQL Server:

```sql
SELECT DISTINCT memory_node_id
FROM sys.dm_os_memory_clerks
```

Se a consulta retornar um nó de memória único (nó 0), significa que você não tem NUMA de hardware ou o hardware está configurado como intercalado (não NUMA). O SQL Server também ignora o NUMA de hardware quando há quatro ou menos CPUs ou se pelo menos um nó tem apenas uma CPU.

Se o computador tiver vários processadores, mas não tiver NUMA de hardware, você também poderá usar [Soft-NUMA](../../database-engine/configure-windows/soft-numa-sql-server.md) para subdividir as CPUs em grupos menores.  No SQL Server 2016 e no SQL Server 2017, o recurso Soft-NUMA é habilitado automaticamente ao iniciar o serviço SQL Server.

Quando o Soft-NUMA está habilitado, o SQL Server gerencia automaticamente os nós para você. No entanto, para otimizar cargas de trabalho específicas, você pode desabilitar a _afinidade flexível_ e configurar manualmente a afinidade de CPU para os nós de Soft-NUMA. Isso poderá proporcionar mais controle sobre quais cargas de trabalho são atribuídas a quais nós, especialmente se você estiver usando uma edição do SQL Server com suporte à governança de recursos. Ao especificar a afinidade de CPU e alinhar os pools de recursos com grupos de CPUs, você pode reduzir a latência e garantir que os processos relacionados sejam executados dentro do mesmo nó NUMA.

O processo geral para configurar a afinidade de CPU e o soft-NUMA para dar suporte a cargas de trabalho de R é o seguinte:

1. Habilitar o soft-NUMA, se disponível
2. Definir a afinidade do processador
3. Criar pools de recursos para processos externos usando o [Resource Governor](../administration/resource-governor.md)
4. Atribuir os [grupos de carga de trabalho](../../relational-databases/resource-governor/resource-governor-workload-group.md) a grupos de afinidade específicos

Para obter detalhes, incluindo o código de exemplo, confira este tutorial: [Dicas e truques de otimização de SQL (Ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**Outros recursos:**

+ [Soft-NUMA no SQL Server](../../database-engine/configure-windows/soft-numa-sql-server.md)
    
    Como mapear nós soft-NUMA para CPUs

## <a name="task-specific-optimizations"></a>Otimizações específicas à tarefa

Esta seção resume os métodos adotados nesses estudos de caso e em outros testes para otimizar cargas de trabalho de aprendizado de máquina específicas. As cargas de trabalho comuns incluem treinamento de modelo, extração de recursos e engenharia de recursos, bem como vários cenários de pontuação: linha única, lote pequeno e lote grande.

### <a name="feature-engineering"></a>Engenharia de recursos

Um ponto problemático com o R é que ele geralmente é processado em uma única CPU. Esse é um grande gargalo de desempenho para muitas tarefas, especialmente a engenharia de recursos. Na solução de correspondência de currículos, só a tarefa de engenharia de recursos criou 2.500 recursos entre produtos que precisavam ser combinados com os 100 recursos originais. Essa tarefa levaria um tempo significativo se tudo tivesse sido feito em uma única CPU.

Há várias maneiras de melhorar o desempenho da engenharia de recursos. Você pode otimizar o código de R e manter a extração de recursos dentro do processo de modelagem ou pode mover o processo de engenharia de recursos para o SQL.

- Usando R, você define uma função e a passa como o argumento para [rxTransform](/r-server/r-reference/revoscaler/rxtransform) durante o treinamento. Se o modelo der suporte ao processamento paralelo, a tarefa de engenharia de recursos poderá ser processada usando várias CPUs. Usando essa abordagem, a equipe de ciência de dados observou uma melhoria de desempenho de 16% em termos de tempo de pontuação. No entanto, essa abordagem requer um modelo com suporte à paralelização e uma consulta que possa ser executada usando um plano paralelo.

- Usar R com um contexto de computação SQL. Em um ambiente multiprocessador com recursos isolados disponíveis para execução de lotes separados, você pode ter maior eficiência isolando as consultas SQL usadas para cada lote, para extrair dados de tabelas e restringir os dados ao mesmo grupo de carga de trabalho. Os métodos usados para isolar os lotes incluem particionamento e uso do PowerShell para executar consultas separadas em paralelo.

- Execução paralela ad hoc: Em um contexto de computação do SQL Server, você poderá confiar no mecanismo de Banco de Dados SQL para impor a execução paralela (se possível) e se essa opção for considerada mais eficiente.

- Use o T-SQL em um processo de criação de recursos separado. Normalmente, a computação prévia dos dados de recurso usando SQL é mais rápida.

### <a name="prediction-scoring-in-parallel"></a>Previsão (pontuação) em paralelo

Um dos benefícios do SQL Server é sua capacidade de lidar com um grande volume de linhas em paralelo. Essa vantagem fica mais evidente na pontuação. Geralmente, o modelo não precisa de acesso a todos os dados para pontuação, de modo que você pode particionar os dados de entrada, com cada grupo de carga de trabalho processando uma tarefa.

Você também pode enviar os dados de entrada como uma única consulta e o SQL Server, por sua vez, analisa a consulta. Se um plano de consulta paralelo puder ser criado para os dados de entrada, ele particionará automaticamente os dados atribuídos aos nós e executará as junções e agregações necessárias em paralelo também.

Se você estiver interessado nos detalhes de como definir um procedimento armazenado para uso na pontuação, confira o projeto de exemplo no [GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips-Resume-Matching/SQLR) e procure o arquivo "step5_score_for_matching.sql". O script de exemplo também controla os horários de início e término da consulta e grava o tempo no console do SQL para que você possa avaliar o desempenho.

### <a name="concurrent-scoring-using-resource-groups"></a>Pontuação simultânea usando grupos de recursos

Para escalar verticalmente o problema de pontuação, é uma boa prática adotar a abordagem de map-reduce, na qual milhões de itens são divididos em vários lotes. Em seguida, vários trabalhos de pontuação são executados simultaneamente. Nessa estrutura, os lotes são processados em diferentes conjuntos de CPU e os resultados são coletados e gravados novamente no banco de dados.

Essa é a abordagem usada no cenário de correspondência de currículos. No entanto, a governança de recursos no SQL Server é essencial para implementar essa abordagem. Ao configurar grupos de carga de trabalho para trabalhos de script externo, você pode rotear trabalhos de pontuação de R para diferentes grupos de processador e obter uma taxa de transferência mais rápida.

A governança de recursos também pode ajudar a alocar a divisão dos recursos disponíveis no servidor (CPU e memória) para minimizar a competição entre cargas de trabalho. Você pode configurar funções de classificação para diferenciar entre os tipos de trabalhos de R: por exemplo, você pode decidir que a pontuação chamada de um aplicativo sempre tem prioridade, enquanto trabalhos para treinar novamente são de baixa prioridade. Esse isolamento de recursos tem o potencial de melhorar o tempo de execução e fornecer um desempenho mais previsível.

### <a name="concurrent-scoring-using-powershell"></a>Pontuação simultânea usando o PowerShell

Se você decidir particionar os dados por conta própria, poderá usar scripts do PowerShell para executar várias tarefas de pontuação simultâneas. Para fazer isso, use o cmdlet Invoke-SqlCmd e inicie as tarefas de pontuação em paralelo.

No cenário de correspondência de currículos, a simultaneidade foi projetada da seguinte maneira:

- 20 processadores divididos em quatro grupos de cinco CPUs cada. Cada grupo de CPUs fica no mesmo nó NUMA.

- O número máximo de lotes simultâneos foi definido como oito.

- Cada grupo de carga de trabalho precisa lidar com duas tarefas de pontuação. Assim que uma tarefa terminar de ler os dados e começar a pontuação, a outra tarefa poderá começar a ler os dados do banco de dados.

Para ver os scripts do PowerShell para esse cenário, abra o arquivo experiment.ps1 no projeto do [GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips-Resume-Matching).

### <a name="storing-models-for-prediction"></a>Armazenando modelos para previsão

Após o treinamento e a avaliação serem concluídos e você selecionar o melhor modelo, recomendamos armazenar o modelo no banco de dados para que ele fique disponível para previsões. Carregar o modelo pré-calculado do banco de dados para a previsão é eficiente, porque o aprendizado de máquina do SQL Server usa algoritmos de serialização especiais para armazenar e carregar modelos ao alternar entre o R e o banco de dados.

> [!TIP]
> No SQL Server 2017, você pode usar a função PREDICT para executar a pontuação, mesmo se o R não estiver instalado no servidor. Tipos de modelos limitados têm suporte do pacote RevoScaleR.

No entanto, dependendo do algoritmo usado, alguns modelos podem ser muito grandes, especialmente quando treinados em um grande conjunto de dados. Por exemplo, algoritmos como **lm** ou **glm** geram muitos dados de resumo junto com as regras. Como há limites quanto ao tamanho de um modelo que pode ser armazenado em uma coluna varbinary, recomendamos que você elimine artefatos desnecessários do modelo antes de armazená-lo no banco de dados para produção.

## <a name="articles-in-this-series"></a>Artigos nesta série

[Ajuste de desempenho para R – Introdução](../r/sql-server-r-services-performance-tuning.md)

[Ajuste de desempenho para R – configuração do SQL Server](../r/sql-server-configuration-r-services.md)

[Ajuste de desempenho para R – otimização de dados e código do R](../r/r-and-data-optimization-r-services.md)

[Ajuste de desempenho – resultados do estudo de caso](../r/performance-case-study-r-services.md)