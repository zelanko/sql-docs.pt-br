---
title: Pacote de R RevoScaleR
description: O RevoScaleR é um pacote de R da Microsoft que dá suporte à computação distribuída, a contextos de computação remota e a algoritmos de ciência de dados de alto desempenho. Ele também dá suporte à importação de dados, à transformação de dados, ao resumo, à visualização e à análise. O pacote está incluído nos Serviços de Machine Learning do SQL Server e no SQL Server 2016 R Services.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/14/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ab427983bdd327775ab817d6b56f496afe733127
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179959"
---
# <a name="revoscaler-r-package-in-sql-server-machine-learning-services"></a>RevoScaleR (pacote de R nos Serviços de Machine Learning do SQL Server)

[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

O **RevoScaleR** é um pacote de R da Microsoft que dá suporte à computação distribuída, a contextos de computação remota e a algoritmos de ciência de dados de alto desempenho. Ele também dá suporte à importação de dados, à transformação de dados, ao resumo, à visualização e à análise. O pacote está incluído nos [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md) e no [SQL Server 2016 R Services](sql-server-r-services.md).

Em contraste com as funções base do R, as operações do RevoScaleR podem ser executadas em conjuntos de dados grandes, em paralelo e em Sistemas de Arquivos Distribuído. As funções podem operar em conjuntos de dados que não cabem na memória usando o agrupamento e remontando os resultados quando as operações são concluídas.

As funções do RevoScaleR são indicadas com um prefixo rx** ou **Rx** para facilitar a identificação.

O RevoScaleR serve como uma plataforma para a ciência de dados distribuída. Por exemplo, você pode usar os contextos de computação e as transformações do RevoScaleR com os algoritmos de última geração no [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package). Você também pode usar o [rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec) para executar funções base do R em paralelo.

## <a name="full-reference-documentation"></a>Documentação de referência completa

O pacote **RevoScaleR** é distribuído em vários produtos da Microsoft, mas o uso é o mesmo com o pacote no SQL Server ou em outro produto. Como as funções são as mesmas, a [documentação para funções individuais do RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) é publicada em apenas uma localização na [referência do R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para o Microsoft Machine Learning Server. Se existirem comportamentos específicos do produto, as discrepâncias serão indicadas na página de ajuda da função.

## <a name="versions-and-platforms"></a>Versões e plataformas

O pacote **RevoScaleR** é baseado no R 3.4.3 e está disponível somente quando você instala um dos seguintes produtos ou downloads da Microsoft:

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [Serviços de Machine Learning do SQL Server](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 ou posterior](https://docs.microsoft.com/machine-learning-server/)
+ [Microsoft R Client](set-up-a-data-science-client.md)

> [!NOTE]
> As versões completas do produto são somente Windows no SQL Server 2017. Há suporte no Windows e no Linux para o **RevoScaleR** no [SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="functions-by-category"></a>Funções por categoria

Esta seção lista as funções por categoria para dar uma ideia de como cada uma é usada. Use também o [sumário](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para localizar as funções em ordem alfabética.

## <a name="1-data-source-and-compute"></a>1 – Fonte de dados e computação

O **RevoScaleR** inclui funções para criar fontes de dados e definir a localização ou o *contexto de computação*, de execução dos cálculos. Um objeto de fonte de dados é um contêiner que especifica uma cadeia de conexão com o conjunto de dados que você deseja, definido como uma tabela, exibição ou consulta. Não há suporte para chamadas de procedimento armazenado. Funções relevantes para cenários do SQL Server são listadas na tabela abaixo.

O SQL Server e o R usam diferentes tipos de dados em alguns casos. Para obter uma lista de mapeamentos entre os tipos de dados SQL e R, confira [Tipos de dados do R para SQL](r-libraries-and-data-types.md).

| Função| Descrição|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) |  Crie um objeto de contexto de computação do SQL Server para efetuar push de cálculos para uma instância remota. Várias funções do **RevoScaleR** usam o contexto de computação como argumento. |
|[rxGetComputeContext / rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) | Obtenha ou defina o contexto de computação ativo. |
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) | Crie um objeto de dados com base em uma consulta ou uma tabela do SQL Server. |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxodbcdata) | Crie uma fonte de dados com base em uma conexão ODBC. |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxxdfdata) | Crie uma fonte de dados com base em um arquivo XDF local. Os arquivos XDF geralmente são usados para descarregar dados na memória no disco. Um arquivo XDF pode ser útil ao trabalhar com mais dados do que é possível transferir do banco de dados em um lote ou mais dados do que cabem na memória. Por exemplo, se você mover regularmente grandes quantidades de dados de um banco de dados para uma estação de trabalho local, em vez de consultar o banco de dados repetidamente para cada operação do R, use o arquivo XDF como um tipo de cache para salvar os dados localmente e, em seguida, trabalhar com eles no workspace do R.|

> [!TIP]
> Se a ideia de fontes de dados ou contextos de computação for uma novidade para você, recomendamos que comece com a [computação distribuída](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing) na documentação do Microsoft Machine Learning Server.

### <a name="perform-ddl-statements"></a>Executar instruções DDL

Você poderá executar instruções DDL no R caso tenha as permissões necessárias na instância e no banco de dados. As funções a seguir usam chamadas ODBC para executar instruções DDL ou recuperar o esquema de banco de dados.

| Função| Descrição|
| ------- | ---------- |
| [rxSqlServerTableExists e rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) | Remova uma tabela do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ou verifique a existência de uma tabela ou um objeto de banco de dados. |
| [rxExecuteSQLDDL](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexecutesqlddl) | Execute um comando DDL (linguagem de definição de dados) que define ou manipula objetos de banco de dados. Essa função não pode retornar dados e é usada somente para recuperar ou modificar o esquema de objeto ou os metadados.|

## <a name="2-data-manipulation-etl"></a>2 – Manipulação de dados (ETL)

Depois de criar um objeto de fonte de dados, use o objeto para carregar dados nele, transformar dados ou gravar novos dados no destino especificado. Dependendo do tamanho dos dados de origem, você também poderá definir o tamanho do lote como parte da fonte de dados e mover dados em partes.

| Função | Descrição |
|----------|-------------|
| [rxOpen-methods](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxopen-methods) | Verifique se uma fonte de dados está disponível, abra ou feche uma fonte de dados, leia os dados de uma fonte, grave dados no destino e feche uma fonte de dados.|
| [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) | Mova os dados de uma fonte de dados para um armazenamento de arquivos ou um quadro de dados.|
| [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) | Transforme os dados ao movê-los entre fontes de dados.|

<a name="graphing-functions"></a>

## <a name="3-graphing-functions"></a>3 – Funções de grafo

| Nome da função | Descrição |
|---------------|-------------|
|[rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram)  |Cria um histograma com base nos dados. | 
|[rxLinePlot](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlineplot) |Cria um gráfico de linha com base nos dados. | 
|[rxLorenz](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlorenz)  |Calcula uma curva Lorenz, que pode ser plotada. | 
|[rxRocCurve](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |Calcula e plota curvas ROC com base nos dados reais e previstos. | 

<a name="statistics-functions"></a>

## <a name="4-descriptive-statistics"></a>4 – Estatísticas descritivas

| Nome da função | Descrição |
|---------------|-------------|
|[rxQuantile](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxquantile) <sup>*</sup> |Calcula quantidades aproximadas para arquivos .xdf e quadros de dados sem classificação. | 
|[rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) <sup>*</sup> |Estatísticas básicas de resumo de dados, incluindo cálculos por grupo. Não há suporte para a gravação por cálculos de grupo no arquivo .xdf. | 
|[rxCrossTabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) <sup>*</sup> |Tabulação cruzada de dados baseada em fórmula. | 
|[rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) <sup>*</sup> |Tabulação cruzada alternativa baseada em fórmula, projetada para uma representação eficiente que retorna os resultados do cubo. Não há suporte para gravação da saída no arquivo .xdf. | 
|[rxMarginals](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxmarginals)  |Resumos marginais de tabulações cruzadas. | 
|[as.xtabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/as.xtabs)  |Converte os resultados da tabulação cruzada em um objeto xtabs. | 
|[rxChiSquaredTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Executa o teste qui quadrado no objeto xtabs. Usado com os conjuntos de dados pequenos e não agrupa os dados. | 
|[rxFisherTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Executa um Teste Exato de Fisher em um objeto xtabs. Usado com os conjuntos de dados pequenos e não agrupa os dados. | 
|[rxKendallCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Calcula o Coeficiente de Correlação da Classificação Tau de Kendall usando um objeto xtabs. | 
|[rxPairwiseCrossTab](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpairwisecrosstab)  |Aplica uma função a combinações de pares de linhas e colunas de um objeto xtabs. | 
|[rxRiskRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |Calcula o risco relativo em um objeto xtabs de dois por dois. | 
|[rxOddsRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |Calcula a proporção de probabilidade em um objeto xtabs de dois por dois. | 

<sup>*</sup> Significa as funções mais populares nessa categoria.

<a name="prediction-functions"></a>

## <a name="5-prediction-functions"></a>5 – Funções de previsão

| Nome da função | Descrição |
|---------------|-------------|
|[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) <sup>*</sup> |Ajusta um modelo linear aos dados. | 
|[rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) <sup>*</sup> |Ajusta um modelo de regressão logística aos dados. | 
|[rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm) <sup>*</sup> |Ajusta um modelo linear generalizado aos dados. | 
|[rxCovCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) <sup>*</sup> |Calcula a covariância, a correlação ou a soma de matriz de quadrados/produto cruzado para um conjunto de variáveis. | 
|[rxDTree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) <sup>*</sup> |Ajusta uma árvore de classificação ou regressão aos dados. | 
|[rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) <sup>*</sup> |Ajusta uma floresta de decisão de classificação ou regressão aos dados usando um algoritmo de gradient boosting alheatório. | 
|[rxDForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) <sup>*</sup> |Ajusta uma floresta de decisão de classificação ou regressão aos dados. | 
|[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxPredict) <sup>*</sup> |Calcula as previsões para os modelos ajustados. A saída precisa ser uma fonte de dados XDF. | 
|[rxKmeans](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxkmeans) <sup>*</sup> |Executa o cluster K-means. | 
|[rxNaiveBayes](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxnaivebayes) <sup>*</sup> |Executa a classificação Naive Bayes. | 
|[rxCov](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) |Calcula a matriz de covariância para um conjunto de variáveis. | 
|[rxCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |Calcula a matriz de correlação para um conjunto de variáveis. | 
|[rxSSCP](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |Calcula a soma de matriz de quadrados/produto cruzado para um conjunto de variáveis. | 
|[rxRoc](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |Cálculos ROC (Característica de Operação do Receptor) usando os valores reais e previstos de um sistema de classificador binário. | 

<sup>*</sup> Significa as funções mais populares nessa categoria.


## <a name="how-to-work-with-revoscaler"></a>Como trabalhar com o RevoScaleR

As funções do **RevoScaleR** podem ser chamadas no código R encapsulado em procedimentos armazenados. A maioria dos desenvolvedores cria soluções do **RevoScaleR** localmente e, em seguida, migra o código R concluído para procedimentos armazenados como um exercício de implantação.

Na execução local, normalmente, você executa um script R na linha de comando ou em um ambiente de desenvolvimento do R e especifica um contexto de computação do SQL Server usando uma das funções do **RevoScaleR**. Use o contexto de computação remota para todo o código ou para funções individuais. Por exemplo, talvez você queira descarregar o treinamento do modelo no servidor para usar os dados mais recentes e evitar a movimentação de dados.

Quando você estiver pronto para encapsular o script R dentro de um procedimento armazenado, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), recomendamos reescrever o código como uma única função que tenha entradas e saídas claramente definidas. 

## <a name="see-also"></a>Confira também

+ [Tutoriais do R](../tutorials/sql-server-r-tutorials.md)
+ [Saiba como usar contextos de computação](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [R para desenvolvedores do SQL: Treinar e colocar um modelo em operação](../tutorials/r-taxi-classification-introduction.md)
+ [Amostras de produtos da Microsoft no GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [Referência do R (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 
