---
title: "Desempenho de serviços do R - otimização dados | Microsoft Docs"
ms.custom: 
ms.date: 07/12/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b6104878-ed19-47a7-ac37-21e4d6e2a1af
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 0ca7a57b10787ca183c2979fe95a5e3fe446dc86
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2018
---
# <a name="performance-for-r-services---data-optimization"></a>Desempenho de serviços do R - otimização de dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo é o terceiro de uma série que descreve a otimização de desempenho para serviços de R com base em dois estudos de caso. Este artigo discute as otimizações de desempenho para R ou Python scripts que são executados no SQL Server. Ele também descreve métodos que você pode usar para atualizar seu código R, para melhorar o desempenho e evitar problemas conhecidos.

## <a name="choosing-a-compute-context"></a>Escolhendo um contexto de computação

No SQL Server 2016 e de 2017, você pode usar o **local** ou **SQL** contexto de computação ao executar script R ou Python.

Ao usar o **local** contexto de computação, análise é executado em seu computador e não no servidor. Portanto, se você estiver obtendo dados do SQL Server para usar em seu código, os dados devem ser buscados através da rede. O impacto no desempenho incorrido para a transferência de rede depende do tamanho dos dados transferidos, velocidade da rede e outras transferências de rede que ocorrem ao mesmo tempo.

Ao usar o **contexto de computação do SQL Server**, o código é executado no servidor. Se você estiver obtendo dados do SQL Server, os dados devem ser locais para o servidor que executa a análise e, portanto, não há sobrecarga de rede é introduzida. Se você precisar importar dados de outras fontes, considere organizando ETL com antecedência.

Ao trabalhar com grandes conjuntos de dados, você sempre deve usar o contexto de computação do SQL.

## <a name="factors"></a>Fatores

A linguagem R tem o conceito de "fatores", que são variáveis especiais para dados categóricos. Os cientistas de dados geralmente usa variáveis de fator em sua fórmula, porque variáveis categóricas como fatores de tratamento assegura que os dados é processado corretamente por funções de aprendizado de máquina. Para obter mais informações, consulte [R para cópias: fator variáveis] (http://www.dummies.com/programming/r/how-to-look-at-the-structure-of-a-factor-in-r/).

Por design, variáveis de fator podem ser convertidos de cadeias de caracteres para números inteiros e voltar novamente para armazenamento ou processamento. R `data.frame` função manipula todas as cadeias de caracteres como variáveis de fator, a menos que o argumento *stringsAsFactors* é definido como **False**. Isso significa é que cadeias de caracteres são automaticamente convertido em um inteiro para o processamento e, em seguida, mapeado de volta para a cadeia de caracteres original.

Se os dados de origem para fatores são armazenados como um número inteiro, o desempenho pode sofrer, como R converte os inteiros de fator em cadeias de caracteres em tempo de execução e, em seguida, executa sua própria conversão de cadeia de caracteres em inteiro interno.

Para evitar tais conversões de tempo de execução, considere armazenar os valores como inteiros na tabela do SQL Server e usar o _colInfo_ argumento para especificar os níveis para a coluna usada como um fator. A maioria dos objetos de fonte de dados em RevoScaleR utilizar o parâmetro _colInfo_. Você pode usar esse parâmetro para nomear as variáveis usadas pela fonte de dados, especifique seu tipo e definir os níveis de variáveis ou transformações nos valores de coluna.

Por exemplo, a chamada de função de R a seguir obtém os inteiros de 1, 2 e 3 de uma tabela, mas mapeia os valores para um fator com níveis de "apple", "laranja" e "banana".

```R
c("fruit" = c(type = "factor", levels=as.character(c(1:3)), newLevels=c("apple", "orange", "banana")))
```

Quando a coluna de origem contém cadeias de caracteres, ele sempre é mais eficiente para especificar os níveis antes do tempo usando o _colInfo_ parâmetro. Por exemplo, o seguinte código R trata as cadeias de caracteres como fatores, como eles estão sendo lidos.

```R
c("fruit" = c(type = "factor", levels= c("apple", "orange", "banana")))
```

Se não houver nenhuma diferença semântica na geração de modelo, a última abordagem pode levar a um desempenho melhor.

## <a name="data-transformations"></a>Transformações de dados

Cientistas de dados frequentemente usam funções de transformação escritas em R como parte da análise. A função de transformação é aplicada a cada linha recuperada da tabela. No SQL Server, essas transformações são aplicadas a todas as linhas recuperadas em um lote, que exige a comunicação entre o interpretador de R e o mecanismo de análise. Para executar a transformação, os dados se movem do SQL para o mecanismo de análise e, em seguida, para o processo do interpretador de R e vice-versa.

Por esse motivo, usando transformações como parte do seu código R pode ter um efeito adverso significativo sobre o desempenho do algoritmo, dependendo da quantidade de dados envolvidos.

É mais eficiente para que todas as colunas necessárias da tabela ou exibição antes de executar a análise e evitar transformações durante o cálculo. Se não for possível acrescentar colunas adicionais a tabelas existentes, considere criar outra tabela ou exibir as colunas transformadas e usar uma consulta apropriada para recuperar os dados.

## <a name="batch-row-reads"></a>Leituras de linha do lote

Se você usar uma fonte de dados do SQL Server (`RxSqlServerData`) no seu código, é recomendável que você tente usar o parâmetro _rowsPerRead_ para especificar o tamanho do lote. Esse parâmetro define o número de linhas que são consultados e, em seguida, enviada para o script externo para processamento. Em tempo de execução, o algoritmo vê apenas o número especificado de linhas em cada lote.

A capacidade de controlar a quantidade de dados que são processados por vez pode ajudá-lo a resolver ou evitar problemas. Por exemplo, se o conjunto de dados de entrada é muito grande (tiver muitas colunas), ou se o conjunto de dados tem algumas colunas grandes (como texto livre), você pode reduzir o tamanho do lote para evitar paginar os dados sem memória.

Por padrão, o valor desse parâmetro é definido como 50000, para garantir um desempenho razoável até mesmo em computadores com pouca memória. Se o servidor tem memória suficiente disponível, aumentar esse valor para 500.000 ou até mesmo milhões pode resultar em melhor desempenho, especialmente para tabelas grandes.

Os benefícios de aumentar o tamanho de lote são evidentes em um grande conjunto de dados e em uma tarefa que pode ser executado em vários processos. No entanto, o aumento desse valor não sempre produzir os melhores resultados. É recomendável fazer experiências com seus dados e o algoritmo para determinar o valor ideal.

## <a name="parallel-processing"></a>Processamento paralelo

Para melhorar o desempenho de **rx** funções analíticas, você pode aproveitar a capacidade de executar tarefas em paralelo usando núcleos disponíveis no computador do servidor do SQL Server.

Há duas maneiras de obter paralelização com R no SQL Server:

-   **Use \@paralela.** Ao usar o procedimento armazenado `sp_execute_external_script` para executar um script de R, defina o parâmetro `@parallel` para `1`. Este é o melhor método se seu script R não **não** usar funções de RevoScaleR, que têm outros mecanismos para processamento. Se o script usa funções de RevoScaleR (geralmente prefixadas com "r"), o processamento paralelo é executado automaticamente e você não precisa definir explicitamente `@parallel` para `1`.

    Se o script de R pode ser colocadas em paralelo, e se a consulta SQL pode ser colocado em paralelo, em seguida, o mecanismo de banco de dados cria vários processos paralelos. O número máximo de processos que podem ser criadas é igual a **grau máximo de paralelismo** configuração (MAXDOP) para a instância. Todos os processos, em seguida, execute o mesmo script, mas recebem apenas uma parte dos dados.
    
    Portanto, esse método não é útil com scripts que devem ver todos os dados, como quando um modelo de treinamento. No entanto, é útil ao executar tarefas como a previsão em lotes em paralelo. Para obter mais informações sobre como usar o paralelismo com `sp_execute_external_script`, consulte o **avançado dicas: processamento paralelo** seção [código R usando Transact-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md).

-   **Use numTasks = 1.** Ao usar **rx** funções em um contexto de computação do SQL Server, defina o valor da _numTasks_ parâmetro para o número de processos que você deseja criar. O número de processos criados nunca pode ser mais de **MAXDOP**; no entanto, o número real de processos criado é determinado pelo mecanismo de banco de dados, e pode ser menor do que você solicitou.

    Se o script de R pode ser colocadas em paralelo, e se a consulta SQL pode ser colocado em paralelo, o SQL Server cria vários processos paralelos, ao executar as funções de rx. O número real de processos que são criados depende de uma variedade de fatores, como o controle de recursos, o uso atual de recursos, outras sessões e o plano de execução de consulta para a consulta usada com o script R.

## <a name="query-parallelization"></a>Paralelização de consultas

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
> Se uma tabela for especificada na fonte de dados em vez de uma consulta, R Services usa heurística interna para determina as colunas necessárias para buscar da tabela; No entanto, essa abordagem é improvável que resultam em execução em paralelo.

Para garantir que os dados podem ser analisados em paralelo, a consulta usada para recuperar os dados deve ser estruturada de forma que o mecanismo de banco de dados pode criar um plano de consulta paralela. Se o código ou o algoritmo usa grandes volumes de dados, verifique se a consulta fornecida ao `RxSqlServerData` é otimizado para execução paralela. Uma consulta que não resulta em um plano de execução paralela pode resultar em um único processo de computação.

Se você precisar trabalhar com grandes conjuntos de dados, use o Management Studio ou o outro analisador de consultas do SQL antes de executar seu código R, para analisar o plano de execução. Em seguida, execute as etapas recomendadas para melhorar o desempenho da consulta. Por exemplo, um índice ausente em uma tabela pode afetar o tempo necessário para executar uma consulta. Para obter mais informações, consulte [monitorar e ajustar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md).

Outro erro comum que pode afetar o desempenho é uma consulta recupera mais colunas que são necessárias. Por exemplo, se uma fórmula se baseia apenas três colunas, mas sua tabela de origem tem 30 colunas, você está movendo dados desnecessariamente.

 + Evite usar `SELECT *`!
 + Reserve algum tempo para examinar as colunas no conjunto de dados e identificar apenas aqueles necessários para análise
 + Remova todas as colunas que contêm tipos de dados que são incompatíveis com o código de R, como GUIDS e rowguids suas consultas
 + Verificação de suporte para formatos de data e hora
 + Em vez de carregar uma tabela, criar uma exibição que seleciona certos valores ou converte colunas para evitar erros de conversão

## <a name="optimizing-the-machine-learning-algorithm"></a>Otimizando o algoritmo de aprendizado de máquina

Esta seção fornece dicas diversas e recursos que são específicos para RevoScaleR e outras opções no Microsoft R.

> [!TIP]
> Uma discussão geral de otimização de R está fora do escopo deste artigo. No entanto, se você precisar fazer o seu código mais rápido, recomendamos o artigo popular, [o Inferno de R](http://www.burns-stat.com/pages/Tutor/R_inferno.pdf). Ele aborda as construções de programação em R e armadilhas comuns no idioma vívido e detalhes e fornece muitos exemplos específicos de técnicas de programação R.

### <a name="optimizations-for-revoscaler"></a>Otimizações para RevoScaleR

Muitos algoritmos de RevoScaleR oferecem suporte a parâmetros para controlar como o modelo treinado é gerado. Enquanto a precisão e a exatidão do modelo é importante, o desempenho do algoritmo pode ser importante. Para obter o equilíbrio certo entre a precisão e tempo de treinamento, você pode modificar parâmetros para aumentar a velocidade de computação e, em muitos casos, melhorar o desempenho sem reduzir a precisão ou exatidão.

+ [rxDTree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)

    `rxDTree`oferece suporte a `maxDepth` parâmetro, que controla a profundidade da árvore de decisão. Como `maxDepth` é aumentado, o desempenho pode diminuir, portanto, é importante analisar os benefícios de aumentar a profundidade versus está prejudicando o desempenho.

    Você também pode controlar o equilíbrio entre a precisão de previsão e complexidade de tempo, ajustando os parâmetros, como `maxNumBins`, `maxDepth`, `maxComplete`, e `maxSurrogate`. Aumentar a profundidade além de 10 ou 15 pode deixar o cálculo muito caro.

+ [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)

    Tente usar o `cube` argumento se a variável dependente primeiro na fórmula é uma variável de fator.
    
    Quando `cube` é definido como `TRUE`, a regressão é executada usando um inverso particionado, o que pode ser mais rápido e usar menos memória do que a computação de regressão padrão. Se a fórmula tiver um grande número de variáveis, o ganho de desempenho poderá ser significativo.

+ [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)

    Use o `cube` argumento se a variável dependente primeiro é uma variável de fator.
    
    Quando `cube` é definido como `TRUE`, o algoritmo usa um inverso particionado, o que pode ser mais rápido e usar menos memória. Se a fórmula tiver um grande número de variáveis, o ganho de desempenho poderá ser significativo.

Para obter orientação adicional sobre a otimização de RevoScaleR, consulte estes artigos:

+ Artigo de suporte: [opções para rxDForest e rxDTree de ajuste de desempenho](https://support.microsoft.com/kb/3104235)

+ Os métodos para controlar o modelo de ajuste em um modelo de árvore aprimorado: [estimando modelos usando Estocástico Impulsionamento de gradiente](https://docs.microsoft.com/r-server/r/how-to-revoscaler-boosting)

+ Visão geral de como o RevoScaleR move e processa os dados: [escrever algoritmos de agrupamento personalizados em ScaleR](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ Modelo de programação para RevoScaleR: [Gerenciando segmentos no RevoScaleR](https://docs.microsoft.com/r-server/r/how-to-developer-manage-threads)

+ Referência de função [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

+ Referência de função [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)

### <a name="use-microsoftml"></a>Use MicrosoftML

Também é recomendável que você examinar o novo **MicrosoftML** pacote, que fornece os algoritmos de aprendizado de máquina escalonável que podem usar os contextos de computação e transformações fornecidas pelo RevoScaleR.

+ [Introdução ao MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)

+ [Como escolher um algoritmo de MicrosoftML](https://docs.microsoft.com/r-server/r/how-to-choose-microsoftml-algorithms-cheatsheet)

### <a name="operationalize-a-solution-using-microsoft-r-server"></a>Colocar uma solução usando o Microsoft R Server

Se seu cenário envolve fast previsão usando um modelo armazenado, ou integrar o aprendizado de máquina em um aplicativo, você pode usar o [operacionalização](https://docs.microsoft.com/r-server/what-is-operationalization) recursos do Microsoft R Server (anteriormente conhecido como DeployR).

+ Como um **cientista de dados**, use o [mrsdeploy pacote](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package) para compartilhar código R com outros computadores e integrar análise R dentro de aplicativos web, área de trabalho, móveis e painel: [como publicar e gerenciar os serviços da web de R no servidor de R](https://docs.microsoft.com/r-server/operationalize/how-to-deploy-web-service-publish-manage-in-r)

+ Como um **administrador**, saiba como gerenciar pacotes, monitore os nós da web e nós de computação e controlar a segurança em trabalhos de R: [como interagir com e consumir serviços web em R](https://docs.microsoft.com/r-server/operationalize/how-to-consume-web-service-interact-in-r)

## <a name="articles-in-this-series"></a>Esta série de artigos

[Desempenho de ajuste para R – Introdução](sql-server-r-services-performance-tuning.md)

[Ajuste de desempenho para R - configuração do SQL Server](sql-server-configuration-r-services.md)

[Ajuste de desempenho para R - R otimização de código e dados](r-and-data-optimization-r-services.md)

[Ajuste de desempenho - resultados de estudo de caso](performance-case-study-r-services.md)
