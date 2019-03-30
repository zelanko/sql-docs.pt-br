---
title: Configuração do SQL Server (R Services) - serviços de aprendizado de máquina do SQL Server
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 9ad4d1a23a05db35e0c4b55473903dbf7e4265da
ms.sourcegitcommit: c60784d1099875a865fd37af2fb9b0414a8c9550
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58645538"
---
# <a name="sql-server-configuration-for-use-with-r"></a>Configuração do SQL Server para uso com o R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo é o segundo de uma série que descreve a otimização de desempenho para serviços de R com base em dois estudos de caso.  Este artigo fornece orientações sobre a configuração de hardware e de rede do computador que é usado para executar o SQL Server R Services. Ele também contém informações sobre maneiras de configurar a instância do SQL Server, banco de dados ou tabelas usadas em uma solução. Porque o uso de no SQL Server Desfoca a linha entre as otimizações de hardware e o banco de dados, uma terceira seção discute a governança de recursos e a relação de CPU em detalhes.

> [!TIP]
> Se você for novo no SQL Server, é altamente recomendável que você também Revise o guia de ajuste de desempenho do SQL Server: [Monitorar e ajustar o desempenho](https://docs.microsoft.com/sql/relational-databases/performance/monitor-and-tune-for-performance).

## <a name="hardware-optimization"></a>Otimização de hardware

Otimização do computador servidor é importante para garantir que você tenha os recursos para executar scripts externos. Quando os recursos forem limitados, você poderá ver os sintomas como estes:

- A execução do trabalho é adiada ou cancelada para priorizar as outras operações de banco de dados
- Script de R causando erro "cota excedida" para encerrar sem preenchimento
- Dados carregados na memória de R truncada para resultados incompletos

### <a name="memory"></a>Memória

A quantidade de memória disponível no computador pode ter um grande impacto sobre o desempenho de algoritmos analíticos avançados. Memória insuficiente pode afetar o grau de paralelismo ao usar o contexto de computação do SQL. Isso também pode afetar o tamanho da parte (linhas por operação de leitura) que pode ser processada e o número de sessões simultâneas para o qual é possível dar suporte.

Um mínimo de 32 GB é altamente recomendável. Se você tiver mais de 32GB disponível, você pode configurar a fonte de dados SQL para usar mais linhas em cada operação de leitura para melhorar o desempenho.

Você também pode gerenciar a memória usada pela instância. Por padrão, o SQL Server terá prioridade sobre os processos de script externo quando a memória é alocada. Em uma instalação padrão do R Services, apenas 20% da memória disponível é alocado para o R.

Normalmente isso não é suficiente para tarefas de ciência de dados, mas nenhum deles você deseja enfraquecer o SQL server de memória. Você deve testar e ajustar a alocação de memória entre o mecanismo de banco de dados, serviços relacionados e scripts externos, Entendendo que a configuração ideal varia de acordo com o caso.

Para o modelo de correspondência de retomada, o uso de script externo foi pesado e não havia nenhum outro banco de dados serviços de mecanismo de execução; Portanto, os recursos alocados para scripts externos foram aumentados para 70%, que era a melhor configuração para o desempenho de script.

### <a name="power-options"></a>Opções de energia

No sistema operacional Windows, o **de alto desempenho** opção de energia deve ser usada. Usando uma configuração de energia diferente resulta em desempenho reduzido ou inconsistente ao usar o SQL Server.

### <a name="disk-io"></a>E/S de disco

Treinamento e previsão trabalhos usando o R Services são inerentemente de e/s associadas e dependem da velocidade dos discos armazenados no banco de dados. Unidades mais rápidas, como unidades de estado sólido (SSD) podem ajudar.

A E/S de disco também é afetada pelo acesso de outros aplicativos ao disco: por exemplo, operações de leitura por outros clientes em um banco de dados. O desempenho de E/S de disco também pode ser afetado pelas configurações no sistema de arquivos em uso, tais como o tamanho do bloco utilizado pelo sistema de arquivos.

Se houver várias unidades disponíveis, os bancos de dados em uma unidade diferente para que as solicitações para o mecanismo de banco de dados do SQL Server não estão atingindo o mesmo disco do armazenamento de solicitações para dados armazenados no banco de dados.

A E/S de disco também pode afetar substancialmente o desempenho durante a execução de funções analíticas RevoScaleR que usam várias iterações durante o treinamento. Por exemplo, `rxLogit`, `rxDTree`, `rxDForest`, e `rxBTrees` todos usam várias iterações. Quando a fonte de dados for SQL Server, esses algoritmos usam arquivos temporários que são otimizados para capturar os dados. Esses arquivos são limpos automaticamente após a conclusão da sessão. Tendo um disco de alto desempenho para operações de leitura/gravação pode melhorar significativamente o tempo total decorrido para esses algoritmos.

> [!NOTE]
> As versões anteriores do R Services necessário suporte de nome de arquivo 8.3 em sistemas de operacionais do Windows. Essa restrição foi eliminada após o Service Pack 1. No entanto, você pode usar fsutil.exe para determinar se uma unidade dá suporte a nomes de 8.3 arquivo ou para habilitar o suporte se não existir.

### <a name="paging-file"></a>Arquivo de paginação

O sistema operacional Windows usa um arquivo de paginação para gerenciar os despejos de memória e para armazenar páginas de memória virtual. Se você observar excesso de paginação, considere aumentar a memória física do computador. Ter mais memória física reduz a necessidade de paginação, embora não elimine a paginação por completo.

A velocidade do disco no qual o arquivo de paginação está armazenado também pode afetar o desempenho. Armazenar o arquivo de paginação em um SSD ou usar vários arquivos de paginação em vários SSDs pode melhorar o desempenho.

Para obter informações sobre o arquivo de paginação de dimensionamento, consulte [como determinar o tamanho do arquivo de paginação apropriado para versões de 64 bits do Windows](https://support.microsoft.com/kb/2860880).

## <a name="optimizations-at-instance-or-database-level"></a>Otimizações no nível de instância ou banco de dados

Otimização da instância do SQL Server é a chave para uma execução eficiente de scripts externos.

> [!NOTE]
> As definições ideais diferem dependendo do tamanho e tipo de dados, o número de colunas que você está usando para treinar um modelo ou pontuação.
> 
> Você pode examinar os resultados das otimizações específicas no artigo final: [Ajuste de desempenho - resultados de estudo de caso](../../advanced-analytics/r/performance-case-study-r-services.md)
> 
> Para scripts de exemplo, consulte separada [repositório GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning).

### <a name="table-compression"></a>Compactação de tabela

Desempenho de e/s geralmente pode ser melhorado usando compactação ou um armazenamento de dados Colunar. Em geral, dados geralmente são repetidos em várias colunas dentro de uma tabela, portanto, usar um columnstore aproveita a existência dessas repetições ao compactar os dados.

Columnstore não pode ser tão eficiente se houver várias inserções na tabela, mas é uma boa opção se os dados são estáticos ou somente mudam com pouca frequência. Se um repositório em colunas não for apropriado, a habilitação da compactação em uma tabela principal de linha poderá ser usada para melhorar a E/S.

Para obter mais informações, consulte os seguintes documentos:

+ [Compactação de dados](../../relational-databases/data-compression/data-compression.md)

+ [Habilitar a compactação em uma tabela ou índice](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Guia de índices columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md)

### <a name="memory-optimized-tables"></a>Tabelas com otimização de memória

Hoje em dia, a memória não é um problema para computadores modernos. Como as especificações de hardware continuam a melhorar, é relativamente fácil chegar a bons valores de RAM. No entanto, ao mesmo tempo, dados seja produzidos mais rapidamente do que nunca, e os dados devem ser processados com baixa latência.

Tabelas com otimização de memória representam uma única solução, em que eles usam a memória grande disponível em computadores avançados para resolver o problema de big data. Tabelas com otimização de memória principalmente residem na memória, para que os dados é lida e gravados na memória. Para durabilidade, uma segunda cópia da tabela é mantida no disco e dados são lidos apenas no disco durante a recuperação de banco de dados.

Se você precisar ler e gravar em tabelas com frequência, as tabelas com otimização de memória podem ajudar com baixa latência e alta escalabilidade.  No cenário de correspondência de retomada, uso de tabelas com otimização de memória nos permitiu ler todos os recursos de retomada do banco de dados e armazená-los na memória principal, para corresponder ao novo emprego. Isso significativamente reduzido e/s de disco.

Foram obtidos ganhos de desempenho adicionais usando a tabela com otimização de memória no processo de write-back de previsões para o banco de dados de vários lotes simultâneos. O uso de tabelas com otimização de memória no SQL Server habilitado baixa latência na tabela leituras e gravações.

Também foi a experiência perfeita durante o desenvolvimento. As tabelas duráveis com otimização de memória foram criadas ao mesmo tempo que o banco de dados foi criado. Portanto, o desenvolvimento usado o mesmo fluxo de trabalho, independentemente de onde os dados foram armazenados.

### <a name="processor"></a>Processador

SQL Server pode executar tarefas em paralelo usando núcleos disponíveis na máquina. quanto mais núcleos disponíveis, melhor o desempenho. Embora não pode ajudar a aumentar o número de núcleos para operações de e/s associada, CPU associada benefício de algoritmos de CPUs mais rápidas com vários núcleos.

Porque o servidor é normalmente usado por vários usuários simultaneamente, o administrador de banco de dados deve determinar o número ideal de núcleos que são necessários para dar suporte a cálculos de carga de trabalho de pico.

### <a name="resource-governance"></a>Governança de recursos

Em edições que dão suporte ao Resource Governor, você pode usar pools de recursos para especificar que determinadas cargas de trabalho são alocadas a um número de CPUs. Você também pode gerenciar a quantidade de memória alocada para cargas de trabalho específicas.

Governança de recursos no SQL Server permite que você centralize o monitoramento e controle dos vários recursos usados pelo SQL Server e por R. Por exemplo, você pode alocar metade a memória disponível para o mecanismo de banco de dados, para garantir que núcleo de serviços podem ser executados sempre apesar das cargas de trabalho mais pesadas temporárias.

O valor padrão para o consumo de memória por scripts externos é limitado a 20% do total de memória disponível para o próprio SQL Server. Esse limite é aplicado por padrão para garantir que todas as tarefas que dependem do servidor de banco de dados não são gravemente afetadas pelos trabalhos de longa execução R. Entretanto, esses limites podem ser alterados pelo administrador de banco de dados. Em muitos casos, o limite de 20% não é adequado para dar suporte a cargas de trabalho de aprendizado de máquina grave.

As opções de configuração com suporte são **MAX_CPU_PERCENT**, **MAX_MEMORY_PERCENT**, e **MAX_PROCESSES**. Para exibir as configurações atuais, use esta instrução: `SELECT * FROM sys.resource_governor_external_resource_pools`

-  Se o servidor é usado principalmente para R Services, ele pode ser útil aumentar MAX_CPU_PERCENT para 40% ou 60%.

-  Se o número de sessões de R deve usar o mesmo servidor ao mesmo tempo, todas as três configurações devem ser aumentadas.

Para alterar os valores de recursos alocados, use instruções T-SQL.

+ Essa instrução define o uso de memória para 40%: `ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)`

+ Essa instrução define todos os três valores configuráveis: `ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`

+ Se você altera uma memória, CPU ou configuração de processo máximo e, em seguida, deseja aplicar as configurações imediatamente, execute esta instrução: `ALTER RESOURCE GOVERNOR RECONFIGURE`

## <a name="soft-numa-hardware-numa-and-cpu-affinity"></a>Afinidade de de software, de hardware e da CPU

Ao usar o SQL Server como o contexto de computação, você pode, às vezes, obter o melhor desempenho ajustando configurações relacionadas à afinidade de processador e NUMA. 

Sistemas com _de hardware_ tiver mais de um barramento de sistema, cada um atendendo a um pequeno conjunto de processadores. Cada CPU pode acessar a memória associada a outros grupos de uma maneira coerente. Cada grupo é chamado de nó NUMA. Se você tiver NUMA de hardware, poderá configurá-lo para usar memória intercalada em vez de NUMA. Nesse caso, Windows e, portanto, o SQL Server não o reconhecerão como NUMA. 

Você pode executar a consulta a seguir para localizar o número de nós de memória disponíveis para o SQL Server:

```sql
SELECT DISTINCT memory_node_id
FROM sys.dm_os_memory_clerks
```

Se a consulta retorna um nó de memória único (nó 0), você não tem de hardware ou o hardware está configurado como intercalado (não NUMA). SQL Server também ignora o de hardware quando não houver quatro ou menos CPUs, ou se pelo menos um nó tiver apenas uma CPU.

Se o computador tiver vários processadores, mas não tem de hardware, você também pode usar [Soft-NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server) subdividir as CPUs em grupos menores.  No SQL Server 2016 e no SQL Server 2017, o recurso de Soft-NUMA é habilitado automaticamente ao iniciar o serviço do SQL Server.

Quando Soft-NUMA é habilitada, o SQL Server gerencia automaticamente os nós para você; No entanto, para otimizar para cargas de trabalho específicas, você pode desabilitar _afinidade flexível_ e configurar manualmente a afinidade de CPU para os nós NUMA reversível. Isso pode lhe dar mais controle sobre quais cargas de trabalho são atribuídas a quais nós, especialmente se você estiver usando uma edição do SQL Server que dá suporte à governança de recursos. Ao especificar a afinidade de CPU e alinhando os pools de recursos com grupos de CPUs, você pode reduzir a latência e certifique-se de que os processos relacionados são realizados dentro do mesmo nó NUMA.

O processo geral para a configuração de soft-NUMA e afinidade de CPU para dar suporte a cargas de trabalho de R é da seguinte maneira:

1. Habilitar o soft-NUMA, se disponível
2. Definir a afinidade de processador
3. Criar pools de recursos para processos externos, usando [Resource Governor](../r/resource-governance-for-r-services.md)
4. Atribuir a [grupos de carga de trabalho](../../relational-databases/resource-governor/resource-governor-workload-group.md) para grupos de afinidade específicos

Para obter detalhes, incluindo o código de exemplo, consulte este tutorial: [Dicas de otimização de SQL e truques (Ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**Outros recursos:**

+ [Soft-no SQL Server](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)
    
    Como mapear nós de software para CPUs

## <a name="task-specific-optimizations"></a>Otimizações de tarefas específicas

Esta seção resume os métodos adotados nesses estudos de caso e em outros testes, para otimizar cargas de trabalho de aprendizado de máquina específica. Cargas de trabalho comuns incluem vários cenários de pontuação, extração de recursos e engenharia de recursos e treinamento do modelo: uma única linha, em pequenos lotes e lote grande.

### <a name="feature-engineering"></a>Engenharia de recursos

Um ponto problemático com R é normalmente são processado em uma única CPU. Este é um gargalo de desempenho importantes para muitas tarefas, especialmente a engenharia de recursos. A solução de correspondência de retomada, a tarefa de engenharia de recurso sozinha criou 2.500 recursos de produto cruzado que tiveram de ser combinados com os recursos de 100 originais. Essa tarefa levaria uma quantidade significativa de tempo se tudo foi feito em uma única CPU.

Há várias maneiras de melhorar o desempenho de engenharia de recursos. Você pode otimizar o código R e manter a extração de recursos dentro do processo de modelagem ou mover o processo de engenharia de recurso para o SQL.

- Usando o R. Definir uma função e, em seguida, passá-lo como o argumento [rxTransform](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxtransform) durante o treinamento. Se o modelo dá suporte ao processamento paralelo, a tarefa de engenharia de recurso pode ser processada com várias CPUs. Usando essa abordagem, a equipe de ciência de dados observado uma melhoria de desempenho de 16% em termos de tempo de pontuação. No entanto, essa abordagem requer um modelo que dá suporte à paralelização e uma consulta que pode ser executada usando um plano paralelo.

- Contexto de computação usam R com um SQL. Em um ambiente com vários processadores com isolado recursos disponíveis para a execução de lotes separados, você pode obter maior eficiência, isolando as consultas SQL usadas para cada lote, para extrair dados de tabelas e restringir os dados no mesmo grupo de carga de trabalho. Métodos usados para isolar os lotes incluem particionamento e usam o PowerShell para executar consultas separadas em paralelo.

- Execução paralela ad hoc: Em um contexto de computação do SQL Server, você pode contar com o mecanismo de banco de dados SQL para impor a execução paralela se possível, e se essa opção for encontrada para ser mais eficiente.

- Use o T-SQL em um processo separado de personalização. Precomputing os dados do recurso usando o SQL geralmente é mais rápido.

### <a name="prediction-scoring-in-parallel"></a>Previsão (pontuação) em paralelo

Um dos benefícios do SQL Server é sua capacidade para lidar com um grande volume de linhas em paralelo. Não é essa vantagem marcada como pontuação. Geralmente o modelo não precisam de acesso a todos os dados para pontuação, portanto, você pode particionar os dados de entrada, com cada grupo de carga de trabalho, uma tarefa de processamento.

Você também pode enviar os dados de entrada como uma única consulta e do SQL Server, em seguida, analisa a consulta. Se um plano de consulta paralela pode ser criado para os dados de entrada, ele automaticamente particiona dados atribuídos a nós e executa necessárias junções e agregações em paralelo também.

Se você estiver interessado nos detalhes de como definir um procedimento armazenado para usar na pontuação, consulte o projeto de exemplo na [GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips/SQLR) e procure o arquivo "step5_score_for_matching.sql". O exemplo de script também rastreia início da consulta e horários de término e grava o tempo para o console do SQL para que você possa avaliar o desempenho.

### <a name="concurrent-scoring-using-resource-groups"></a>Pontuação simultâneas usando grupos de recursos

Para escalar verticalmente o problema de pontuação, uma prática recomendada é a adotar a abordagem de Map-reduce em que milhões de itens são divididos em vários lotes. Em seguida, vários trabalhos de pontuação são executados simultaneamente. Nessa estrutura, os lotes são processados em diferentes conjuntos de CPU, e os resultados são coletados e gravados no banco de dados.

Essa é a abordagem usada no cenário de correspondência de retomar; No entanto, a governança de recursos no SQL Server é essencial para a implementação dessa abordagem. Configurando grupos de carga de trabalho para trabalhos de script externo, você pode rotear os trabalhos de pontuação para grupos de processador diferente do R e atingir a taxa de transferência mais rápida.

Governança de recursos também pode ajudar a alocar dividir os recursos disponíveis no servidor (CPU e memória) para minimizar a competição de carga de trabalho. Você pode configurar funções de classificação para distinguir entre diferentes tipos de trabalhos do R: por exemplo, você pode decidir que pontuação chamado a partir de um aplicativo sempre terá prioridade, enquanto os trabalhos de readaptação têm prioridade baixa. Esse isolamento de recurso pode potencialmente melhorar o tempo de execução e fornecer um desempenho mais previsível.

### <a name="concurrent-scoring-using-powershell"></a>Pontuação simultâneas usando o PowerShell

Se você decidir dividir os dados por conta própria, você pode usar scripts do PowerShell para executar várias tarefas simultâneas de pontuação. Para fazer isso, use o cmdlet Invoke-SqlCmd e iniciar as tarefas de pontuação em paralelo.

No cenário de correspondência de retomada, simultaneidade foi criada da seguinte maneira:

- 20 processadores divididas em quatro grupos de cinco CPUs. Cada grupo de CPUs está localizado no mesmo nó NUMA.

- Número máximo de lotes simultâneos foi definido como oito.

- Cada grupo de cargas de trabalho deve lidar com duas tarefas de pontuação. Assim que uma tarefa terminar a leitura de dados e inicia a pontuação, a outra tarefa pode começar a ler dados do banco de dados.

Para ver os scripts do PowerShell para esse cenário, abra o experiment.ps1 de arquivo na [projeto Github](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips).

### <a name="storing-models-for-prediction"></a>Armazenando modelos para previsão

Quando o treinamento e avaliação termina e você tiver selecionado um modelo de melhor, é recomendável armazenar o modelo no banco de dados para que ele esteja disponível para previsões. Ao carregar o modelo pré-calculado do banco de dados para a previsão é muito eficiente, porque o aprendizado de máquina do SQL Server usa algoritmos especiais de serialização para armazenar e carregar modelos durante a movimentação entre R e o banco de dados.

> [!TIP]
> No SQL Server 2017, você pode usar a função PREDICT para executar a pontuação, mesmo se R não estiver instalado no servidor. Tipos de modelos limitados têm suporte do pacote RevoScaleR.

No entanto, dependendo do algoritmo usado, alguns modelos podem ser muito grandes, especialmente quando treinado em um grande conjunto de dados. Por exemplo, os algoritmos, como **lm** ou **glm** gerar muitos dados resumidos juntamente com as regras. Como há limites no tamanho de um modelo que pode ser armazenado em uma coluna varbinary, é recomendável que você elimine a artefatos desnecessários do modelo antes de armazenar o modelo no banco de dados de produção.

## <a name="articles-in-this-series"></a>Artigos desta série

[Desempenho de ajuste para R – Introdução](../r/sql-server-r-services-performance-tuning.md)

[Ajuste de desempenho para R – configuração do SQL Server](../r/sql-server-configuration-r-services.md)

[Ajuste de desempenho para R – R otimização de código e dados](../r/r-and-data-optimization-r-services.md)

[Ajuste de desempenho - resultados de estudo de caso](../r/performance-case-study-r-services.md)
