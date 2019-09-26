---
title: Gere previsões e previsões usando modelos de aprendizado de máquina
description: Use rxPredict ou sp_rxPredict para pontuação em tempo real ou preveja o T-SQL para Pontuação nativa para previsões e previsão em R e Python no SQL Server Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/30/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 14ccd4beb2186213cb3d94b10031ac732224f4d9
ms.sourcegitcommit: 2f56848ec422845ee81fb84ed321a716c677aa0e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2019
ms.locfileid: "71271900"
---
# <a name="how-to-generate-forecasts-and-predictions-using-machine-learning-models-in-sql-server"></a>Como gerar previsões e previsão usando modelos de aprendizado de máquina no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Usar um modelo existente para prever ou prever resultados para novas entradas de dados é uma tarefa fundamental no aprendizado de máquina. Este artigo enumera as abordagens para gerar previsões no SQL Server. Entre as abordagens estão as metodologias de processamento interno para previsões de alta velocidade, em que a velocidade é baseada em reduções incrementais de dependências de tempo de execução. Menos dependências significam previsões mais rápidas.

O uso da infraestrutura de processamento interno (Pontuação em tempo real ou nativa) é fornecido com os requisitos da biblioteca. As funções devem ser das bibliotecas da Microsoft. O código de R ou Python que chama funções de software livre ou de terceiros não tem suporte no C++ CLR ou nas extensões.

A tabela a seguir resume as estruturas de Pontuação para previsão e previsões. 

| Metodologia           | Interface         | Requisitos da biblioteca | Velocidades de processamento |
|-----------------------|-------------------|----------------------|----------------------|
| Estrutura de extensibilidade | [rxPredict (R)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) <br/>[rx_predict (Python)](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | nenhuma. Os modelos podem ser baseados em qualquer função de R ou Python | Centenas de milissegundos. <br/>O carregamento de um ambiente de tempo de execução tem um custo fixo, com média de três a 600 milissegundos, antes de os novos dados serem pontuados. |
| [Extensão CLR de pontuação em tempo real](../real-time-scoring.md) | [sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) em um modelo serializado | R: RevoScaleR, MicrosoftML <br/>Python: revoscalepy, microsoftml | Dezenas de milissegundos, em média. |
| [Extensão de C++ Pontuação nativa](../sql-native-scoring.md) | [Prever a função T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) em um modelo serializado | R: RevoScaleR <br/>Python: revoscalepy | Menos de 20 milissegundos, em média. | 

A velocidade de processamento e não a substância da saída é o recurso diferencial. Supondo as mesmas funções e entradas, a saída pontuada não deve variar com base na abordagem usada.

O modelo deve ser criado usando uma função com suporte, em seguida, serializado em um fluxo de bytes brutos salvo no disco ou armazenado em formato binário em um banco de dados. Usando um procedimento armazenado ou T-SQL, você pode carregar e usar um modelo binário sem a sobrecarga de um tempo de execução de linguagem R ou Python, resultando em tempo de conclusão mais rápido ao gerar pontuações de previsão sobre novas entradas.

O significado do CLR e C++ das extensões é a proximidade com o próprio mecanismo de banco de dados. O idioma nativo do mecanismo de banco de C++dados é, o que significa C++ que as extensões são escritas em execução com menos dependências. Por outro lado, as extensões CLR dependem do .NET Core. 

Como você deve esperar, o suporte à plataforma é afetado por esses ambientes de tempo de execução. As extensões do mecanismo de banco de dados nativo são executadas em qualquer lugar o banco de dados relacional tem Windows, Linux e Azure. As extensões CLR com o requisito do .NET Core são atualmente somente para Windows.

## <a name="scoring-overview"></a>Visão geral da Pontuação

A _Pontuação_ é um processo de duas etapas. Primeiro, você especifica um modelo já treinado para carregar de uma tabela. Em segundo lugar, passe novos dados de entrada para a função, para gerar valores deprevisão (ou pontuações). A entrada geralmente é uma consulta T-SQL, retornando tabular ou linhas únicas. Você pode optar por gerar um valor de coluna única representando uma probabilidade ou pode produzir vários valores, como um intervalo de confiança, um erro ou outro complemento útil para a previsão.

Voltando um pouco, o processo geral de preparação do modelo e, em seguida, a geração de pontuações pode ser resumido dessa forma:

1. Crie um modelo usando um algoritmo com suporte. O suporte varia de acordo com a metodologia de Pontuação escolhida.
2. Treine o modelo.
3. Serialize o modelo usando um formato binário especial.
3. Salve o modelo para SQL Server. Normalmente, isso significa armazenar o modelo serializado em uma tabela SQL Server.
4. Chame a função ou o procedimento armazenado, especificando o modelo e as entradas de dados como parâmetros.

Quando a entrada inclui muitas linhas de dados, geralmente é mais rápido inserir os valores de previsão em uma tabela como parte do processo de pontuação. A geração de uma única Pontuação é mais comum em um cenário em que você obtém valores de entrada de um formulário ou solicitação de usuário e retorna a pontuação a um aplicativo cliente. Para melhorar o desempenho ao gerar pontuações sucessivas, SQL Server pode armazenar em cache o modelo para que ele possa ser recarregado na memória.

## <a name="compare-methods"></a>Métodos de comparação

Para preservar a integridade dos processos do mecanismo de banco de dados principal, o suporte para R e Python é habilitado em uma arquitetura dupla que isola o processamento de idioma do processamento de RDBMS. A partir do SQL Server 2016, a Microsoft adicionou uma estrutura de extensibilidade que permite que os scripts de R sejam executados do T-SQL. No SQL Server 2017, a integração com o Python foi adicionada. 

A estrutura de extensibilidade dá suporte a qualquer operação que você possa executar em R ou Python, variando de funções simples para treinar modelos de aprendizado de máquina complexos. No entanto, a arquitetura de processo duplo exige a invocação de um processo de R ou Python externo para cada chamada, independentemente da complexidade da operação. Quando a carga de trabalho envolve o carregamento de um modelo pré-treinado de uma tabela e a pontuação em relação aos dados que já estão em SQL Server, a sobrecarga de chamar os processos externos adiciona latência que pode ser inaceitável em determinadas circunstâncias. Por exemplo, a detecção de fraudes exige uma pontuação rápida para ser relevante.

Para aumentar as velocidades de Pontuação para cenários como detecção de fraudes, SQL Server adicionou bibliotecas de C++ Pontuação internas como e extensões CLR que eliminam a sobrecarga dos processos de inicialização do R e do Python.

A [**Pontuação em tempo real**](../real-time-scoring.md) foi a primeira solução para Pontuação de alto desempenho. Introduzido em versões anteriores do SQL Server 2017 e atualizações posteriores para SQL Server 2016, a pontuação em tempo real se baseia em bibliotecas CLR que se encontram para o processamento de R e Python sobre funções controladas pela Microsoft em RevoScaleR, MicrosoftML (R), revoscalepy e microsoftml (Python). As bibliotecas CLR são invocadas usando o procedimento armazenado **sp_rxPredict** para gerar pontuações de qualquer tipo de modelo com suporte, sem chamar o tempo de execução de R ou Python.

[Pontuação nativa](../sql-native-scoring.md) é um recurso SQL Server 2017, implementado como uma biblioteca C++ nativa, mas somente para modelos RevoScaleR e revoscalepy. É a abordagem mais rápida e segura, mas dá suporte a um conjunto menor de funções em relação a outras metodologias.

## <a name="choose-a-scoring-method"></a>Escolher um método de Pontuação

Os requisitos de plataforma geralmente determinam qual metodologia de Pontuação usar.

| Versão e plataforma do produto | Metodologia |
|------------------------------|-------------|
| SQL Server 2017 no Windows, SQL Server 2017 Linux e banco de dados SQL do Azure | **Pontuação nativa** com previsão de T-SQL |
| SQL Server 2017 (somente Windows), SQL Server 2016 R Services no SP1 ou superior | **Pontuação em tempo real** com o\_procedimento armazenado SP rxPredict |

Recomendamos a pontuação nativa com a função PREDICT. Usar o\_SP rxPredict exige que você habilite a integração do SQLCLR. Considere as implicações de segurança antes de habilitar essa opção.

## <a name="serialization-and-storage"></a>Serialização e armazenamento

Para usar um modelo com uma das opções de Pontuação rápida, salve o modelo usando um formato serializado especial, que foi otimizado para eficiência de tamanho e pontuação.

+ Chame [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) para gravar um modelo com suporte para o formato **RAW** .
+ Chame [rxUnserializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)' para reconstituir o modelo para uso em outro código de R ou para exibir o modelo.

**Usando o SQL**

No código SQL, você pode treinar o modelo usando [sp_execute_external_script](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)e inserir diretamente os modelos treinados em uma tabela, em uma coluna do tipo **varbinary (max)** . Para obter um exemplo simples, consulte [criar um modelo preditive em R](../tutorials/quickstart-r-train-score-model.md)

**Usando o R**

No código do R, chame a função [rxWriteObject](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxwriteobject) do pacote RevoScaleR para gravar o modelo diretamente no banco de dados. A função **rxWriteObject ()** pode recuperar objetos do R de uma fonte de dados ODBC como SQL Server ou gravar objetos em SQL Server. A API é modelada após um repositório de chave-valor simples.
  
Se você usar essa função, certifique-se de serializar o modelo usando [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) primeiro. Em seguida, defina o argumento *Serialize* em **rxWriteObject** como false para evitar a repetição da etapa de serialização.

A serialização de um modelo para um formato binário é útil, mas não é necessária se você estiver classificando previsões usando R e o ambiente de tempo de execução do Python na estrutura de extensibilidade. Você pode salvar um modelo no formato de byte bruto em um arquivo e, em seguida, ler o arquivo no SQL Server. Essa opção pode ser útil se você estiver movendo ou copiando modelos entre ambientes.

## <a name="scoring-in-related-products"></a>Pontuação em produtos relacionados

Se você estiver usando o [servidor autônomo](r-server-standalone.md) ou um [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), terá outras opções além dos procedimentos armazenados e das funções do T-SQL para gerar previsões rapidamente. Tanto o servidor autônomo quanto o Machine Learning Server dão suporte ao conceito de um *serviço Web* para implantação de código. Você pode agrupar um modelo de R ou Python pré-treinado como um serviço Web, chamado em tempo de execução para avaliar novas entradas de dados. Para obter mais informações, consulte estes tópicos:

+ [O que são serviços Web no Machine Learning Server?](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services)
+ [O que é operacionalização?](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)
+ [Implantar um modelo Python como um serviço Web com o azureml-Model-Management-SDK](https://docs.microsoft.com/machine-learning-server/operationalize/python/quickstart-deploy-python-web-service)
+ [Publicar um bloco de código R ou um modelo em tempo real como um novo serviço Web](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)
+ [pacote mrsdeploy para R](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)


## <a name="see-also"></a>Confira também

+ [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)  
+ [rxRealTimeScoring](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxrealtimescoring)
+ [sp-rxPredict](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql)
+ [PREVER T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)