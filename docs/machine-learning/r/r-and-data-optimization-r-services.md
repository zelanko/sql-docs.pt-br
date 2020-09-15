---
title: Ajuste de desempenho para dados
description: Este artigo discute as otimizações de desempenho a scripts do R ou do Python executados no SQL Server. Ele também descreve os métodos que você pode usar para atualizar seu código R, aumentar o desempenho e evitar problemas conhecidos.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 04/15/2018
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 95600d85c02d120f1bb4df2e7a73411a9965550a
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179985"
---
# <a name="performance-for-r-services---data-optimization"></a>Desempenho do R Services – otimização de dados
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Este artigo é o terceiro de uma série que descreve a otimização de desempenho para R Services com base em dois estudos de caso. Este artigo discute as otimizações de desempenho a scripts do R ou do Python executados no SQL Server. Ele também descreve os métodos que você pode usar para atualizar seu código R, aumentar o desempenho e evitar problemas conhecidos.

## <a name="choosing-a-compute-context"></a>Como escolher um contexto de computação

No SQL Server 2016 e 2017, você pode usar o contexto de computação **local** ou **SQL** ao executar o script R ou Python.

Ao usar o contexto de computação **local**, a análise é executada no computador, não no servidor. Portanto, se você estiver obtendo dados do SQL Server para usar em seu código, os dados deverão ser buscados pela rede. O impacto no desempenho incorrido para a transferência de rede depende do tamanho dos dados transferidos, velocidade da rede e outras transferências de rede que ocorrem ao mesmo tempo.

Ao usar o **contexto de computação do SQL Server**, o código é executado no servidor. Se você estiver obtendo dados do SQL Server, eles deverão ser locais para o servidor que executa a análise e, portanto, nenhuma sobrecarga de rede será introduzida. Se você precisar importar dados de outras fontes, considere organizar o ETL antecipadamente.

Ao trabalhar com grandes conjuntos de dados, você sempre deve usar o contexto de computação do SQL.

## <a name="factors"></a>Fatores

A linguagem R tem o conceito de *fatores*, que são variáveis especiais para dados categóricos. Os cientistas de dados geralmente usam variáveis de fator em sua fórmula, pois manipular variáveis categóricas como fatores garante o processamento correto dos dados pelas funções de aprendizado de máquina. Para obter mais informações, confira [Introdução ao R: variáveis de fator](https://www.dummies.com/programming/r/how-to-look-at-the-structure-of-a-factor-in-r/).

As variáveis de fator podem ser convertidas de cadeias de caracteres em inteiros e de volta para fins de armazenamento ou processamento. A função `data.frame` do R processa todas as cadeias de caracteres como variáveis de fator, a menos que o argumento *stringsAsFactors* seja definido como **false**. Isso significa que as cadeias de caracteres são automaticamente convertidas em um inteiro para processamento e depois mapeadas de volta para a cadeia de caracteres original.

Se os dados de origem para fatores forem armazenados como um inteiro, o desempenho poderá ser afetado, pois o R converte os inteiros de fator em cadeias de caracteres no runtime e, em seguida, executa a própria conversão interna de cadeia de caracteres em inteiro.

Para evitar essas conversões de runtime, considere armazenar os valores como inteiros na tabela do SQL Server e usar o argumento _colInfo_ para especificar os níveis para a coluna usada como fator. A maioria dos objetos de fonte de dados no RevoScaleR usa o parâmetro _colInfo_. Você usa esse parâmetro para nomear as variáveis que a fonte de dados usa, especificar seu tipo e definir os níveis de variáveis ou transformações nos valores da coluna.

Por exemplo, a seguinte chamada de função R obtém os inteiros 1, 2 e 3 de uma tabela, mas mapeia os valores para um fator com os níveis "maçã", "laranja" e "banana".

```R
c("fruit" = c(type = "factor", levels=as.character(c(1:3)), newLevels=c("apple", "orange", "banana")))
```

Quando a coluna de origem contém cadeias de caracteres, é sempre mais eficiente especificar os níveis com antecedência usando o parâmetro _colInfo_. Por exemplo, o código R a seguir trata as cadeias de caracteres como fatores à medida que elas estão sendo lidas.

```R
c("fruit" = c(type = "factor", levels= c("apple", "orange", "banana")))
```

Se não há nenhuma diferença semântica na geração de modelo, esta abordagem pode levar a um desempenho melhor.

## <a name="data-transformations"></a>Transformações de dados

Cientistas de dados frequentemente usam funções de transformação escritas em R como parte da análise. As funções de transformação são aplicadas a cada linha recuperada da tabela. No SQL Server, essas transformações são aplicadas a todas as linhas recuperadas em um lote, o que exige comunicação entre o interpretador do R e o mecanismo de análise. Para executar a transformação, os dados se movem do SQL para o mecanismo de análise e, em seguida, para o processo do interpretador de R e vice-versa.

Por esse motivo, usar transformações como parte de seu código R pode ter um efeito adverso significativo no desempenho do algoritmo, dependendo da quantidade de dados envolvidos.

É mais eficiente ter todas as colunas necessárias na tabela ou exibir antes de executar a análise e evitar as transformações durante o cálculo. Se não for possível acrescentar colunas adicionais a tabelas existentes, considere criar outra tabela ou exibir as colunas transformadas e usar uma consulta apropriada para recuperar os dados.

## <a name="batch-row-reads"></a>Leituras de linha em lote

Se você usar uma fonte de dados do SQL Server (`RxSqlServerData`) em seu código, recomendamos tentar usar o parâmetro _rowsPerRead_ para especificar o tamanho do lote. Esse parâmetro define o número de linhas que são consultadas e então enviadas para o script externo para processamento. No runtime, o algoritmo vê apenas o número especificado de linhas em cada lote.

A capacidade de controlar a quantidade de dados processados por vez pode ajudar você a resolver ou evitar problemas. Por exemplo, se o conjunto de dados de entrada for muito largo (tiver muitas colunas) ou tiver algumas colunas grandes (como texto livre), você poderá reduzir o tamanho do lote para evitar falta de memória na paginação de dados.

Por padrão, o valor desse parâmetro é definido como 50.000 para garantir um desempenho razoável mesmo em computadores com pouca memória. Se o servidor tiver memória suficiente disponível, aumente esse valor para 500.000 ou até mesmo um milhão para produzir o melhor desempenho, especialmente em grandes tabelas.

Os benefícios de aumentar o tamanho do lote ficam evidentes em um conjunto de dados grande e em uma tarefa que pode ser executada em vários processos. No entanto, aumentar esse valor nem sempre produzirá os melhores resultados. Recomendamos testar os dados e os algoritmos para determinar o valor ideal.

## <a name="parallel-processing"></a>Processamento paralelo

Para melhorar o desempenho das funções analíticas **rx**, você pode aproveitar a capacidade do SQL Server de executar tarefas em paralelo usando núcleos disponíveis no computador servidor.

Há duas maneiras de obter paralelização com o R no SQL Server:

-   **Usar \@parallel.** Ao usar o procedimento armazenado `sp_execute_external_script` para executar um script de R, defina o parâmetro `@parallel` para `1`. Esse é o melhor método se o script R **não** usa funções RevoScaleR, que têm outros mecanismos para processamento. Caso seu script use funções RevoScaleR (geralmente prefixadas com "RX"), o processamento paralelo será executado automaticamente e você não precisará definir explicitamente `@parallel` como `1`.

    Se o script R e a consulta SQL puderem ser paralelizados, o mecanismo de banco de dados criará vários processos paralelos. O número máximo de processos que podem ser criados é igual à configuração de MAXDOP (**grau máximo de paralelismo**) para a instância. Todos os processos então executam o mesmo script, mas recebem apenas uma parte dos dados.
    
    Portanto, esse método não é útil com scripts que devem ver todos os dados, como ao treinar um modelo. No entanto, é útil ao executar tarefas como a previsão em lotes em paralelo. Para obter mais informações sobre o uso de paralelismo com `sp_execute_external_script`, confira as **Dicas avançadas: processamento em paralelo** de [Usando código R no Transact-SQL](../tutorials/quickstart-r-create-script.md).

-   **Usar numTasks =1.** Ao usar funções **rx** em um contexto de computação do SQL Server, defina o valor do parâmetro _numTasks_ como o número de processos que você deseja criar. O número de processos criados nunca pode ser maior que **MAXDOP**. Porém, o número real de processos criados é determinado pelo mecanismo de banco de dados e pode ser menor que o solicitado.

    Se o script R e a consulta SQL puderem ser paralelizados, o SQL Server criará vários processos paralelos ao executar as funções rx. O número real de processos criados depende de uma variedade de fatores, como o controle de recursos, uso atual de recursos, outras sessões e o plano de execução de consulta para a consulta usada com o script R.

## <a name="query-parallelization"></a>Paralelização de consulta

No Microsoft R, você pode trabalhar com fontes de dados do SQL Server definindo os dados como um objeto de fonte de dados RxSqlServerData.

Cria uma fonte de dados com base em uma tabela ou exibição inteira:

```R
RxSqlServerData(table= "airline", connectionString = sqlConnString)
```

Cria uma fonte de dados com base em uma consulta SQL:

```R
RxSqlServerData(sqlQuery= "SELECT [ArrDelay],[CRSDepTime],[DayOfWeek] FROM  airlineWithIndex WHERE rowNum <= 100000", connectionString = sqlConnString)
```

> [!NOTE]
> Se uma tabela for especificada na fonte de dados em vez de uma consulta, o R Services usará heurística interna para determinar as colunas necessárias a serem buscadas na tabela. No entanto, é improvável que essa abordagem resulte na execução em paralelo.

Para garantir que os dados possam ser analisados em paralelo, a consulta usada para recuperar os dados deve ser estruturada de modo que o mecanismo de banco de dados possa criar um plano de consulta paralelo. Se o código ou algoritmo usar grandes volumes de dados, a consulta fornecida para `RxSqlServerData` deve estar otimizada para execução paralela. Uma consulta que não resulta em um plano de execução paralela pode resultar em um único processo de computação.

Se você precisar trabalhar com grandes conjuntos de dados, use o Management Studio ou outro analisador de consultas SQL antes de executar o código R para analisar o plano de execução. Em seguida, execute as etapas recomendadas para melhorar o desempenho da consulta. Por exemplo, um índice ausente em uma tabela pode afetar o tempo necessário para executar uma consulta. Para obter mais informações, confira [Monitorar e ajustar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md).

Outro erro comum que pode afetar o desempenho é que uma consulta recupera mais colunas do que o necessário. Por exemplo, se uma fórmula for baseada em apenas três colunas, mas a tabela de origem tiver 30 colunas, você estará movendo os dados desnecessariamente.

 + Evite usar `SELECT *`!
 + Reserve algum tempo para examinar as colunas no conjunto de registros e identificar apenas as necessárias para análise
 + Remova de suas consultas todas as colunas que contenham tipos de dados incompatíveis com código R, como GUIDS e rowguids
 + Verificar se há formatos de data e hora sem suporte
 + Em vez de carregar uma tabela, crie uma exibição que selecione determinados valores ou converta colunas para evitar erros de conversão

## <a name="optimizing-the-machine-learning-algorithm"></a>Como otimizar o algoritmo de aprendizado de máquina

Esta seção apresenta dicas e recursos diversos específicos do RevoScaleR e outras opções no Microsoft R.

> [!TIP]
> Uma discussão geral de otimização do R está fora do escopo deste artigo. Porém, se você precisar tornar seu código mais rápido, recomendamos o artigo popular, [The R Inferno](https://www.burns-stat.com/pages/Tutor/R_inferno.pdf). Ele aborda constructos de programação em R e armadilhas comuns em detalhes e linguagem vívida, além de apresentar muitos exemplos específicos de técnicas de programação em R.

### <a name="optimizations-for-revoscaler"></a>Otimizações para RevoScaleR

Muitos algoritmos de RevoScaleR dão suporte a parâmetros para controlar como o modelo de treinado é gerado. Embora a precisão e a exatidão do modelo seja importante, o desempenho do algoritmo pode ser igualmente importante. Para obter o equilíbrio certo entre precisão e tempo de treinamento, modifique os parâmetros para aumentar a velocidade de computação e, em muitos casos, melhorar o desempenho sem reduzir a precisão ou a exatidão.

+ [rxDTree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)

    `rxDTree` dá suporte ao parâmetro `maxDepth`, que controla a profundidade da árvore de decisão. Como `maxDepth` é aumentado, o desempenho pode diminuir, portanto, é importante analisar os benefícios de aumentar a profundidade versus prejudicar o desempenho.

    Você também pode controlar o equilíbrio entre a complexidade de tempo e a precisão da previsão ajustando parâmetros como `maxNumBins`, `maxDepth`, `maxComplete` e `maxSurrogate`. Aumentar a profundidade além de 10 ou 15 pode deixar o cálculo muito caro.

+ [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)

    Tente usar o argumento `cube` se a primeira variável dependente na fórmula for uma variável de fator.
    
    Quando `cube` é definido como `TRUE`, a regressão é realizado usando um inverso particionado, o que pode ser mais rápido e consumir menos memória que a computação de regressão padrão. Se a fórmula tiver um grande número de variáveis, o ganho de desempenho poderá ser significativo.

+ [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)

    Use o argumento `cube` se a primeira variável dependente for uma variável de fator.
    
    Quando `cube` é definido como `TRUE`, o algoritmo usa um inverso particionado, o que pode ser mais rápido e consumir menos memória. Se a fórmula tiver um grande número de variáveis, o ganho de desempenho poderá ser significativo.

Para obter mais diretrizes sobre a otimização do RevoScaleR, confira estes artigos:

+ Artigo de suporte: [Opções de ajuste de desempenho para rxDForest e rxDTree](https://support.microsoft.com/kb/3104235)

+ Métodos para controlar o ajuste de modelo em modelo de árvore aprimorado: [Como estimar modelos usando o gradient boosting estocástico](https://docs.microsoft.com/r-server/r/how-to-revoscaler-boosting)

+ Visão geral de como o RevoScaleR move e processa os dados: [Gravar algoritmos de agrupamento personalizados no ScaleR](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ Modelo de programação para RevoScaleR: [como gerenciar threads no RevoScaleR](https://docs.microsoft.com/r-server/r/how-to-developer-manage-threads)

+ Referência de função para [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

+ Referência de função para [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)

### <a name="use-microsoftml"></a>Usar o MicrosoftML

Também recomendamos examinar o novo pacote **MicrosoftML**, que fornece algoritmos escalonáveis de aprendizado de máquina que podem usar os contextos de computação e as transformações fornecidas pelo RevoScaleR.

+ [Introdução ao MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)

+ [Como escolher um algoritmo do MicrosoftML](https://docs.microsoft.com/r-server/r/how-to-choose-microsoftml-algorithms-cheatsheet)

### <a name="operationalize-a-solution-using-microsoft-r-server"></a>Operacionalizar uma solução usando o Microsoft R Server

Se o seu cenário envolve a previsão rápida usando um modelo armazenado ou a integração de aprendizado de máquina em um aplicativo, você pode usar os recursos de [operacionalização](https://docs.microsoft.com/r-server/what-is-operationalization) no Microsoft R Server (anteriormente conhecido como DeployR).

+ Como um **cientistas de dados**, use o [pacote mrsdeploy](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package) para compartilhar código R com outros computadores e integrar a análise de R em aplicativos Web, de desktop, de dispositivo móvel e de painel: [Como publicar e gerenciar serviços Web do R no R Server](https://docs.microsoft.com/r-server/operationalize/how-to-deploy-web-service-publish-manage-in-r)

+ Como um **administrador**, saiba como gerenciar pacotes, monitorar nós da Web e nós de computação e controlar a segurança em trabalhos do R: [Como interagir com serviços Web no R e consumi-los](https://docs.microsoft.com/r-server/operationalize/how-to-consume-web-service-interact-in-r)

## <a name="articles-in-this-series"></a>Artigos nesta série

[Ajuste de desempenho para R – Introdução](sql-server-r-services-performance-tuning.md)

[Ajuste de desempenho para R – configuração do SQL Server](sql-server-configuration-r-services.md)

[Ajuste de desempenho para R – otimização de dados e código do R](r-and-data-optimization-r-services.md)

[Ajuste de desempenho – resultados do estudo de caso](performance-case-study-r-services.md)
