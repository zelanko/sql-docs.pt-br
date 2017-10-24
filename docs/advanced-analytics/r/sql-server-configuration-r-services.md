---
title: "Configuração do SQL Server (R Services) | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4b08969f-b90b-46b3-98e7-0bf7734833fc
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: dbd29457adf7a3dd05211c2dc0688d45a54e405e
ms.contentlocale: pt-br
ms.lasthandoff: 09/27/2017

---
# <a name="sql-server-configuration-for-use-with-r"></a>Configuração do SQL Server para uso com R

Este artigo é o segundo de uma série que descreve a otimização de desempenho para serviços de R com base em dois estudos de caso.  Este artigo fornece orientação sobre a configuração de hardware e de rede do computador que é usada para executar o SQL Server R Services. Ele também contém informações sobre maneiras de configurar a instância do SQL Server, banco de dados ou tabelas usadas em uma solução. Como o uso de no SQL Server Desfoca a linha entre as otimizações de hardware e de banco de dados, uma terceira seção discute governança de recursos e a relação de CPU em detalhes.

> [!TIP]
> Se você for novo no SQL Server, é altamente recomendável que você também Revise o guia de ajuste de desempenho do SQL Server: [Monitor e ajuste de desempenho](https://docs.microsoft.com/sql/relational-databases/performance/monitor-and-tune-for-performance).

## <a name="hardware-optimization"></a>Otimização de hardware

Otimização do computador do servidor é importante para garantir que você tenha os recursos para executar scripts externos. Quando os recursos forem limitados, você poderá ver os sintomas como estes:

- A execução do trabalho foi adiada ou cancelada para priorizar as outras operações de banco de dados
- Script de R causando erro "cota excedida" para encerrar sem preenchimento
- Dados carregados na memória de R truncada para resultados incompletos

### <a name="memory"></a>Memória

A quantidade de memória disponível no computador pode ter um grande impacto sobre o desempenho de algoritmos analíticos avançados. Memória insuficiente pode afetar o grau de paralelismo ao usar o contexto de computação do SQL. Isso também pode afetar o tamanho da parte (linhas por operação de leitura) que pode ser processada e o número de sessões simultâneas para o qual é possível dar suporte.

Um mínimo de 32 GB é altamente recomendável. Se você tiver mais de 32 GB disponível, você pode configurar a fonte de dados do SQL para usar mais linhas em cada operação de leitura para melhorar o desempenho.

Você também pode gerenciar a memória usada pela instância. Por padrão, o SQL Server é priorizado sobre os processos de script externo quando a memória é alocada. Em uma instalação padrão dos serviços do R, somente 20% da memória disponível é alocado para R.

Normalmente isso não é suficiente para tarefas de ciência de dados, mas não deseja enfraquecer o SQL server de memória. Você deve testar e ajustar a alocação de memória entre scripts externos, sabendo que a configuração ideal varia de acordo com o caso, o mecanismo de banco de dados e serviços relacionados.

Para o modelo de correspondência para continuar, use script externo foi pesada e não houve nenhum outro banco de dados serviços de mecanismo de execução; Portanto, os recursos alocados para scripts externos foram aumentados para 70%, que foi a melhor configuração para o desempenho do script.

### <a name="power-options"></a>Opções de energia

No sistema operacional Windows, o **alto desempenho** opção de energia deve ser usada. Usando uma configuração de energia diferente resulta em desempenho reduzido ou inconsistente quando usar o SQL Server.

### <a name="disk-io"></a>E/S de disco

Treinamento e previsão trabalhos usando os serviços de R são inerentemente e/s associada e dependem da velocidade do disco que o banco de dados é armazenado no. As unidades mais rápidas, como unidades de estado sólidas (SSD) podem ajudar.

A E/S de disco também é afetada pelo acesso de outros aplicativos ao disco: por exemplo, operações de leitura por outros clientes em um banco de dados. O desempenho de E/S de disco também pode ser afetado pelas configurações no sistema de arquivos em uso, tais como o tamanho do bloco utilizado pelo sistema de arquivos.

Se houver várias unidades, solicitações de bancos de dados em uma unidade diferente do SQL Server para que as solicitações para o mecanismo de banco de dados não estão atingindo o mesmo disco de armazenamento de dados armazenados no banco de dados.

A E/S de disco também pode afetar substancialmente o desempenho durante a execução de funções analíticas RevoScaleR que usam várias iterações durante o treinamento. Por exemplo, `rxLogit`, `rxDTree`, `rxDForest`, e `rxBTrees` usam várias iterações. Quando a fonte de dados do SQL Server, esses algoritmos usam arquivos temporários que são otimizados para capturar os dados. Esses arquivos são limpos automaticamente após a conclusão da sessão. Ter um disco de alto desempenho para operações de leitura/gravação pode melhorar significativamente o tempo total decorrido para esses algoritmos.

> [!NOTE]
> Versões anteriores do R Services necessário suporte de nome de arquivo 8.3 em sistemas operacionais Windows. Essa restrição foi eliminada após o Service Pack 1. No entanto, você pode usar fsutil.exe para determinar se uma unidade dá suporte a nomes de 8.3 arquivos ou para habilitar o suporte se não existir.

### <a name="paging-file"></a>Arquivo de paginação

O sistema operacional Windows usa um arquivo de paginação para gerenciar os despejos de memória e para armazenar páginas de memória virtual. Se você observar excesso de paginação, considere aumentar a memória física do computador. Ter mais memória física reduz a necessidade de paginação, embora não elimine a paginação por completo.

A velocidade do disco no qual o arquivo de paginação está armazenado também pode afetar o desempenho. Armazenar o arquivo de paginação em um SSD ou usar vários arquivos de paginação em vários SSDs pode melhorar o desempenho.

Para obter informações sobre o dimensionamento de arquivo de paginação, consulte [como determinar o tamanho do arquivo de página apropriada para versões de 64 bits do Windows](https://support.microsoft.com/en-us/kb/2860880).

## <a name="optimizations-at-instance-or-database-level"></a>Otimizações de nível de instância ou banco de dados

Otimização da instância do SQL Server é a chave para a execução eficiente de scripts externos.

> [!NOTE]
> As definições ideais diferem dependendo do tamanho e tipo de dados, o número de colunas que você está usando para pontuação ou treinar um modelo.
> 
> Você pode examinar os resultados de otimizações específicas no artigo final: [ajuste de desempenho - resultados de estudo de caso](../../advanced-analytics/r/performance-case-study-r-services.md)
> 
> Para scripts de exemplo, consulte separadas [repositório GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning).

### <a name="table-compression"></a>Compactação de tabela

Geralmente, o desempenho de e/s pode ser melhorado usando a compactação ou um repositório de dados de colunas. Em geral, os dados geralmente são repetidos em várias colunas dentro de uma tabela, modo usar columnstore aproveita essas repetições ao compactar os dados.

Columnstore não pode ser mais eficiente se houver várias inserções na tabela, mas é uma boa opção se os dados são estáticos ou altera apenas raramente. Se um repositório em colunas não for apropriado, a habilitação da compactação em uma tabela principal de linha poderá ser usada para melhorar a E/S.

Para obter mais informações, consulte os seguintes documentos:

+ [Compactação de dados](../../relational-databases/data-compression/data-compression.md)

+ [Habilitar a compactação em uma tabela ou índice](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Guia de índices ColumnStore](../../relational-databases/indexes/columnstore-indexes-overview.md)

### <a name="memory-optimized-tables"></a>Tabelas com otimização de memória

Hoje em dia, a memória não é um problema para computadores modernos. Como as especificações de hardware continuam a melhorar, é relativamente fácil de obter os valores ideais RAM. No entanto, ao mesmo tempo, sendo produzidos dados mais rapidamente do que nunca, e os dados devem ser processados com baixa latência.

Tabelas com otimização de memória representam uma solução, em que eles usam a memória grande disponível em computadores avançadas para resolver o problema de dados grandes. Tabelas com otimização de memória principalmente residem na memória, para que os dados lidos do e gravados na memória. Para durabilidade, uma segunda cópia da tabela é mantida em disco e dados é somente leitura do disco durante a recuperação de banco de dados.

Se você precisar de leitura e gravação para tabelas com frequência, tabelas com otimização de memória podem ajudar com alto desempenho e baixa latência.  No cenário de correspondência de retomada, o uso de tabelas com otimização de memória permitido ler todos os recursos de retomada do banco de dados e armazená-los na memória principal, para corresponder com novas oportunidades de trabalho. Isso significativamente reduzido de e/s de disco.

Foram obtidos ganhos de desempenho adicionais usando a tabela com otimização de memória no processo de gravar previsões de volta para o banco de dados de vários lotes simultâneos. O uso de tabelas com otimização de memória no SQL Server habilitada baixa latência na tabela leituras e gravações.

Também foi a experiência perfeita durante o desenvolvimento. Tabelas com otimização de memória foram criadas ao mesmo tempo que o banco de dados foi criado. Portanto, o desenvolvimento usado mesmo fluxo de trabalho, independentemente de onde os dados foram armazenados.

### <a name="processor"></a>Processador

SQL Server pode executar tarefas em paralelo usando núcleos disponíveis na máquina. núcleos que estão disponíveis, melhor o desempenho. Enquanto não pode ajudar a aumentar o número de núcleos para operações de e/s associada, a CPU associada benefício de algoritmos de CPUs mais rápidas com vários núcleos.

Porque o servidor é normalmente usado por vários usuários simultaneamente, o administrador de banco de dados deve determinar o número ideal de núcleos que são necessários para dar suporte a cálculos de carga de trabalho de pico.

### <a name="resource-governance"></a>Governança de recursos

Em edições que dão suporte ao administrador de recursos, você pode usar pools de recursos para especificar que determinadas cargas de trabalho são alocadas a um número de CPUs. Você também pode gerenciar a quantidade de memória alocada para cargas de trabalho específicas.

Governança de recursos no SQL Server permite que você centralize o monitoramento e controle de vários recursos usados pelo SQL Server e por R. Por exemplo, você pode alocar metade a memória disponível para o mecanismo de banco de dados, certifique-se de que core services pode sempre executar apesar transitórias cargas de trabalho mais pesadas.

O valor padrão para o consumo de memória por scripts externos é limitado a 20% do total de memória disponível para o próprio SQL Server. Esse limite é aplicado por padrão para garantir que todas as tarefas que dependem do servidor de banco de dados não são gravemente afetadas por trabalhos de longa execução R. Entretanto, esses limites podem ser alterados pelo administrador de banco de dados. Em muitos casos, o limite de 20% não é suficiente dar suporte a cargas de trabalho do aprendizado de máquina grave.

As opções de configuração com suporte são **MAX_CPU_PERCENT**, **MAX_MEMORY_PERCENT**, e **MAX_PROCESSES**. Para exibir as configurações atuais, use esta instrução:`SELECT * FROM sys.resource_governor_external_resource_pools`

-  Se o servidor é usado principalmente para serviços de R, pode ser útil aumentar MAX_CPU_PERCENT para 40% ou 60%.

-  Se o número de sessões de R deve usar o mesmo servidor ao mesmo tempo, todas as três configurações devem ser aumentadas.

Para alterar os valores de recursos alocados, use instruções T-SQL.

+ Essa instrução define o uso de memória para 40%:`ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)`

+ Essa instrução define todos os três valores configuráveis:`ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`

+ Se você altera uma memória, CPU ou configuração de processo máximo e, em seguida, deseja aplicar as configurações imediatamente, execute esta instrução:`ALTER RESOURCE GOVERNOR RECONFIGURE`

## <a name="soft-numa-hardware-numa-and-cpu-affinity"></a>Afinidade de de software, hardware NUMA e da CPU

Ao usar o SQL Server como o contexto de computação, às vezes você pode obter um melhor desempenho ajustando configurações relacionadas a afinidade de processador e NUMA. 

Sistemas com _de hardware_ tem mais de um barramento de sistema, cada um atendendo a um pequeno conjunto de processadores. Cada CPU pode acessar a memória associada a outros grupos de uma maneira coerente. Cada grupo é chamado de nó NUMA. Se você tiver NUMA de hardware, poderá configurá-lo para usar memória intercalada em vez de NUMA. Nesse caso, Windows e, portanto, o SQL Server não o reconhecerão como NUMA. 

Você pode executar a consulta a seguir para localizar o número de nós de memória disponíveis para o SQL Server:

```SQL
SELECT DISTINCT memory_node_id
FROM sys.dm_os_memory_clerks
```

Se a consulta retorna um nó de memória único (nó 0), você não tem de hardware ou o hardware está configurado como intercalado (não NUMA). SQL Server também ignora de hardware quando há quatro ou menos CPUs, ou se pelo menos um nó tiver apenas uma CPU.

Se o computador tiver vários processadores, mas não tem de hardware, você também pode usar [Soft-NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server) subdividir as CPUs em grupos menores.  No SQL Server 2016 e no SQL Server 2017, o recurso de software é habilitado automaticamente ao iniciar o serviço do SQL Server.

Quando o NUMA é habilitado, o SQL Server gerencia automaticamente os nós para você; No entanto, para otimizar para cargas de trabalho específicas, você pode desabilitar _afinidade flexível_ e configurar manualmente a afinidade de CPU para nós NUMA flexíveis. Isso pode dar a você mais controle sobre quais cargas de trabalho são atribuídas a quais nós, especialmente se você estiver usando uma edição do SQL Server que oferece suporte à administração de recursos. Especificando a afinidade de CPU e alinhamento de pools de recursos com grupos de CPUs, você pode reduzir a latência e certifique-se de que os processos relacionados são executados no mesmo nó NUMA.

O processo geral para a configuração de soft-NUMA e afinidade de CPU para oferecer suporte a cargas de trabalho de R é o seguinte:

1. Habilitar o NUMA, se disponível
2. Definir a afinidade de processador
3. Criar pools de recursos para processos externos, usando [administrador de recursos](../r/resource-governance-for-r-services.md)
4. Atribuir o [grupos de carga de trabalho](../../relational-databases/resource-governor/resource-governor-workload-group.md) para grupos de afinidade específicos

Para obter detalhes, incluindo o código de exemplo, consulte este tutorial: [SQL otimização dicas e truques (Ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**Outros recursos:**

+ [Soft-no SQL Server](https://docs.microsoft.com/en-us/sql/database-engine/configure-windows/soft-numa-sql-server)
    
    Como mapear nós de software para CPUs

+ [Soft-NUMA automático: ele somente é executado mais rápido (Bob Ward)](https://blogs.msdn.microsoft.com/bobsql/2016/06/03/sql-2016-it-just-runs-faster-automatic-soft-numa/)

   Descreve o histórico, bem como os detalhes de implementação, com desempenho em novos servidores de vários núcleos.

## <a name="task-specific-optimizations"></a>Otimizações de tarefas específicas

Esta seção resume os métodos adotados nesses estudos de caso e em outros testes, para otimizar cargas de trabalho do aprendizado de máquina específica. Cargas de trabalho comuns incluem o treinamento do modelo, extração de um recurso e engenharia de recurso e vários cenários de pontuação: única linha, em pequenos lotes e lote grande.

### <a name="feature-engineering"></a>Engenharia de recursos

Um ponto problemático com R é normalmente são processado em uma única CPU. Este é um gargalo de desempenho principais para muitas tarefas, especialmente de engenharia de recurso. Na solução de correspondência para retomar a tarefa de engenharia de recurso sozinha criado 2.500 recursos de produto cruzado que tiveram de ser combinado com os recursos de 100 originais. Essa tarefa deve levar uma quantidade significativa de tempo se tudo foi feito em uma única CPU.

Há várias maneiras de melhorar o desempenho de engenharia de recurso. Você pode otimizar seu código R e manter a extração de um recurso dentro do processo de modelagem ou mover o processo de engenharia de recurso em SQL.

- Usando o R. Definir uma função e, em seguida, passa-a como o argumento para [rxTransform](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxtransform) durante o treinamento. Se o modelo dá suporte ao processamento paralelo, a tarefa de engenharia de recurso pode ser processada com várias CPUs. Usando essa abordagem, a equipe de ciência de dados observados uma melhoria de desempenho de 16% em termos de tempo de pontuação. No entanto, essa abordagem requer um modelo que oferece suporte a paralelização e uma consulta que pode ser executada usando um plano paralelo.

- Contexto de computação usam R com um SQL. Em um ambiente com vários processadores com recursos isolados disponíveis para execução de lotes separados, você pode obter maior eficiência ao isolar as consultas SQL usadas para cada lote, para extrair dados de tabelas e restringir os dados no mesmo grupo de carga de trabalho. Métodos usados para isolar os lotes incluem particionamento e usam o PowerShell para executar consultas separadas em paralelo.

- Execução paralela ad hoc: contexto de computação em um SQL Server, você pode contar com o mecanismo de banco de dados SQL para impor a execução paralela se possível, e se essa opção for encontrada para ser mais eficiente.

- Use T-SQL em um processo separado de personalização. Precomputing os dados de recurso usando SQL é geralmente mais rápido.

### <a name="prediction-scoring-in-parallel"></a>Previsão (classificação) em paralelo

Um dos benefícios do SQL Server é sua capacidade de lidar com um grande volume de linhas em paralelo. Isso é essa vantagem marcada como pontuação. Geralmente o modelo não precisam acessar para todos os dados para pontuação, você pode particionar os dados de entrada, cada grupo de carga de trabalho, uma tarefa de processamento.

Você também pode enviar os dados de entrada como uma única consulta e do SQL Server, em seguida, analisa a consulta. Se um plano de consulta paralela pode ser criado para os dados de entrada, automaticamente atribuídos a nós de dados das partições e executa necessárias junções e agregações em paralelo bem.

Se você estiver interessado nos detalhes de como definir um procedimento armazenado para ser usado na pontuação, consulte o projeto de exemplo no [GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips/SQLR) e procure o arquivo "step5_score_for_matching.sql". O exemplo de script também rastreia início da consulta e horários de término e grava o tempo para o console do SQL para que você possa avaliar o desempenho.

### <a name="concurrent-scoring-using-resource-groups"></a>Pontuação simultâneas usando grupos de recursos

Para dimensionar o problema de pontuação, uma prática recomendada é a adotar a abordagem de Map-reduce na qual milhões de itens são divididos em vários lotes. Em seguida, vários trabalhos de pontuação são executados simultaneamente. Nessa estrutura, os lotes são processados em diferentes conjuntos de CPU, e os resultados são coletados e gravados no banco de dados.

Essa é a abordagem usada no cenário de correspondência de retomar; No entanto, a governança de recursos no SQL Server é essencial para implementar essa abordagem. Configurando grupos de cargas de trabalho para trabalhos de script externo, você pode rotear trabalhos de pontuação para grupos de processador diferente do R e atingir uma taxa de transferência.

Governança de recursos também pode ajudar a alocar dividir os recursos disponíveis no servidor (CPU e memória) para minimizar a concorrência de carga de trabalho. Você pode configurar funções de classificação para distinguir entre diferentes tipos de trabalhos de R: por exemplo, você pode decidir que pontuação chamado a partir de um aplicativo sempre terá prioridade, enquanto trabalhos novos treinamentos tem baixa prioridade. Esse isolamento de recursos potencialmente pode melhorar o tempo de execução e fornecer um desempenho mais previsível.

### <a name="concurrent-scoring-using-powershell"></a>Pontuação simultâneas usando o PowerShell

Se você decidir dividir os dados por conta própria, você pode usar scripts do PowerShell para executar várias tarefas simultâneas de pontuação. Para fazer isso, use o cmdlet Invoke-SqlCmd e iniciar as tarefas de pontuação em paralelo.

No cenário de correspondência de retomada, simultaneidade foi projetada como segue:

- 20 processadores divididas em quatro grupos de cinco CPUs. Cada grupo de CPUs está localizado no mesmo nó NUMA.

- Número máximo de lotes simultâneos foi definido para oito.

- Cada grupo de carga de trabalho deve tratar duas tarefas de pontuação. Assim que uma tarefa concluída leitura de dados e inicia a pontuação, a outra tarefa pode iniciar a leitura de dados do banco de dados.

Para ver os scripts do PowerShell para este cenário, abra o experiment.ps1 de arquivo no [Github projeto](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips).

### <a name="storing-models-for-prediction"></a>Armazenar modelos para previsão

Quando o treinamento e avaliação concluída e você tiver selecionado um modelo de melhor, é recomendável armazenar o modelo no banco de dados para que ele esteja disponível para previsões. Carregar o modelo computado antes do banco de dados para a previsão é eficiente, porque o aprendizado de máquina do SQL Server usa algoritmos de serialização especial para armazenar e carregar modelos ao mover entre R e o banco de dados.

> [!TIP]
> No SQL Server de 2017, você pode usar a função de previsão para executar pontuação mesmo se R não está instalado no servidor. Tipos de modelos limitado têm suporte do pacote RevoScaleR.

No entanto, dependendo do algoritmo usado, alguns modelos podem ser muito grandes, especialmente quando treinado em um grande conjunto de dados. Por exemplo, os algoritmos, como **lm** ou **glm** gerar uma série de dados do resumo juntamente com as regras. Como há limites para o tamanho de um modelo que pode ser armazenado em uma coluna varbinary, recomendamos que você elimine o desnecessários artefatos do modelo antes de armazenar o modelo no banco de dados de produção.

## <a name="articles-in-this-series"></a>Esta série de artigos

[Desempenho de ajuste para R – Introdução](../r/sql-server-r-services-performance-tuning.md)

[Ajuste de desempenho para R - configuração do SQL Server](../r/sql-server-configuration-r-services.md)

[Ajuste de desempenho para R - R otimização de código e dados](../r/r-and-data-optimization-r-services.md)

[Ajuste de desempenho - resultados de estudo de caso](../r/performance-case-study-r-services.md)

