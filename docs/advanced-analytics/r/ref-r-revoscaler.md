---
title: Biblioteca de funções do RevoScaleR R
description: Introdução à biblioteca de funções do RevoScaleR no SQL Server 2016 R Services e SQL Server Serviços de Machine Learning com R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b5dcd2f14d1a1d8e23a62be299b1ff6f41814041
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715063"
---
# <a name="revoscaler-r-library-in-sql-server"></a>RevoScaleR (R library in SQL Server)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**RevoScaleR** é uma biblioteca de funções de ciência de dados de alto desempenho da Microsoft. As funções dão suporte à importação de dados, à transformação de dados, ao resumo, à visualização e à análise.

Em contraste com as funções base do R, as operações RevoScaleR podem ser executadas em conjuntos de dados muito grandes, em paralelo e em sistemas de arquivos distribuídos. O Functions pode operar em conjuntos de valores que não se ajustam à memória usando o agrupamento e remontando os resultados quando as operações são concluídas.

As funções RevoScaleR são indicadas com um prefixo **RX** ou **RX** para facilitar a identificação.

O RevoScaleR serve como uma plataforma para a ciência de dados distribuída. Por exemplo, você pode usar os contextos de computação RevoScaleR e transformações com os algoritmos de última geração no [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package). Você também pode usar [rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec) para executar funções de R base em paralelo.

## <a name="full-reference-documentation"></a>Documentação de referência completa

A biblioteca **RevoScaleR** é distribuída em vários produtos da Microsoft, mas o uso é o mesmo se você obter a biblioteca em SQL Server ou em outro produto. Como as funções são as mesmas, a [documentação para funções individuais RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) é publicada em apenas um local sob a [referência de R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para Microsoft Machine Learning Server. Se existirem comportamentos específicos do produto, as discrepâncias serão indicadas na página de ajuda da função.

## <a name="versions-and-platforms"></a>Versões e plataformas

A biblioteca **RevoScaleR** é baseada em R 3.4.3 e disponível somente quando você instala um dos seguintes produtos ou downloads da Microsoft:

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [Serviços de aprendizado de máquina do SQL Server](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 ou posterior](https://docs.microsoft.com/machine-learning-server/)
+ [Cliente do Microsoft R](set-up-a-data-science-client.md)

> [!NOTE]
> As versões completas de lançamento do produto são somente Windows, a partir do SQL Server 2017. O suporte do Linux para **RevoScaleR** é novo na versão [prévia do SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="functions-by-category"></a>Funções por categoria

Esta seção lista as funções por categoria para dar uma ideia de como cada uma é usada. Você também pode [usar o Sumário](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para localizar funções em ordem alfabética.

## <a name="1-data-source-and-compute"></a>1-fonte de dados e computação

O **RevoScaleR** inclui funções para criar fontes de dados e definir o local, ou o *contexto de computação*, de onde as computações são executadas. Um objeto de fonte de dados é um contêiner que especifica uma cadeia de conexão com o conjunto de dados que você deseja, definido como uma tabela, exibição ou consulta. Não há suporte para chamadas de procedimento armazenado. Funções relevantes para SQL Server cenários são listadas na tabela a seguir.

SQL Server e R usam tipos de dados diferentes em alguns casos. Para obter uma lista de mapeamentos entre os tipos de dados SQL e R, consulte [tipos de dados de r para SQL](r-libraries-and-data-types.md).

| Função| Descrição|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) |  Crie um objeto de contexto de computação SQL Server para enviar computações por push a uma instância remota. Várias funções **RevoScaleR** usam o contexto de computação como um argumento. |
|[rxGetComputeContext/rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) | Obter ou definir o contexto de computação ativo. |
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) | Crie um objeto de dados com base em uma SQL Server consulta ou tabela. |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxodbcdata) | Crie uma fonte de dados com base em uma conexão ODBC. |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxxdfdata) | Crie uma fonte de dados com base em um arquivo XDF local. Os arquivos XDF geralmente são usados para descarregar dados na memória para o disco. Um arquivo XDF pode ser útil ao trabalhar com mais dados do que pode ser transferido do banco de dado em um lote ou mais dados do que podem caber na memória. Por exemplo, se você mover regularmente grandes quantidades de dados de um banco de dados para uma estação de trabalho local, em vez de consultar o banco de dado repetidamente para cada operação de R, poderá usar o arquivo XDF como um tipo de cache para salvar os dados localmente e, em seguida, trabalhar com eles em seu espaço de trabalho do R.|

> [!TIP]
> Se você for novo na ideia de fontes de dados ou contextos de computação, recomendamos que comece com a [computação distribuída](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing) na documentação do Microsoft Machine Learning Server.

### <a name="perform-ddl-statements"></a>Executar instruções DDL

Você pode executar instruções DDL do R, se tiver as permissões necessárias na instância e no banco de dados. As funções a seguir usam chamadas ODBC para executar instruções DDL ou recuperar o esquema de banco de dados.

| Função| Descrição|
| ------- | ---------- |
| [rxSqlServerTableExists e rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) | Descartar uma [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] tabela ou verificar a existência de uma tabela ou objeto de banco de dados. |
| [rxExecuteSQLDDL](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexecutesqlddl) | Execute um comando DDL que define ou manipula objetos de banco de dados. Essa função não pode retornar dados e é usada somente para recuperar ou modificar o esquema de objeto ou os metadados.|

## <a name="2-data-manipulation-etl"></a>2-manipulação de dados (ETL)

Depois de criar um objeto de fonte de dados, você pode usar o objeto para carregar dados nele, transformar dados ou gravar novos dados no destino especificado. Dependendo do tamanho dos dados de origem, você também poderá definir o tamanho do lote como parte da fonte de dados e mover dados em partes.

| Função | Descrição |
|----------|-------------|
| [rxOpen-métodos](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxopen-methods) | Verifique se uma fonte de dados está disponível, abra ou feche uma fonte de dados, leia os dados de uma fonte, grave dados no destino e feche uma fonte de dados.|
| [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) | Mover dados de uma fonte de dados para um armazenamento de arquivos ou para um quadro de dados.|
| [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) | Transforme dados ao movê-los entre fontes de dados.|

<a name="graphing-functions"></a>

## <a name="3-graphing-functions"></a>3-funções de gráfico

| Nome da função | Descrição |
|---------------|-------------|
|[rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram)  |Cria um histograma a partir de dados. | 
|[rxLinePlot](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlineplot) |Cria uma plotagem de linha a partir dos dados. | 
|[rxLorenz](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlorenz)  |Computa uma curva Lorenz que pode ser plotada. | 
|[rxRocCurve](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |Computa e plota curvas ROC de dados reais e previstos. | 

<a name="statistics-functions"></a>

## <a name="4-descriptive-statistics"></a>4-estatísticas descritivas

| Nome da função | Descrição |
|---------------|-------------|
|[rxQuantile](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxquantile) <sup>*</sup> |Computa quantis aproximados para arquivos. Xdf e quadros de dados sem classificação. | 
|[rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) <sup>*</sup> |Estatísticas básicas de Resumo de dados, incluindo cálculos por grupo. Não há suporte para a gravação por cálculos de grupo no arquivo. Xdf. | 
|[rxCrossTabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) <sup>*</sup> |Tabulação cruzada baseada em fórmula de dados. | 
|[rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube)<sup>*</sup> |Tabulação alternativa baseada em fórmulas, projetada para uma representação eficiente que retorna os resultados do cubo. Não há suporte para gravar a saída no arquivo. Xdf. | 
|[rxMarginals](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxmarginals)  |Resumos marginales de tabulações cruzadas. | 
|[as.xtabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/as.xtabs)  |Converte os resultados de tabulação cruzada em um objeto xtabs. | 
|[rxChiSquaredTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Executa o teste qui-quadrado no objeto xtabs. Usado com pequenos conjuntos de dados e não faz a parte dos dados. | 
|[rxFisherTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Executa o teste exato do Fisher no objeto xtabs. Usado com pequenos conjuntos de dados e não faz a parte dos dados. | 
|[rxKendallCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Computa o coeficiente de correlação de classificação Tau do Kendall usando o objeto xtabs. | 
|[rxPairwiseCrossTab](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpairwisecrosstab)  |Aplicar uma função a combinações emparelhadas de linhas e colunas de um objeto xtabs. | 
|[rxRiskRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |Calcule o risco relativo em um objeto xtabs de dois por dois. | 
|[rxOddsRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |Calcule a taxa de probabilidade em um objeto xtabs de dois por dois. | 

<sup>*</sup>Significa as funções mais populares nesta categoria.

<a name="prediction-functions"></a>

## <a name="5-prediction-functions"></a>5-funções de previsão

| Nome da função | Descrição |
|---------------|-------------|
|[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) <sup>*</sup> |Ajusta um modelo linear aos dados. | 
|[rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) <sup>*</sup> |Ajusta um modelo de regressão logística aos dados. | 
|[rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm) <sup>*</sup> |Ajusta um modelo linear generalizado aos dados. | 
|[rxCovCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) <sup>*</sup> |Calcule a covariância, a correlação ou a soma de quadrados/matriz entre produtos para um conjunto de variáveis. | 
|[rxDTree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) <sup>*</sup> |Ajusta uma árvore de classificação ou regressão aos dados. | 
|[rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) <sup>*</sup> |Ajusta uma floresta de decisão de classificação ou regressão aos dados usando um algoritmo de aumento de gradiente estocástico. | 
|[rxDForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) <sup>*</sup> |Ajusta uma floresta de decisão de classificação ou regressão aos dados. | 
|[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxPredict) <sup>*</sup> |Calcula previsões para modelos ajustados. A saída deve ser uma fonte de dados XDF. | 
|[rxKmeans](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxkmeans) <sup>*</sup> |Executa o clustering k-means. | 
|[rxNaiveBayes](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxnaivebayes)<sup>*</sup> |Executa a classificação Naive Bayes. | 
|[rxCov](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) |Calcule a matriz de covariância para um conjunto de variáveis. | 
|[rxCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |Calcule a matriz de correlação para um conjunto de variáveis. | 
|[rxSSCP](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |Calcule a soma dos quadrados/matriz entre produtos para um conjunto de variáveis. | 
|[rxRoc](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |Cálculos de características operacionais do receptor (ROC) usando valores reais e previstos do sistema de classificação binário. | 

<sup>*</sup>Significa as funções mais populares nesta categoria.


## <a name="how-to-work-with-revoscaler"></a>Como trabalhar com o RevoScaleR

As funções no **RevoScaleR** são chamáveis em código R encapsulado em procedimentos armazenados. A maioria dos desenvolvedores cria soluções **RevoScaleR** localmente e, em seguida, migra o código R concluído para procedimentos armazenados como um exercício de implantação.

Ao executar localmente, você normalmente executa um script R da linha de comando ou de um ambiente de desenvolvimento R e especifica um SQL Server contexto de computação usando uma das funções **RevoScaleR** . Você pode usar o contexto de computação remota para todo o código ou para funções individuais. Por exemplo, talvez você queira descarregar o treinamento do modelo para o servidor para usar os dados mais recentes e evitar a movimentação de dados.

Quando você estiver pronto para encapsular o script R dentro de um procedimento armazenado, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), é recomendável reescrever o código como uma única função que tenha entradas e saídas claramente definidas. 

## <a name="see-also"></a>Confira também

+ [Tutoriais de R](../tutorials/sql-server-r-tutorials.md)
+ [Aprenda a usar contextos de computação](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [R para desenvolvedores do SQL: Treinar e colocar um modelo em operação](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [Exemplos de produtos da Microsoft no GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [Referência de R (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 
