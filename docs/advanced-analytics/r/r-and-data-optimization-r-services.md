---
title: Ajuste de desempenho para otimização de dados
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a8143bae69e85ecf0056dcb9433707a681a69077
ms.sourcegitcommit: 2f56848ec422845ee81fb84ed321a716c677aa0e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2019
ms.locfileid: "71271887"
---
# <a name="performance-for-r-services---data-optimization"></a>Desempenho do R Services – otimização de dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo é o terceiro de uma série que descreve a otimização de desempenho para o R Services com base em dois estudos de caso. Este artigo discute otimizações de desempenho para scripts de R ou Python que são executados no SQL Server. Ele também descreve os métodos que você pode usar para atualizar seu código R, para aumentar o desempenho e para evitar problemas conhecidos.

## <a name="choosing-a-compute-context"></a>Escolhendo um contexto de computação

No SQL Server 2016 e 2017, você pode usar o contexto de computação **local** ou **SQL** ao executar o script R ou Python.

Ao usar o contexto de computação **local** , a análise é executada no computador e não no servidor. Portanto, se você estiver obtendo dados de SQL Server para usar em seu código, os dados devem ser buscados pela rede. O impacto no desempenho incorrido para a transferência de rede depende do tamanho dos dados transferidos, velocidade da rede e outras transferências de rede que ocorrem ao mesmo tempo.

Ao usar o **contexto de computação SQL Server**, o código é executado no servidor. Se você estiver obtendo dados de SQL Server, os dados deverão ser locais para o servidor que executa a análise e, portanto, nenhuma sobrecarga de rede será introduzida. Se você precisar importar dados de outras fontes, considere organizar o ETL antecipadamente.

Ao trabalhar com grandes conjuntos de dados, você sempre deve usar o contexto de computação do SQL.

## <a name="factors"></a>Fatores

A linguagem R tem o conceito de *fatores*, que são variáveis especiais para dados categóricos. Os cientistas de dados geralmente usam variáveis de fator em sua fórmula, pois manipular variáveis categóricas como fatores garante que os dados sejam processados corretamente pelas funções de aprendizado de máquina. Para obter mais informações, [consulte R para cópias: Variáveis](https://www.dummies.com/programming/r/how-to-look-at-the-structure-of-a-factor-in-r/)de fator.

Por design, variáveis de fator podem ser convertidas de cadeias de caracteres para inteiros e de volta para armazenamento ou processamento. A função `data.frame` R manipula todas as cadeias de caracteres como variáveis de fator, a menos que o argumento *stringsAsFactors* seja definido como **false**. Isso significa que as cadeias de caracteres são automaticamente convertidas em um inteiro para processamento e, em seguida, mapeadas de volta para a cadeia de caracteres original.

Se os dados de origem de fatores forem armazenados como um inteiro, o desempenho poderá ser afetado, pois o R converte os inteiros de fator em cadeias de caracteres em tempo de execução e, em seguida, executa sua própria conversão interna de cadeia de caracteres em inteiro.

Para evitar essas conversões de tempo de execução, considere armazenar os valores como inteiros na tabela de SQL Server e usar o argumento _colInfo_ para especificar os níveis para a coluna usada como fator. A maioria dos objetos de fonte de dados no RevoScaleR assumem o parâmetro _colInfo_. Você usa esse parâmetro para nomear as variáveis usadas pela fonte de dados, especificar seu tipo e definir os níveis de variáveis ou transformações nos valores da coluna.

Por exemplo, a seguinte chamada de função R Obtém os inteiros 1, 2 e 3 de uma tabela, mas mapeia os valores para um fator com os níveis "Apple", "laranja" e "banana".

```R
c("fruit" = c(type = "factor", levels=as.character(c(1:3)), newLevels=c("apple", "orange", "banana")))
```

Quando a coluna de origem contém cadeias de caracteres, é sempre mais eficiente especificar os níveis antecipadamente usando o parâmetro _colInfo_ . Por exemplo, o código R a seguir trata as cadeias de caracteres como fatores à medida que elas estão sendo lidas.

```R
c("fruit" = c(type = "factor", levels= c("apple", "orange", "banana")))
```

Se não houver nenhuma diferença semântica na geração do modelo, a última abordagem poderá levar a um melhor desempenho.

## <a name="data-transformations"></a>Transformações de dados

Cientistas de dados frequentemente usam funções de transformação escritas em R como parte da análise. A função de transformação é aplicada a cada linha recuperada da tabela. Em SQL Server, essas transformações são aplicadas a todas as linhas recuperadas em um lote, o que exige a comunicação entre o interpretador de R e o mecanismo de análise. Para executar a transformação, os dados se movem do SQL para o mecanismo de análise e, em seguida, para o processo do interpretador de R e vice-versa.

Por esse motivo, o uso de transformações como parte do código R pode ter um efeito adverso significativo no desempenho do algoritmo, dependendo da quantidade de dados envolvidos.

É mais eficiente ter todas as colunas necessárias na tabela ou exibição antes de executar a análise e evitar transformações durante a computação. Se não for possível acrescentar colunas adicionais a tabelas existentes, considere criar outra tabela ou exibir as colunas transformadas e usar uma consulta apropriada para recuperar os dados.

## <a name="batch-row-reads"></a>Leituras de linha do lote

Se você usar uma fonte de dados de`RxSqlServerData`SQL Server () em seu código, recomendamos que você tente usar o parâmetro _rowsPerRead_ para especificar o tamanho do lote. Esse parâmetro define o número de linhas que são consultadas e, em seguida, enviadas para o script externo para processamento. No tempo de execução, o algoritmo vê apenas o número especificado de linhas em cada lote.

A capacidade de controlar a quantidade de dados processados por vez pode ajudá-lo a resolver ou evitar problemas. Por exemplo, se o conjunto de dados de entrada for muito largo (tem muitas colunas), ou se o conjunto tiver algumas colunas grandes (como texto livre), você poderá reduzir o tamanho do lote para evitar a paginação de dados fora da memória.

Por padrão, o valor desse parâmetro é definido como 50000, para garantir um desempenho razoável mesmo em computadores com pouca memória. Se o servidor tiver memória suficiente disponível, aumentar esse valor para 500.000 ou até mesmo um milhão pode gerar um melhor desempenho, especialmente para tabelas grandes.

Os benefícios do aumento do tamanho do lote se tornam evidentes em um grande conjunto de dados e em uma tarefa que pode ser executada em vários processos. No entanto, aumentar esse valor nem sempre produzirá os melhores resultados. Recomendamos que você teste seus dados e algoritmos para determinar o valor ideal.

## <a name="parallel-processing"></a>Processamento paralelo

Para melhorar o desempenho das funções analíticas **RX** , você pode aproveitar a capacidade de SQL Server executar tarefas em paralelo usando núcleos disponíveis no computador servidor.

Há duas maneiras de obter paralelização com R no SQL Server:

-   **Use \@Parallel.** Ao usar o procedimento armazenado `sp_execute_external_script` para executar um script de R, defina o parâmetro `@parallel` para `1`. Esse é o melhor método se o script R não **usar funções** RevoScaleR, que têm outros mecanismos para processamento. Se o seu script usar funções RevoScaleR (geralmente prefixadas com "RX"), o processamento paralelo será executado automaticamente e você não precisará `@parallel` definir `1`explicitamente como.

    Se o script R puder ser paralelizado e se a consulta SQL puder ser paralelizada, o mecanismo de banco de dados criará vários processos paralelos. O número máximo de processos que podem ser criados é igual à configuração do **grau máximo de paralelismo** (MAXDOP) para a instância. Em seguida, todos os processos executam o mesmo script, mas recebem apenas uma parte dos dados.
    
    Portanto, esse método não é útil com scripts que devem ver todos os dados, como ao treinar um modelo. No entanto, é útil ao executar tarefas como a previsão em lotes em paralelo. Para obter mais informações sobre como usar o `sp_execute_external_script`paralelismo com o, consulte a seção **dicas avançadas: processamento paralelo** de [usando o código R no Transact-SQL](../tutorials/quickstart-r-create-script.md).

-   **Use numTasks = 1.** Ao usar funções **RX** em um contexto de computação SQL Server, defina o valor do parâmetro _numTasks_ como o número de processos que você deseja criar. O número de processos criados nunca pode ser maior que **MAXDOP**; no entanto, o número real de processos criados é determinado pelo mecanismo de banco de dados e pode ser menor que o solicitado.

    Se o script R puder ser paralelizado e se a consulta SQL puder ser paralelizada, SQL Server criará vários processos paralelos ao executar as funções RX. O número real de processos criados depende de uma variedade de fatores, como governança de recursos, uso atual de recursos, outras sessões e o plano de execução de consulta para a consulta usada com o script R.

## <a name="query-parallelization"></a>Paralelização de consulta

No Microsoft R, você pode trabalhar com SQL Server fontes de dados definindo os dados como um objeto de fonte de dados RxSqlServerData.

Cria uma fonte de dados com base em uma tabela ou exibição inteira:

```R
RxSqlServerData(table= "airline", connectionString = sqlConnString)
```

Cria uma fonte de dados com base em uma consulta SQL:

```R
RxSqlServerData(sqlQuery= "SELECT [ArrDelay],[CRSDepTime],[DayOfWeek] FROM  airlineWithIndex WHERE rowNum <= 100000", connectionString = sqlConnString)
```

> [!NOTE]
> Se uma tabela for especificada na fonte de dados em vez de uma consulta, o R Services usará heurística interna para determinar as colunas necessárias a serem buscadas da tabela; no entanto, essa abordagem é improvável de resultar em execução paralela.

Para garantir que os dados possam ser analisados em paralelo, a consulta usada para recuperar os dados deve ser enquadrada de forma que o mecanismo de banco de dados possa criar um plano de consulta paralelo. Se o código ou algoritmo usar grandes volumes de dados, certifique-se de que a consulta `RxSqlServerData` fornecida é otimizada para execução paralela. Uma consulta que não resulta em um plano de execução paralela pode resultar em um único processo de computação.

Se você precisar trabalhar com grandes conjuntos de altos, use Management Studio ou outro analisador de consultas SQL antes de executar o código R, para analisar o plano de execução. Em seguida, execute as etapas recomendadas para melhorar o desempenho da consulta. Por exemplo, um índice ausente em uma tabela pode afetar o tempo necessário para executar uma consulta. Para obter mais informações, consulte [monitorar e ajustar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md).

Outro erro comum que pode afetar o desempenho é que uma consulta recupera mais colunas do que as necessárias. Por exemplo, se uma fórmula for baseada em apenas três colunas, mas a tabela de origem tiver 30 colunas, você estará movendo os dados desnecessariamente.

 + Evite usar `SELECT *`!
 + Reserve algum tempo para examinar as colunas no conjunto de registros e identificar apenas as necessárias para análise
 + Remover de suas consultas quaisquer colunas que contenham tipos de dados que são incompatíveis com o código R, como GUIDs e RowGuids
 + Verificar se há formatos de data e hora sem suporte
 + Em vez de carregar uma tabela, crie uma exibição que selecione determinados valores ou converta colunas para evitar erros de conversão

## <a name="optimizing-the-machine-learning-algorithm"></a>Otimizando o algoritmo de aprendizado de máquina

Esta seção fornece dicas e recursos diversos específicos para o RevoScaleR e outras opções no Microsoft R.

> [!TIP]
> Uma discussão geral sobre a otimização do R está fora do escopo deste artigo. No entanto, se você precisar tornar seu código mais rápido, recomendamos o artigo popular [do R inferno](https://www.burns-stat.com/pages/Tutor/R_inferno.pdf). Ele aborda construções de programação em R e armadilhas comuns em linguagem e detalhes vívidas e fornece vários exemplos específicos de técnicas de programação de R.

### <a name="optimizations-for-revoscaler"></a>Otimizações para RevoScaleR

Muitos algoritmos RevoScaleR dão suporte a parâmetros para controlar como o modelo treinado é gerado. Embora a precisão e a exatidão do modelo sejam importantes, o desempenho do algoritmo pode ser igualmente importante. Para obter o equilíbrio certo entre precisão e tempo de treinamento, você pode modificar parâmetros para aumentar a velocidade de computação e, em muitos casos, melhorar o desempenho sem reduzir a precisão ou a exatidão.

+ [rxDTree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)

    `rxDTree`dá suporte `maxDepth` ao parâmetro, que controla a profundidade da árvore de decisão. À `maxDepth` medida que aumenta, o desempenho pode diminuir, portanto, é importante analisar os benefícios de aumentar a profundidade versus o desempenho do prejudicando.

    Você também pode controlar o equilíbrio entre a complexidade do tempo e a precisão da previsão ajustando `maxNumBins`parâmetros `maxDepth`como `maxComplete`,, `maxSurrogate`e. Aumentar a profundidade além de 10 ou 15 pode deixar o cálculo muito caro.

+ [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)

    Tente usar o `cube` argumento se a primeira variável dependente na fórmula for uma variável de fator.
    
    Quando `cube` é definido como `TRUE`, a regressão é executada usando um inverso particionado, que pode ser mais rápido e usar menos memória do que a computação de regressão padrão. Se a fórmula tiver um grande número de variáveis, o ganho de desempenho poderá ser significativo.

+ [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)

    Use o `cube` argumento se a primeira variável dependente for uma variável de fator.
    
    Quando `cube` é definido como `TRUE`, o algoritmo usa um inverso particionado, que pode ser mais rápido e usar menos memória. Se a fórmula tiver um grande número de variáveis, o ganho de desempenho poderá ser significativo.

Para obter diretrizes adicionais sobre a otimização do RevoScaleR, consulte estes artigos:

+ Artigo de suporte: [Opções de ajuste de desempenho para rxDForest e rxDTree](https://support.microsoft.com/kb/3104235)

+ Métodos para controlar o modelo se ajustam a um modelo de árvore aprimorado: [Estimando modelos usando o aumento de gradiente estocástico](https://docs.microsoft.com/r-server/r/how-to-revoscaler-boosting)

+ Visão geral de como o RevoScaleR move e processa os dados: [Gravar algoritmos de agrupamento personalizados no scaler](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ Modelo de programação para RevoScaleR: [Gerenciando threads no RevoScaleR](https://docs.microsoft.com/r-server/r/how-to-developer-manage-threads)

+ Referência de função para [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

+ Referência de função para [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)

### <a name="use-microsoftml"></a>Usar MicrosoftML

Também recomendamos que você examine o novo pacote **MicrosoftML** , que fornece algoritmos escalonáveis de aprendizado de máquina que podem usar os contextos de computação e as transformações fornecidas pelo RevoScaleR.

+ [Introdução ao MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)

+ [Como escolher um algoritmo MicrosoftML](https://docs.microsoft.com/r-server/r/how-to-choose-microsoftml-algorithms-cheatsheet)

### <a name="operationalize-a-solution-using-microsoft-r-server"></a>Colocar uma solução em operação usando Microsoft R Server

Se o seu cenário envolve a previsão rápida usando um modelo armazenado ou integrando o Machine Learning em um aplicativo, você pode usar os recursos de [operacionalização](https://docs.microsoft.com/r-server/what-is-operationalization) no Microsoft R Server (anteriormente conhecido como implantador).

+ Como um **cientista de dados**, use o [pacote mrsdeploy](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package) para compartilhar o código r com outros computadores e integrar a análise de r nos aplicativos Web, desktop, Mobile e Dashboard: [Como publicar e gerenciar serviços Web do R no R Server](https://docs.microsoft.com/r-server/operationalize/how-to-deploy-web-service-publish-manage-in-r)

+ Como **administrador**, saiba como gerenciar pacotes, monitorar nós da Web e nós de computação e controlar a segurança em trabalhos do R: [Como interagir com e consumir serviços Web em R](https://docs.microsoft.com/r-server/operationalize/how-to-consume-web-service-interact-in-r)

## <a name="articles-in-this-series"></a>Artigos desta série

[Ajuste de desempenho para R-introdução](sql-server-r-services-performance-tuning.md)

[Ajuste de desempenho para configuração de SQL Server R](sql-server-configuration-r-services.md)

[Ajuste de desempenho para otimização de dados e código R-R](r-and-data-optimization-r-services.md)

[Ajuste de desempenho-resultados do estudo de caso](performance-case-study-r-services.md)
