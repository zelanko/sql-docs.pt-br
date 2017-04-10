---
title: "R e otimiza&#231;&#227;o de dados (servi&#231;os de R) | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b6104878-ed19-47a7-ac37-21e4d6e2a1af
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# R e otimiza&#231;&#227;o de dados (servi&#231;os de R)
Este tópico descreve métodos para atualizar seu código R para melhorar o desempenho ou evitar problemas conhecidos.

## Contexto de computação

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] pode usar o __local__ ou __SQL__ computação contexto ao executar a análise. Ao usar o __local__ contexto de computação, análise é executado no computador cliente e os dados devem ser obtidos de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] pela rede. O impacto no desempenho incorrido para a transferência de rede depende do tamanho dos dados transferidos, velocidade da rede e outras transferências de rede que ocorrem ao mesmo tempo.

Se o contexto de computação é __SQL Server__, em seguida, as funções analíticas são executadas dentro de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Os dados são locais para a tarefa de análise, para que nenhuma sobrecarga de rede é introduzida. 

Ao trabalhar com grandes conjuntos de dados, você deve sempre usar o contexto de computação do SQL.

## Fatores

A linguagem R converte cadeias de caracteres de tabelas em fatores. Muitos objetos de fonte de dados levar `colInfo` como um parâmetro para controlar como as colunas são tratadas. Por exemplo, `c(“fruit” = c(type = “factor”, levels=as.character(c(1:3)), newLevels=c(“apple”, “orange”, “banana”)))` irá consumir inteiros de 1, 2 e 3 de uma tabela e tratá-los como fatores com níveis de `apple`, `orange`, e `banana`. 

Cientistas de dados geralmente usam variáveis fator em sua fórmula. No entanto, usar fatores quando a fonte de dados é um inteiro incorrerá em desempenho como inteiros são convertidos em cadeias de caracteres em tempo de execução. No entanto, se a coluna contiver cadeias de caracteres, você pode especificar os níveis antes do tempo usando `colInfo`. Nesse caso, a instrução equivalente seria  `c(“fruit” = c(type = “factor”, levels= c(“apple”, “orange”, “banana”)))`, que trata as cadeias de caracteres como fatores conforme elas são lidas. 

Para evitar conversões de tempo de execução, considere armazenar níveis como inteiros na tabela e consumi-las conforme descrito na primeira fórmula de exemplo. Se não há nenhuma diferença semântica na geração de modelo, essa abordagem pode levar a um desempenho melhor.

## Transformação de dados

Cientistas de dados frequentemente usam funções de transformação escritas em R como parte da análise. As funções de transformação devem ser aplicadas a cada linha recuperada da tabela. Em [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], essa transformação ocorre no modo de lote e envolve a comunicação entre o interpretador R e o mecanismo de análise. Para executar a transformação, movem os dados do SQL para o mecanismo de análise e, em seguida, o processo do interpretador de R e vice-versa. Portanto, usando transformações pode terum adverso efeito significativo no desempenho do algoritmo, dependendo da quantidade de dados envolvidos.

É mais eficiente a ter todas as colunas necessárias da tabela ou exibição antes de executar a análise, pois isso evita as transformações durante o cálculo. Se não é possível adicionar colunas a tabelas existentes, considere a criação de outra tabela ou exibição com as colunas transformadas e usar uma consulta apropriada para recuperar os dados.

## Envio em lote

A fonte de dados SQL (`RxSqlServerData`) tem uma opção para indicar o tamanho do lote usando o parâmetro `rowsPerRead`. Esse parâmetro especifica o número de linhas a serem processadas por vez. Em tempo de execução algoritmos lerá o número de linhas em cada lote especificado. Por padrão, o valor desse parâmetro é definido como 50.000, para garantir que os algoritmos podem executar bem mesmo em máquinas com pouca memória. Se o computador tiver memória suficiente disponível, aumentar esse valor 500.000 ou até mesmo um milhão pode produzir o melhor desempenho, especialmente para grandes tabelas. 

Aumentar esse valor talvez nem sempre produzem resultados melhores e pode exigir algumas experimentação para determinar o valor ideal. Os benefícios desse serão mais evidentes em um grande conjunto de dados com vários processos (`numTasks` definido como um valor maior que `1`).

## Processamento paralelo

Para melhorar o desempenho da execução rx funções analíticas em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] se baseia no processamento em paralelo usando os núcleos disponíveis no [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] máquina. Há duas maneiras de obter paralelização com [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]:

* Ao usar o `sp_execute_external_script` procedimento armazenado para executar um script de R, definir o `@parallel` parâmetro para `1`. Isso é útil para scripts de R que não usam funções RevoScaleR, que geralmente são prefixadas com "r". Se o script usa funções RevoScaleR, processamento paralelo é tratado automaticamente e você não deve definir `@parallel` para `1`.

    Se o script de R pode ser colocado em paralelo e se o [!INCLUDE[tsql_md](../../includes/tsql-md.md)] consulta pode ser colocado em paralelo, em seguida, [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] criará vários processos paralelos (até o __Máx grau de paralelismo MAXDOP__ configuração [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)],) e executar o mesmo script em todos os processos. Cada processo recebe apenas uma parte dos dados, portanto, isso não é útil com scripts que devem ver todos os dados, como quando um modelo de treinamento. No entanto, é útil ao executar tarefas como a previsão em lotes em paralelo. Para obter mais informações sobre o uso de paralelismo com [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), consulte o __dicas avançadas: processamento paralelo__ seção [usando código R no Transact-SQL](../../advanced-analytics/r-services/using-r-code-in-transact-sql-sql-server-r-services.md).

* Ao usar funções de rx com um contexto de computação do SQL Server, defina `numTasks` para o número de processos que você deseja criar. O número real de processos criados é determinado por [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], e pode ser menor do que você solicitou. O número de processos criados nunca pode ser mais de __MAXDOP__.

    Se o script de R pode ser colocado em paralelo e se o [!INCLUDE[tsql_md](../../includes/tsql-md.md)] consulta pode ser colocado em paralelo, em seguida, [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] criará vários processos paralelos ao executar as funções de rx.

O número de processos que serão criados depende de uma variedade de fatores, como o controle de recursos, uso atual de recursos, outras sessões e o plano de execução de consulta para a consulta usada com o script R. 

### Paralelização de consultas

Para garantir que os dados podem ser analisados em paralelo, a consulta usada para recuperar os dados deve ser estruturada de forma que ele pode ser processado para execução paralela. 

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] oferece suporte ao trabalhar com fontes de dados SQL usando `RxSqlServerData` para especificar a origem. A origem pode ser uma tabela ou uma consulta. Por exemplo, os seguintes exemplos de código definem um objeto de fonte de dados R com base em uma consulta SQL:
~~~~
RxSqlServerData(table=”airline”, connectionString = sqlConnString)
~~~~

~~~~
RxSqlServerData(sqlquery=”select [ArrDelay],[CRSDepTime],[DayOfWeek] from airlineWithIndex where rowNum <= 100000”, connectionString = sqlConnString)
~~~~ 

Como os algoritmos de análise efetuar pull de grandes volumes de dados das tabelas, é importante garantir que a consulta fornecida para `RxSqlServerData` é otimizado para execução paralela. Uma consulta que não resulta em um plano de execução paralela pode resultar em um único processo de computação.

[!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] pode ser usado para analisar o plano de execução e melhorar o desempenho da consulta. Por exemplo, um índice ausente em uma tabela pode afetar o tempo necessário para executar uma consulta. Consulte [monitorar e ajustar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md) para obter mais informações.

Outro supervisão que pode afetar o desempenho é quando a consulta recupera mais colunas que são necessárias. Por exemplo, se uma fórmula se baseia apenas 3 colunas e a tabela tem 30 colunas, não use uma consulta como `select *` ou que seleciona mais colunas do que o necessário.

> [!NOTE]
> Se uma tabela for especificada na fonte de dados em vez de uma consulta, [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] internamente determinará as colunas necessárias para buscar da tabela; no entanto, essa abordagem é improvável que resultam em execução em paralelo.

## Parâmetros do Algoritmo

Muitos algoritmos de treinamento rx oferecem suporte a parâmetros para controlar como o modelo de treinamento é gerado. Embora a precisão e a exatidão do modelo é importante, o desempenho do algoritmo pode ser igualmente importante. Você pode modificar parâmetros de treinamento de modelo parametersthe para aumentar a velocidade de computação e, em muitos casos, você poderá melhorar o desempenho sem reduzir a precisão ou exatidão. 

Por exemplo, `rxDTree` oferece suporte a `maxDepth` parâmetro, que controla a profundidade máxima de árvore. Como `maxDepth` é aumentado, o desempenho pode diminuir, portanto, é importante analisar os benefícios de aumentar a profundidade versus o impacto no desempenho. 

Um dos parâmetros que podem ser usados com `rxLinMod` e `rxLogit` é o `cube` argumento. Esse argumento pode ser usado quando a primeira variável dependente da fórmula é uma variável de fator. Se `cube` for definido como `TRUE`, a regressão é feita usando um inverso particionado, podem ser mais rápido e usam menos memória que a computação de regressão padrão. Se a fórmula tem um grande número de variáveis, o ganho de desempenho pode ser significativo.

O [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler) Guia dos usuários tem algumas informações úteis para controlar o modelo adequado para vários algoritmos. Por exemplo, com `rxDTree` você pode controlar o equilíbrio entre a precisão de previsão e de complexidade de tempo ajustando parâmetros, como `maxNumBins`, `maxDepth`, `maxComplete`, e `maxSurrogate`. Aumentar a profundidade para além de 10 ou 15 pode fazer o cálculo muito caro.

Para obter mais informações sobre ajuste de desempenho para `rxDForest` e `rxDTree`, consulte [rxDForest/rxDTree opções de ajuste de desempenho](https://support.microsoft.com/kb/3104235).

## Modelo e previsão

Depois que o treinamento foi concluída e o melhor modelo selecionado, é recomendável armazenar o modelo no banco de dados para que ele estará disponível para previsões. Para processamento de transações on-line que requer previsão, carregar o modelo computado antes do banco de dados para a previsão é muito eficiente. Os scripts de exemplo usam essa abordagem para serializar e armazenar o modelo em uma tabela de banco de dados. Previsão, o modelo é desserializado do banco de dados.

Alguns modelos gerados por algoritmos como lm ou glm podem ser muito grandes, especialmente quando usada em um grande conjunto de dados. Há limitações de tamanho para os dados que podem ser armazenados em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Você deve limpar o modelo antes de armazená-lo no banco de dados.

> [!NOTE] Se a previsão rápida usando um modelo armazenado e integrar a análise de um aplicativo é um cenário importante, é recomendável __DeployR__. Ele pode ser usado para integrar facilmente a análise de R dentro de aplicativos web, desktop, celular e painel. Em particular, é adequado para armazenar um modelo e, em seguida, executar a previsão de única linha usando o modelo armazenado. Para obter mais informações, consulte [sobre DeployR](https://msdn.microsoft.com/microsoft-r/rserver/deployr-about).

## Consulte também
[Governança de recursos](../../advanced-analytics/r-services/resource-governance-for-r-services.md)
[administrador de recursos](../../relational-databases/resource-governor/resource-governor.md)

[CRIAR POOL DE RECURSOS EXTERNOS](../../t-sql/statements/create-external-resource-pool-transact-sql.md)

 [Guia de ajuste de desempenho do SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-performance-tuning.md)
 
 [Configuração do SQL Server para serviços de R](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)
 
 [Estudo de caso de desempenho](../../advanced-analytics/r-services/performance-case-study-r-services.md)
 