---
title: Gerar previsões
description: Use rxPredict ou sp_rxPredict para pontuação em tempo real ou PREDICT do T-SQL para pontuação nativa para previsões em R e Python no Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/30/2020
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c07a5b8d3e1b34c0bb33f44a20ab5fff867db922
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2020
ms.locfileid: "81117619"
---
# <a name="how-to-generate-forecasts-and-predictions-using-machine-learning-models-in-sql-server"></a>Como gerar previsões usando modelos de machine learning no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Usar um modelo existente para prever resultados para novas entradas de dados é uma tarefa fundamental em aprendizado de máquina. Este artigo apresenta as abordagens para gerar previsões no SQL Server. Entre as abordagens, estão as metodologias de processamento interno para previsões de alta velocidade, em que a velocidade é baseada em reduções incrementais de dependências de tempo de execução. Menos dependências significam previsões mais rápidas.

O uso da infraestrutura de processamento interno (pontuação em tempo real ou nativa) vem com os requisitos da biblioteca. As funções devem ser das bibliotecas da Microsoft. O código R ou Python que chama funções de software livre ou de terceiros não tem suporte em extensões C++ ou CLR.

A tabela a seguir resume as estruturas de pontuação para previsões. 

| Metodologia           | Interface         | Requisitos da biblioteca | Velocidades de processamento |
|-----------------------|-------------------|----------------------|----------------------|
| Estrutura de extensibilidade | [rxPredict (R)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) <br/>[rx_predict (Python)](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | Nenhum. Os modelos podem ser baseados em qualquer função do R ou do Python | Centenas de milissegundos. <br/>O carregamento de um ambiente de runtime tem um custo fixo, em média, de três a 600 milissegundos, antes de novos dados serem pontuados. |
| [Extensão CLR de pontuação em tempo real](../real-time-scoring.md) | [sp_rxPredict](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) em um modelo serializado | R: RevoScaleR, MicrosoftML <br/>Python: revoscalepy, microsoftml | Dezenas de milissegundos, em média. |
| [Extensão C++ de pontuação nativa](../sql-native-scoring.md) | [Função PREDICT do T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) em um modelo serializado | R: RevoScaleR <br/>Python: revoscalepy | Menos de 20 milissegundos, em média. | 

A velocidade de processamento e não a substância da saída é o recurso diferencial. Supondo as mesmas funções e entradas, a saída pontuada não deve variar com base na abordagem usada.

O modelo deve ser criado usando uma função com suporte e, em seguida, serializado em um fluxo de bytes brutos salvo no disco ou armazenado em formato binário em um banco de dados. Usando um procedimento armazenado ou T-SQL, você pode carregar e usar um modelo binário sem a sobrecarga de um runtime de linguagem R ou Python, resultando em um tempo de conclusão mais rápido ao gerar pontuações de previsão sobre novas entradas.

O significado das extensões CLR e C++ é a proximidade ao próprio mecanismo de banco de dados. A linguagem nativa do mecanismo de banco de dados é C++, o que significa que as extensões escritas em C++ são executadas com menos dependências. Por outro lado, as extensões CLR dependem do .NET Core. 

Como você deve esperar, o suporte à plataforma é afetado por esses ambientes de runtime. As extensões do mecanismo de banco de dados nativo são executadas em qualquer lugar em que haja suporte para banco de dados relacional: Windows, Linux, Azure. As extensões CLR com o requisito do .NET Core atualmente são somente para Windows.

## <a name="scoring-overview"></a>Visão geral da pontuação

A _pontuação_ é um processo de duas etapas. Primeiro, você especifica um modelo já treinado para carregar de uma tabela. Em segundo lugar, passa novos dados de entrada para a função para gerar valores de previsão (ou _pontuações_). A entrada geralmente é uma consulta T-SQL, retornando linhas tabulares ou únicas. Você pode optar por gerar um valor de coluna única representando uma probabilidade ou produzir diversos valores, como um intervalo de confiança, um erro ou outro complemento útil para a previsão.

Voltando um pouco, o processo geral de preparar o modelo então gerar as pontuações pode ser resumido desta forma:

1. Criar um modelo usando um algoritmo com suporte. O suporte varia de acordo com a metodologia de pontuação escolhida.
2. Treinar o modelo.
3. Serialize o modelo usando um formato binário especial.
3. Salvar o modelo no SQL Server. Normalmente, isso significa armazenar o modelo serializado em uma tabela do SQL Server.
4. Chame a função ou o procedimento armazenado especificando o modelo e as entradas de dados como parâmetros.

Quando a entrada inclui muitas linhas de dados, costuma ser mais rápido inserir os valores de previsão em uma tabela como parte do processo de pontuação. Gerar uma única pontuação é mais comum em um cenário em que você obtém valores de entrada de um formulário ou solicitação de usuário e retorna a pontuação a um aplicativo cliente. Para melhorar o desempenho ao gerar pontuações sucessivas, o SQL Server pode armazenar em cache o modelo para que ele possa ser recarregado na memória.

## <a name="compare-methods"></a>Métodos de comparação

Para preservar a integridade dos processos do mecanismo de banco de dados principal, o suporte para R e Python é habilitado em uma arquitetura dupla que isola o processamento de idioma do processamento de RDBMS. Do SQL Server 2016 em diante, a Microsoft adicionou uma estrutura de extensibilidade que permite que os scripts de R sejam executados do T-SQL. No SQL Server 2017, a integração com o Python foi adicionada. 

A estrutura de extensibilidade dá suporte a qualquer operação que você possa executar em R ou Python, variando de funções simples ao treinamento de modelos de machine learning complexos. No entanto, a arquitetura de processo duplo exige a invocação de um processo externo do R ou do Python para cada chamada, independentemente da complexidade da operação. Quando a carga de trabalho envolve o carregamento de um modelo pré-treinado de uma tabela e a pontuação em relação a ele em dados já no SQL Server, a sobrecarga de chamar os processos externos adiciona latência que pode ser inaceitável em determinadas circunstâncias. Por exemplo, a detecção de fraudes exige uma pontuação rápida para ser relevante.

Para aumentar as velocidades de pontuação para cenários como detecção de fraudes, o SQL Server adicionou bibliotecas de pontuação internas como extensões C++ e CLR que eliminam a sobrecarga dos processos de inicialização do R e do Python.

A [**pontuação em tempo real**](../real-time-scoring.md) foi a primeira solução para pontuação de alto desempenho. Introduzida em versões anteriores do SQL Server 2017 e atualizações posteriores para o SQL Server 2016, a pontuação em tempo real conta com bibliotecas CLR que realizam o processamento de R e Python sobre funções controladas pela Microsoft em RevoScaleR, MicrosoftML(R), revoscalepy e microsoftml (Python). As bibliotecas CLR são chamadas usando o procedimento armazenado **sp_rxPredict** para gerar pontuações de qualquer tipo de modelo com suporte sem chamar o runtime do R ou do Python.

A [**pontuação nativa**](../sql-native-scoring.md) é um recurso do SQL Server 2017, implementado como uma biblioteca nativa em C++, mas somente para modelos RevoScaleR e revoscalepy. É a abordagem mais rápida e segura, mas dá suporte a um conjunto menor de funções em relação a outras metodologias.

## <a name="choose-a-scoring-method"></a>Escolher um método de pontuação

Os requisitos de plataforma geralmente determinam qual metodologia de pontuação usar.

| Versão do produto e plataforma | Metodologia |
|------------------------------|-------------|
| SQL Server 2017 no Windows, SQL Server 2017 no Linux e Banco de Dados SQL do Azure | **Pontuação nativa** com PREDICT do T-SQL |
| SQL Server 2017 (somente Windows), SQL Server 2016 R Services em SP1 ou superior | **Pontuação em tempo real** com o procedimento armazenado sp\_rxPredict |

Recomendamos a pontuação nativa com a função PREDICT. Usar o sp\_rxPredict exige que você habilite a integração do SQLCLR. Considere as implicações de segurança antes de habilitar essa opção.

## <a name="serialization-and-storage"></a>Serialização e armazenamento

Para usar um modelo com uma das opções de pontuação rápida, salve o modelo usando um formato serializado especial, que foi otimizado para tamanho e eficiência de pontuação.

+ Chame [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) para gravar um modelo com suporte no formato **bruto**.
+ Chame [rxUnserializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)' para reconstituir o modelo para uso em outro código R ou para exibir o modelo.

**Como usar o SQL**

No código SQL, você pode treinar o modelo usando [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) e inserir diretamente os modelos treinados em uma tabela em uma coluna do tipo **varbinary (max)** . Para obter um exemplo simples, confira [Criar um modelo de previsão em R](../tutorials/quickstart-r-train-score-model.md)

**Como usar R**

No código R, chame a função [rxWriteObject](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxwriteobject) do pacote RevoScaleR para gravar o modelo diretamente no banco de dados. A função **rxWriteObject ()** pode recuperar objetos do R de uma fonte de dados ODBC, como SQL Server, ou gravar objetos no SQL Server. A API é modelada após um repositório de chave-valor simples.
  
Se você usar essa função, serialize o modelo usando [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) primeiro. Em seguida, defina o argumento *serialize* em **rxWriteObject** como FALSE para evitar a repetição da etapa de serialização.

Serializar um modelo para um formato binário é útil, mas não é necessário se você está pontuando previsões usando R e o ambiente de tempo de execução do Python na estrutura de extensibilidade. Você pode salvar um modelo no formato de byte bruto em um arquivo e então ler o arquivo no SQL Server. Essa opção poderá ser útil se você estiver movendo ou copiando modelos entre ambientes.

## <a name="scoring-in-related-products"></a>Pontuação em produtos relacionados

Se você estiver usando o [servidor autônomo](r-server-standalone.md) ou um [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), terá outras opções além dos procedimentos armazenados e das funções do T-SQL para gerar previsões rapidamente. Tanto o servidor autônomo quanto o Machine Learning Server dão suporte ao conceito de um *serviço Web* para implantação de código. Você pode empacotar um modelo do R ou do Python pré-treinado como um serviço Web, chamado no runtime para avaliar novas entradas de dados. Para obter mais informações, consulte estes artigos:

+ [O que são serviços Web no Machine Learning Server?](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services)
+ [O que é operacionalização?](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)
+ [Implantar um modelo do Python como um serviço Web com azureml-model-management-sdk](https://docs.microsoft.com/machine-learning-server/operationalize/python/quickstart-deploy-python-web-service)
+ [Publicar um bloco de código R ou um modelo em tempo real como um novo serviço Web](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)
+ [Pacote mrsdeploy para R](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)


## <a name="see-also"></a>Confira também

+ [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)  
+ [rxRealTimeScoring](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxrealtimescoring)
+ [sp-rxPredict](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql)
+ [PREDICT T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)