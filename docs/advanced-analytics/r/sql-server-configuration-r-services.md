---
title: Configuração do SQL Server (R Services)
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: feb59ac529b0a66603d9e8b901e9755588ac0379
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344853"
---
# <a name="sql-server-configuration-for-use-with-r"></a>Configuração de SQL Server para uso com o R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo é o segundo de uma série que descreve a otimização de desempenho para o R Services com base em dois estudos de caso.  Este artigo fornece diretrizes sobre a configuração de hardware e de rede do computador que é usado para executar o SQL Server R Services. Ele também contém informações sobre maneiras de configurar a SQL Server instância, o banco de dados ou as tabelas usadas em uma solução. Como o uso de NUMA em SQL Server desfoca a linha entre otimizações de hardware e banco de dados, uma terceira seção aborda a affinitization de CPU e a governança de recursos em detalhes.

> [!TIP]
> Se você for novo no SQL Server, é altamente recomendável que você também examine o guia de ajuste de desempenho SQL Server: [Monitore e ajuste o desempenho](https://docs.microsoft.com/sql/relational-databases/performance/monitor-and-tune-for-performance).

## <a name="hardware-optimization"></a>Otimização de hardware

A otimização do computador servidor é importante para garantir que você tenha os recursos para executar scripts externos. Quando os recursos são limitados, você pode ver sintomas como estes:

- A execução do trabalho é adiada ou cancelada para priorizar outras operações de banco de dados
- Erro "Cota excedida" fazendo com que o script R seja encerrado sem conclusão
- Dados carregados na memória R truncados, para resultados incompletos

### <a name="memory"></a>Memória

A quantidade de memória disponível no computador pode ter um grande impacto sobre o desempenho de algoritmos analíticos avançados. A memória insuficiente pode afetar o grau de paralelismo ao usar o contexto de computação do SQL. Isso também pode afetar o tamanho da parte (linhas por operação de leitura) que pode ser processada e o número de sessões simultâneas para o qual é possível dar suporte.

É altamente recomendável um mínimo de 32 GB. Se você tiver mais de 32 GB disponíveis, poderá configurar a fonte de dados SQL para usar mais linhas em cada operação de leitura para melhorar o desempenho.

Você também pode gerenciar a memória usada pela instância. Por padrão, SQL Server é priorizada sobre processos de script externo quando a memória é alocada. Em uma instalação padrão do R Services, somente 20% da memória disponível são alocados para R.

Normalmente, isso não é suficiente para tarefas de ciência de dados, mas nem você deseja privar o SQL Server da memória. Você deve experimentar e ajustar a alocação de memória entre o mecanismo de banco de dados, os serviços relacionados e os scripts externos, com a compreensão de que a configuração ideal varia de acordo com maiúsculas e minúsculas.

Para o modelo de correspondência de retomada, o uso de script externo era pesado e não havia outros serviços de mecanismo de banco de dados em execução; Portanto, os recursos alocados para scripts externos foram aumentados para 70%, que era a melhor configuração para o desempenho do script.

### <a name="power-options"></a>Opções de energia

No sistema operacional Windows, a opção de energia de **alto desempenho** deve ser usada. Usar uma configuração de energia diferente resulta em desempenho reduzido ou inconsistente ao usar SQL Server.

### <a name="disk-io"></a>E/S de disco

Os trabalhos de treinamento e previsão usando o R Services são inerentemente ligados à e/s e dependem da velocidade dos discos em que o banco de dados está armazenado. Unidades mais rápidas, como unidades de estado sólido (SSD) podem ajudar.

A E/S de disco também é afetada pelo acesso de outros aplicativos ao disco: por exemplo, operações de leitura por outros clientes em um banco de dados. O desempenho de E/S de disco também pode ser afetado pelas configurações no sistema de arquivos em uso, tais como o tamanho do bloco utilizado pelo sistema de arquivos.

Se houver várias unidades disponíveis, armazene os bancos de dados em uma unidade diferente de SQL Server para que as solicitações do mecanismo de banco de dados não estejam atingindo o mesmo disco que as solicitações de dados armazenados no banco.

A E/S de disco também pode afetar substancialmente o desempenho durante a execução de funções analíticas RevoScaleR que usam várias iterações durante o treinamento. Por exemplo, `rxLogit` `rxDTree` `rxBTrees` ,, e todos usam várias iterações. `rxDForest` Quando a fonte de dados é SQL Server, esses algoritmos usam arquivos temporários que são otimizados para capturar os dados. Esses arquivos são limpos automaticamente após a conclusão da sessão. Ter um disco de alto desempenho para operações de leitura/gravação pode melhorar significativamente o tempo total decorrido para esses algoritmos.

> [!NOTE]
> As versões anteriores do R Services exigiram 8,3 de suporte a nome de arquivo em sistemas operacionais Windows. Essa restrição foi levantada após o Service Pack 1. No entanto, você pode usar o fsutil. exe para determinar se uma unidade dá suporte a 8,3 nomes de um ou para habilitar o suporte se não tiver.

### <a name="paging-file"></a>Arquivo de paginação

O sistema operacional Windows usa um arquivo de paginação para gerenciar os despejos de memória e para armazenar páginas de memória virtual. Se você observar excesso de paginação, considere aumentar a memória física do computador. Ter mais memória física reduz a necessidade de paginação, embora não elimine a paginação por completo.

A velocidade do disco no qual o arquivo de paginação está armazenado também pode afetar o desempenho. Armazenar o arquivo de paginação em um SSD ou usar vários arquivos de paginação em vários SSDs pode melhorar o desempenho.

Para obter informações sobre como dimensionar o arquivo de paginação, consulte [como determinar o tamanho do arquivo de paginação apropriado para versões de 64 bits do Windows](https://support.microsoft.com/kb/2860880).

## <a name="optimizations-at-instance-or-database-level"></a>Otimizações na instância ou no nível de banco de dados

A otimização da instância de SQL Server é a chave para a execução eficiente de scripts externos.

> [!NOTE]
> As configurações ideais variam de acordo com o tamanho e o tipo dos dados, o número de colunas que você está usando para pontuação ou treinamento de um modelo.
> 
> Você pode examinar os resultados de otimizações específicas no artigo final: [Ajuste de desempenho-resultados do estudo de caso](../../advanced-analytics/r/performance-case-study-r-services.md)
> 
> Para scripts de exemplo, consulte o [repositório GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)separado.

### <a name="table-compression"></a>Compactação de tabela

O desempenho de e/s geralmente pode ser melhorado usando compactação ou armazenamento de dados de coluna. Geralmente, os dados geralmente são repetidos em várias colunas em uma tabela, portanto, usar um columnstore aproveita essas repetições ao compactar os dados.

Um columnstore pode não ser tão eficiente se houver várias inserções na tabela, mas é uma boa opção se os dados são estáticos ou apenas são alterados com pouca frequência. Se um repositório em colunas não for apropriado, a habilitação da compactação em uma tabela principal de linha poderá ser usada para melhorar a E/S.

Para obter mais informações, consulte os seguintes documentos:

+ [Compactação de dados](../../relational-databases/data-compression/data-compression.md)

+ [Habilitar a compactação em uma tabela ou índice](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Guia de índices columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md)

### <a name="memory-optimized-tables"></a>Tabelas com otimização de memória

Hoje em dia, a memória não é mais um problema para os computadores modernos. À medida que as especificações de hardware continuam a melhorar, é relativamente fácil obter a RAM em valores bons. No entanto, ao mesmo tempo, os dados estão sendo produzidos mais rapidamente do que nunca, e os dados devem ser processados com baixa latência.

As tabelas com otimização de memória representam uma solução, pois elas aproveitam a memória grande disponível em computadores avançados para resolver o problema de Big Data. As tabelas com otimização de memória residem principalmente na memória, para que os dados sejam lidos e gravados na memória. Para durabilidade, uma segunda cópia da tabela é mantida no disco e os dados são lidos somente do disco durante a recuperação do banco de dado.

Se você precisar ler e gravar em tabelas com frequência, as tabelas com otimização de memória podem ajudar com alta escalabilidade e baixa latência.  No cenário retomar correspondência, o uso de tabelas com otimização de memória nos permitiu ler todos os recursos de retomada do banco de dados e armazená-los na memória principal, para corresponder a novas aberturas de trabalho. Isso reduz significativamente a e/s de disco.

Foram obtidos ganhos de desempenho adicionais usando a tabela com otimização de memória no processo de gravação de previsões de volta ao banco de dados de vários lotes simultâneos. O uso de tabelas com otimização de memória no SQL Server latência baixa habilitada em leituras e gravações de tabela.

A experiência também era direta durante o desenvolvimento. As tabelas duráveis com otimização de memória foram criadas ao mesmo tempo em que o banco de dados foi criado. Portanto, o desenvolvimento usou o mesmo fluxo de trabalho, independentemente de onde os dados foram armazenados.

### <a name="processor"></a>Processador

SQL Server pode executar tarefas em paralelo usando os núcleos disponíveis no computador; Quanto mais núcleos estiverem disponíveis, melhor será o desempenho. Embora o aumento do número de núcleos possa não ajudar as operações associadas à e/s, os algoritmos associados à CPU se beneficiam de CPUs mais rápidas com muitos núcleos.

Como o servidor é normalmente usado por vários usuários simultaneamente, o administrador de banco de dados deve determinar o número ideal de núcleos necessários para dar suporte a cálculos de carga de trabalho de pico.

### <a name="resource-governance"></a>Governança de recursos

Em edições que dão suporte a Resource Governor, você pode usar pools de recursos para especificar que determinadas cargas de trabalho sejam alocadas a um número de CPUs. Você também pode gerenciar a quantidade de memória alocada para cargas de trabalho específicas.

A governança de recursos no SQL Server permite centralizar o monitoramento e o controle dos vários recursos usados pelo SQL Server e pelo R. Por exemplo, você pode alocar metade da memória disponível para o mecanismo de banco de dados, para garantir que os serviços principais sempre possam ser executados apesar de cargas de trabalho pesadas transitórias.

O valor padrão para o consumo de memória por scripts externos é limitado a 20% da memória total disponível para SQL Server em si. Esse limite é aplicado por padrão para garantir que todas as tarefas que dependem do servidor de banco de dados não sejam severamente afetadas por trabalhos de R de longa execução. Entretanto, esses limites podem ser alterados pelo administrador de banco de dados. Em muitos casos, o limite de 20% não é adequado para dar suporte a cargas de trabalho de aprendizado de máquina sérias.

As opções de configuração com suporte são **MAX_CPU_PERCENT**, **MAX_MEMORY_PERCENT**e **MAX_PROCESSES**. Para exibir as configurações atuais, use esta instrução:`SELECT * FROM sys.resource_governor_external_resource_pools`

-  Se o servidor for usado principalmente para o R Services, poderá ser útil aumentar o MAX_CPU_PERCENT para 40% ou 60%.

-  Se muitas sessões de R devem usar o mesmo servidor ao mesmo tempo, todas as três configurações devem ser aumentadas.

Para alterar os valores de recursos alocados, use instruções T-SQL.

+ Essa instrução define o uso de memória como 40%:`ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)`

+ Essa instrução define todos os três valores configuráveis:`ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`

+ Se você alterar uma configuração de memória, CPU ou máximo de processo e quiser aplicar as configurações imediatamente, execute esta instrução:`ALTER RESOURCE GOVERNOR RECONFIGURE`

## <a name="soft-numa-hardware-numa-and-cpu-affinity"></a>Afinidade de CPU, NUMA e de hardware

Ao usar SQL Server como o contexto de computação, às vezes você pode obter melhor desempenho ajustando as configurações relacionadas à afinidade NUMA e de processador. 

Sistemas com _hardware numa_ têm mais de um barramento de sistema, cada um servindo um pequeno conjunto de processadores. Cada CPU pode acessar a memória associada a outros grupos de forma coerente. Cada grupo é chamado de nó NUMA. Se você tiver NUMA de hardware, poderá configurá-lo para usar memória intercalada em vez de NUMA. Nesse caso, o Windows e, portanto, SQL Server não irá reconhecê-lo como NUMA. 

Você pode executar a consulta a seguir para localizar o número de nós de memória disponíveis para SQL Server:

```sql
SELECT DISTINCT memory_node_id
FROM sys.dm_os_memory_clerks
```

Se a consulta retornar um único nó de memória (nó 0), você não tem um NUMA de hardware ou o hardware é configurado como intercalado (não NUMA). SQL Server também ignora o NUMA de hardware quando há quatro ou menos CPUs, ou se pelo menos um nó tem apenas uma CPU.

Se o computador tiver vários processadores, mas não tiver hardware-NUMA, você também poderá usar o [Soft-numa](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server) para subdividir as CPUs em grupos menores.  No SQL Server 2016 e SQL Server 2017, o recurso soft-NUMA é habilitado automaticamente ao iniciar o serviço SQL Server.

Quando o soft-NUMA está habilitado, SQL Server gerencia automaticamente os nós para você; no entanto, para otimizar cargas de trabalho específicas, você pode desabilitar a _afinidade flexível_ e configurar manualmente a afinidade de CPU para os nós Soft numa. Isso pode fornecer a você mais controle sobre quais cargas de trabalho são atribuídas a quais nós, especialmente se você estiver usando uma edição do SQL Server que dá suporte à governança de recursos. Ao especificar a afinidade de CPU e alinhar os pools de recursos com grupos de CPUs, você pode reduzir a latência e garantir que os processos relacionados sejam executados dentro do mesmo nó NUMA.

O processo geral para configurar a afinidade de CPU e soft-NUMA para dar suporte a cargas de trabalho de R é o seguinte:

1. Habilite o soft-NUMA, se disponível
2. Definir afinidade de processador
3. Criar pools de recursos para processos externos usando [resource governor](../r/resource-governance-for-r-services.md)
4. Atribuir os [grupos de cargas de trabalho](../../relational-databases/resource-governor/resource-governor-workload-group.md) a grupos de afinidade específicos

Para obter detalhes, incluindo o código de exemplo, consulte este tutorial: [Dicas e truques de otimização do SQL (ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**Outros recursos:**

+ [Soft-NUMA em SQL Server](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)
    
    Como mapear nós soft-NUMA para CPUs

## <a name="task-specific-optimizations"></a>Otimizações específicas à tarefa

Esta seção resume os métodos adotados nesses estudos de caso e em outros testes para otimizar cargas de trabalho de Machine Learning específicas. As cargas de trabalho comuns incluem treinamento de modelo, extração de recursos e engenharia de recursos e vários cenários de Pontuação: linha única, lote pequeno e lote grande.

### <a name="feature-engineering"></a>Engenharia de recursos

Um ponto problemático com o R é que ele geralmente é processado em uma única CPU. Esse é um grande afunilamento de desempenho para muitas tarefas, especialmente a engenharia de recursos. Na solução retomar correspondência, a tarefa de engenharia de recursos criou sozinho 2.500 recursos entre produtos que precisavam ser combinados com os recursos originais do 100. Essa tarefa levaria uma quantidade significativa de tempo se tudo tiver sido feito em uma única CPU.

Há várias maneiras de melhorar o desempenho da engenharia de recursos. Você pode otimizar o código R e manter a extração de recursos dentro do processo de modelagem ou mover o processo de engenharia de recursos para o SQL.

- Usando o R. Você define uma função e a passa como o argumento para [rxTransform](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxtransform) durante o treinamento. Se o modelo oferecer suporte ao processamento paralelo, a tarefa de engenharia de recursos poderá ser processada usando várias CPUs. Usando essa abordagem, a equipe de ciência de dados observou uma melhoria de desempenho de 16% em termos de tempo de pontuação. No entanto, essa abordagem requer um modelo que dá suporte à paralelização e uma consulta que pode ser executada usando um plano paralelo.

- Use o R com um contexto de computação do SQL. Em um ambiente multiprocessador com recursos isolados disponíveis para execução de lotes separados, você pode obter maior eficiência isolando as consultas SQL usadas para cada lote, para extrair dados de tabelas e restringir os dados no mesmo grupo de carga de trabalho. Os métodos usados para isolar os lotes incluem particionamento e uso do PowerShell para executar consultas separadas em paralelo.

- Execução paralela ad hoc: Em um contexto de computação SQL Server, você pode confiar no mecanismo de banco de dados SQL para impor a execução paralela, se possível, e se essa opção for considerada mais eficiente.

- Use o T-SQL em um processo personalização separado. A computação dos dados de recurso usando o SQL é geralmente mais rápida.

### <a name="prediction-scoring-in-parallel"></a>Previsão (Pontuação) em paralelo

Um dos benefícios da SQL Server é sua capacidade de lidar com um grande volume de linhas em paralelo. Em qualquer lugar, essa vantagem é marcada como em Pontuação. Geralmente, o modelo não precisa de acesso a todos os dados para pontuação, para que você possa particionar os dados de entrada, com cada grupo de carga de trabalho processando uma tarefa.

Você também pode enviar os dados de entrada como uma única consulta e SQL Server analisa a consulta. Se um plano de consulta paralelo puder ser criado para os dados de entrada, ele particionará automaticamente os dados atribuídos aos nós e executará junções e agregações necessárias em paralelo também.

Se você estiver interessado nos detalhes de como definir um procedimento armazenado para uso em pontuação, consulte o projeto de exemplo no [GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips/SQLR) e procure o arquivo "step5_score_for_matching. SQL". O script de exemplo também controla os horários de início e término da consulta e grava o tempo no console do SQL para que você possa avaliar o desempenho.

### <a name="concurrent-scoring-using-resource-groups"></a>Pontuação simultânea usando grupos de recursos

Para escalar verticalmente o problema de pontuação, uma boa prática é adotar a abordagem de redução de mapa na qual milhões de itens são divididos em vários lotes. Em seguida, vários trabalhos de pontuação são executados simultaneamente. Nessa estrutura, os lotes são processados em diferentes conjuntos de CPU e os resultados são coletados e gravados novamente no banco de dados.

Essa é a abordagem usada no cenário de correspondência de retomada; no entanto, a governança de recursos no SQL Server é essencial para implementar essa abordagem. Ao configurar grupos de carga de trabalho para trabalhos de script externo, você pode rotear trabalhos de Pontuação de R para diferentes grupos de processador e obter uma taxa de transferência mais rápida.

A governança de recursos também pode ajudar a alocar a divisão dos recursos disponíveis no servidor (CPU e memória) para minimizar a competição de carga de trabalho. Você pode configurar funções de classificação para distinguir entre diferentes tipos de trabalhos de R: por exemplo, você pode decidir que a pontuação chamada de um aplicativo sempre tem prioridade, enquanto os trabalhos de readaptação têm prioridade baixa. Esse isolamento de recursos pode potencialmente melhorar o tempo de execução e fornecer um desempenho mais previsível.

### <a name="concurrent-scoring-using-powershell"></a>Pontuação simultânea usando o PowerShell

Se você decidir particionar os dados por conta própria, poderá usar scripts do PowerShell para executar várias tarefas de Pontuação simultâneas. Para fazer isso, use o cmdlet Invoke-SqlCmd e inicie as tarefas de pontuação em paralelo.

No cenário retomar correspondência, a simultaneidade foi projetada da seguinte maneira:

- 20 processadores divididos em quatro grupos de cinco CPUs cada. Cada grupo de CPUs está localizado no mesmo nó NUMA.

- O número máximo de lotes simultâneos foi definido como oito.

- Cada grupo de carga de trabalho deve lidar com duas tarefas de pontuação. Assim que uma tarefa terminar de ler os dados e começar a pontuação, a outra tarefa poderá começar a ler os dados do Database.

Para ver os scripts do PowerShell para esse cenário, abra o arquivo experimento. ps1 no [projeto do GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips).

### <a name="storing-models-for-prediction"></a>Armazenando modelos para previsão

Quando o treinamento e a avaliação forem concluídos e você tiver selecionado um melhor modelo, recomendamos armazenar o modelo no banco de dados para que ele esteja disponível para previsões. Carregar o modelo previamente computado do banco de dados para a previsão é eficiente, porque SQL Server Machine Learning usa algoritmos de serialização especiais para armazenar e carregar modelos ao se mover entre o R e o banco de dados.

> [!TIP]
> No SQL Server 2017, você pode usar a função PREDICT para executar a pontuação, mesmo se o R não estiver instalado no servidor. Os tipos de modelos limitados têm suporte, do pacote RevoScaleR.

No entanto, dependendo do algoritmo usado, alguns modelos podem ser muito grandes, especialmente quando treinados em um grande conjunto de dados. Por exemplo, os algoritmos como o **LM** ou o **GLM** geram muitos dados de resumo junto com as regras. Como há limites no tamanho de um modelo que pode ser armazenado em uma coluna varbinary, recomendamos que você elimine artefatos desnecessários do modelo antes de armazenar o modelo no banco de dados para produção.

## <a name="articles-in-this-series"></a>Artigos desta série

[Ajuste de desempenho para R-introdução](../r/sql-server-r-services-performance-tuning.md)

[Ajuste de desempenho para configuração de SQL Server R](../r/sql-server-configuration-r-services.md)

[Ajuste de desempenho para otimização de dados e código R-R](../r/r-and-data-optimization-r-services.md)

[Ajuste de desempenho-resultados do estudo de caso](../r/performance-case-study-r-services.md)
