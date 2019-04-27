---
title: Biblioteca de funções de RevoScaleR R - serviços do SQL Server Machine Learning
description: Introdução à biblioteca de funções de RevoScaleR no SQL Server 2016 R Services e os serviços do SQL Server 2017 Machine Learning com R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 3745c6cd8c340ce4ad89cac84c5b6286126e3f89
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62641916"
---
# <a name="revoscaler-r-library-in-sql-server"></a>RevoScaleR (biblioteca de R no SQL Server)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**RevoScaleR** é uma biblioteca de funções de ciência de dados de alto desempenho da Microsoft. Funções dão suporte a importação de dados, transformação de dados, resumo, visualização e análise.

Em contraste com funções de R base, as operações de RevoScaleR podem ser executadas em relação a conjuntos de dados muito grandes, em paralelo e em sistemas de arquivos distribuído. Funções podem operar em conjuntos de dados que não cabem na memória por meio de agrupamento e pelos resultados de remontagem quando as operações forem concluídas.

Funções de RevoScaleR são denotadas com um **rx** ou **Rx** prefixo para torná-los mais fáceis de identificar.

RevoScaleR serve como uma plataforma para a ciência de dados distribuídos. Por exemplo, você pode usar as transformações e contextos de computação de RevoScaleR com os algoritmos de última geração na [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package). Você também pode usar [rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec) para executar funções de base do R em paralelo.

## <a name="full-reference-documentation"></a>Documentação de referência completo

O **RevoScaleR** biblioteca é distribuída em vários produtos da Microsoft, mas o uso é o mesmo se você obter a biblioteca no SQL Server ou outro produto. Porque as funções são os mesmos, [documentação para funções de RevoScaleR individuais](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) for publicado em apenas um local sob a [referência de R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para Microsoft Machine Learning Server. Deve qualquer produto específico comportamentos existirem, serão observadas o discrepâncias na página de ajuda de função.

## <a name="versions-and-platforms"></a>As versões e plataformas

O **RevoScaleR** biblioteca é com base em R 3.4.3 e está disponível apenas quando você instala um dos seguintes produtos da Microsoft ou downloads:

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 ou posterior](https://docs.microsoft.com/machine-learning-server/)
+ [Microsoft R client](set-up-a-data-science-client.md)

> [!NOTE]
> São versões de lançamento de produto completo somente Windows, começando com o SQL Server 2017. Suporte do Linux para **RevoScaleR** há de novo no [visualização do SQL Server de 2019](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="functions-by-category"></a>Funções por categoria

Esta seção lista as funções por categoria para lhe dar uma ideia de como cada um deles é usado. Você também pode usar o [sumário](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para localizar funções em ordem alfabética.

## <a name="1-data-source-and-compute"></a>Computação e a fonte de dados 1

**RevoScaleR** inclui funções para criar fontes de dados e definir o local, ou *contexto de computação*, de onde os cálculos são executados. Um objeto de fonte de dados é um contêiner que especifica uma cadeia de conexão com o conjunto de dados que você deseja, definido como uma tabela, exibição ou consulta. Não há suporte para chamadas de procedimento armazenado. Funções relevantes para cenários do SQL Server são listadas na tabela a seguir.

SQL Server e R usam diferentes tipos de dados em alguns casos. Para obter uma lista de mapeamentos entre tipos de dados SQL e R, consulte [tipos de dados do R para SQL](r-libraries-and-data-types.md).

| Função| Descrição|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) |  Crie um objeto de contexto de computação do SQL Server para enviar cálculos para uma instância remota. Vários **RevoScaleR** funções usam um contexto de computação como um argumento. |
|[rxGetComputeContext / rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) | Obtenha ou defina o contexto de computação ativo. |
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) | Crie um objeto de dados com base em uma consulta do SQL Server ou table. |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxodbcdata) | Crie uma fonte de dados com base em uma conexão ODBC. |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxxdfdata) | Crie uma fonte de dados com base em um arquivo XDF local. Arquivos XDF geralmente são usados para descarregar dados na memória em disco. Um arquivo XDF pode ser útil ao trabalhar com mais dados que podem ser transferidos do banco de dados em um lote ou mais dados do que pode caber na memória. Por exemplo, se você move regularmente grandes quantidades de dados de um banco de dados para uma estação de trabalho local, em vez de consultar o banco de dados repetidamente para cada operação de R, você pode usar o arquivo XDF como um tipo de cache para salvar os dados localmente e, em seguida, trabalhar com eles no seu espaço de trabalho do R.|

> [!TIP]
> Se você estiver familiarizado com a ideia de fontes de dados ou contextos de computação, é recomendável que você comece com [computação distribuída](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing) na documentação do Microsoft Machine Learning Server.

### <a name="perform-ddl-statements"></a>Executar instruções DDL

Você pode executar instruções DDL do R, se você tiver as permissões necessárias na instância e banco de dados. As seguintes funções usarem chamadas ODBC para executar instruções DDL ou recuperar o esquema de banco de dados.

| Função| Descrição|
| ------- | ---------- |
| [rxSqlServerTableExists e rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) | Descartar um [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] de tabela, ou verifique a existência de uma tabela de banco de dados ou objeto. |
| [rxExecuteSQLDDL](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexecutesqlddl) | Execute um comando de linguagem de definição de dados (DDL) que define ou manipula os objetos de banco de dados. Essa função não pode retornar dados e é usada somente para recuperar ou modificar o esquema do objeto ou metadados.|

## <a name="2-data-manipulation-etl"></a>Manipulação de dados 2 (ETL)

Depois de criar um objeto de fonte de dados, você pode usar o objeto para carregar dados nele, transformar os dados ou gravar novos dados para o destino especificado. Dependendo do tamanho dos dados de origem, você também poderá definir o tamanho do lote como parte da fonte de dados e mover dados em partes.

| Função | Descrição |
|----------|-------------|
| [rxOpen-methods](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxopen-methods) | Verifique se uma fonte de dados está disponível, abra ou feche uma fonte de dados, ler dados de uma fonte, gravar dados no destino e fechar uma fonte de dados.|
| [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) | Mova dados de uma fonte de dados no armazenamento de arquivos ou em um quadro de dados.|
| [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) | Transforme os dados ao movê-lo entre fontes de dados.|

<a name="graphing-functions"></a>

## <a name="3-graphing-functions"></a>Representação gráfica 3 funções

| Nome da função | Descrição |
|---------------|-------------|
|[rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram)  |Cria um histograma dos dados. | 
|[rxLinePlot](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlineplot) |Cria um gráfico de linha de dados. | 
|[rxLorenz](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlorenz)  |Calcula uma curva Lorenz que pode ser plotada. | 
|[rxRocCurve](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |Calcula e curvas ROC dos dados reais e previstos. | 

<a name="statistics-functions"></a>

## <a name="4-descriptive-statistics"></a>Estatísticas descritivas de 4

| Nome da função | Descrição |
|---------------|-------------|
|[rxQuantile](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxquantile) <sup>*</sup> |Calcula uma ideia de quantis para arquivos. xdf e quadros de dados sem classificação. | 
|[rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) <sup>*</sup> |Estatísticas de resumo básicas de dados, incluindo cálculos por grupo. Escrita por cálculos de grupo para o arquivo. xdf não tem suportada. | 
|[rxCrossTabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) <sup>*</sup> |Com base em fórmula de referência cruzada de dados. | 
|[rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) <sup>*</sup> |Alternativas com base em fórmula tabulação cruzada criada para representação eficiente, retornando resultados de cubo. Gravar a saída para o arquivo. xdf não tem suportado. | 
|[rxMarginals](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxmarginals)  |Resumos marginais de tabulations cruzada. | 
|[as.xtabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/as.xtabs)  |Converte os resultados de tabulação cruzada em um objeto xtabs. | 
|[rxChiSquaredTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Executa o teste de Chi-squared no objeto xtabs. Usado com pequenos conjuntos de dados e não divida os dados. | 
|[rxFisherTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Executa um teste exato de Fisher em objeto xtabs. Usado com pequenos conjuntos de dados e não divida os dados. | 
|[rxKendallCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Calcula coeficiente de correlação Kendall Tau usando objeto xtabs. | 
|[rxPairwiseCrossTab](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpairwisecrosstab)  |Aplica uma função a combinações de pares de linhas e colunas de um objeto xtabs. | 
|[rxRiskRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |Calcule o risco relativo em um objeto xtabs de dois por dois. | 
|[rxOddsRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |Calcule a proporção de probabilidade em um objeto xtabs de dois por dois. | 

<sup>*</sup> Significa que as funções mais comuns nessa categoria.

<a name="prediction-functions"></a>

## <a name="5-prediction-functions"></a>Funções de previsão de 5

| Nome da função | Descrição |
|---------------|-------------|
|[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) <sup>*</sup> |Se encaixa em um modelo linear aos dados. | 
|[rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) <sup>*</sup> |Ajusta a um modelo de regressão logística para dados. | 
|[rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm) <sup>*</sup> |Ajusta a um modelo linear generalizado para dados. | 
|[rxCovCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) <sup>*</sup> |Calcule a covariância, correlação ou soma dos quadrados / produto cruzado matriz para um conjunto de variáveis. | 
|[rxDTree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) <sup>*</sup> |Se encaixa em uma árvore de classificação ou regressão para dados. | 
|[rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) <sup>*</sup> |Se encaixa em uma floresta de decisão de classificação ou regressão aos dados usando um algoritmo impulsionado de gradiente estocástico. | 
|[rxDForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) <sup>*</sup> |Se encaixa em uma floresta de decisão de classificação ou regressão para dados. | 
|[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxPredict) <sup>*</sup> |Calcula as previsões para modelos ajustados. Saída deve ser uma fonte de dados do XDF. | 
|[rxKmeans](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxkmeans) <sup>*</sup> |Executa o clustering k-means. | 
|[rxNaiveBayes](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxnaivebayes) <sup>*</sup> |Executa a classificação Bayesiana ingênua. | 
|[rxCov](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) |Calcule a matriz de covariância para um conjunto de variáveis. | 
|[rxCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |Calcule a matriz de correlação para um conjunto de variáveis. | 
|[rxSSCP](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |Calcular a soma dos quadrados / produto cruzado matriz para um conjunto de variáveis. | 
|[rxRoc](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |Cálculos de característica de operação (Cco) do receptor usando valores previstos e reais do sistema de classificação binária. | 

<sup>*</sup> Significa que as funções mais comuns nessa categoria.


## <a name="how-to-work-with-revoscaler"></a>Como trabalhar com RevoScaleR

Funções em **RevoScaleR** podem ser chamados no código R encapsulado em procedimentos armazenados. A maioria dos desenvolvedores construir **RevoScaleR** localmente, soluções e, em seguida, migrar código de R concluído para procedimentos armazenados como um exercício de implantação.

Ao executar localmente, você normalmente executar um script R de linha de comando ou de um ambiente de desenvolvimento de R e especificar um contexto de computação do SQL Server usando um dos **RevoScaleR** funções. Você pode usar o contexto de computação remota para todo o código, ou para funções individuais. Por exemplo, você talvez queira descarregamento de treinamento do modelo para o servidor para usar os dados mais recentes e evitar a movimentação de dados.

Quando você estiver pronto para encapsular o script de R dentro de um procedimento armazenado, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), é recomendável reescrever o código como uma única função que claramente definida entradas e saídas. 

## <a name="see-also"></a>Confira também

+ [Tutoriais de R](../tutorials/sql-server-r-tutorials.md)
+ [Saiba como usar contextos de computação](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [R para desenvolvedores do SQL: Treinar e operacionalizar um modelo](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [Exemplos de produtos da Microsoft no GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [Referência de R (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 
