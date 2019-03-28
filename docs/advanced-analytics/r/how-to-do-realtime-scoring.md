---
title: Gerar previsões e previsões usando modelos de aprendizado de máquina - serviços de aprendizado de máquina do SQL Server
description: Use rxPredict ou sp_rxPredict para pontuação em tempo real ou PREVER o T-SQL para nativo de pontuação para previsões e previsões no R e Pythin no aprendizado de máquina do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/30/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 001b90eafd26c90f730e5647f0dc62d756ca9d1b
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510083"
---
# <a name="how-to-generate-forecasts-and-predictions-using-machine-learning-models-in-sql-server"></a>Como gerar previsões e previsões usando modelos de aprendizado de máquina no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Usando um modelo existente para prever ou prever resultados para novas entradas de dados é uma tarefa essencial no aprendizado de máquina. Este artigo enumera as abordagens para a geração das previsões no SQL Server. Entre as abordagens são metodologias de processamento interno para previsões de alta velocidade, onde a velocidade é baseada em uma reduções incremental do, execute as dependências de tempo. Menos dependências significa que previsões mais rápidas.

Usando a infraestrutura de processamento interno (pontuação em tempo real ou nativa) vem com os requisitos da biblioteca. Funções devem variar entre as bibliotecas da Microsoft. Não há suporte para o código R ou Python, chamando funções de terceiros ou de código-fonte aberto nas extensões CLR ou C++.

A tabela a seguir resume as estruturas de pontuação para previsão e previsões. 

| Metodologia           | Interface         | Requisitos da biblioteca | Velocidades de processamento |
|-----------------------|-------------------|----------------------|----------------------|
| Estrutura de extensibilidade | [rxPredict (R)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) <br/>[rx_predict (Python)](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | Nenhum. Modelos podem ser baseados em qualquer função R ou Python | Centenas de milissegundos. <br/>Carregar um ambiente de tempo de execução tem um custo fixo, média de três a seis centenas de milissegundos, antes de todos os novos dados são pontuados. |
| [Extensão CLR de pontuação em tempo real](../real-time-scoring.md) | [sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) em um modelo serializado | R: RevoScaleR, MicrosoftML <br/>Python: revoscalepy, microsoftml | Dezenas de milissegundos em média. |
| [Pontuação nativa de extensão do C++](../sql-native-scoring.md) | [Função T-SQL PREVER](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) em um modelo serializado | R: RevoScaleR <br/>Python: revoscalepy | Menor que 20 milissegundos em média. | 

Velocidade de processamento e não a substância da saída são o recurso diferenciador. Supondo que as mesmas funções e entradas, a saída pontuada deve varia de acordo com a abordagem usada.

O modelo deve ser criado usando uma função com suporte e serializado para um fluxo de bytes brutos salvo em disco ou armazenados em formato binário em um banco de dados. Usando um procedimento armazenado ou T-SQL, você pode carregar e usar um modelo binário sem a sobrecarga de um tempo de execução de linguagem R ou Python, resultando em menor tempo para conclusão ao gerar pontuações de previsão sobre novas entradas.

O significado das extensões CLR e do C++ é proximidade com o mecanismo de banco de dados em si. A linguagem nativa do mecanismo de banco de dados é C++, o que significa que as extensões escritas em C++ para executar com menos dependências. Em contraste, as extensões do CLR dependem do .NET Core. 

Como você pode esperar, suporte de plataforma é afetado por esses ambientes de tempo de execução. Extensões do mecanismo de banco de dados nativo execute em qualquer lugar em que o banco de dados relacional há suporte para: Windows, Linux, Azure. Extensões CLR com o requisito do .NET Core está atualmente Windows apenas.

## <a name="scoring-overview"></a>Visão geral de pontuação

_Pontuação_ é um processo em duas etapas. Primeiro, você pode especificar um carga de uma tabela já treinado. Em segundo lugar, passagem de novos dados de entrada para a função, para gerar valores de previsão (ou _pontuações_). A entrada é geralmente uma consulta T-SQL, retornando as linhas de tabela ou únicas. Você pode optar por um valor de coluna única que representa a probabilidade de saída, ou você pode saída vários valores, como um intervalo de confiança, erro ou outro complemento útil para a previsão.

Dando um passo de volta, o processo geral de preparar o modelo e, em seguida, gerar pontuações pode ser resumida desta forma:

1. Crie um modelo usando um algoritmo com suporte. Suporte varia de acordo com a metodologia de pontuação que você escolher.
2. Treine o modelo.
3. Serialize o modelo usando um formato binário especial.
3. Salve o modelo para o SQL Server. Normalmente, isso significa armazenar o modelo serializado em uma tabela do SQL Server.
4. Chame a função ou procedimento armazenado, especificando as entradas de modelo e dados como parâmetros.

Quando a entrada inclui muitas linhas de dados, é geralmente mais rápido inserir os valores de previsão em uma tabela como parte do processo de classificação. Gerar uma pontuação única é mais comum em um cenário onde obter os valores de entrada de uma solicitação de forma ou de usuário e retornar a pontuação a um aplicativo cliente. Para melhorar o desempenho ao gerar as pontuações de sucessivas, SQL Server pode armazenar em cache o modelo para que ele pode ser recarregado na memória.

## <a name="compare-methods"></a>Métodos de comparar

Para preservar a integridade dos principais processos de mecanismo de banco de dados, suporte para R e Python está habilitado em uma arquitetura dual que isola o processamento de linguagem do processamento do RDBMS. A partir do SQL Server 2016, a Microsoft adicionou uma estrutura de extensibilidade que permite que os scripts de R ser executado a partir do T-SQL. No SQL Server 2017, foi adicionada a integração do Python. 

A estrutura de extensibilidade dá suporte a qualquer operação que você pode executar em R ou Python, variando de funções simples para modelos de aprendizado de máquina complexos de treinamento. No entanto, a arquitetura dual-processo requer invocar um processo externo do R ou Python para cada chamada, independentemente da complexidade da operação. Quando a carga de trabalho envolve carregar um modelo previamente treinado de uma tabela e de pontuação em relação a ele em dados já existentes no SQL Server, a sobrecarga da chamada de processos externos adiciona latência que pode ser aceitável em determinadas circunstâncias. Por exemplo, a detecção de fraudes requer rápida de pontuação para ser relevante.

Para aumentar as velocidades de pontuação para cenários como detecção de fraudes, SQL Server adicionado bibliotecas internas de pontuação como extensões do C++ e CLR que eliminam a sobrecarga de processos de inicialização do R e Python.

[**Pontuação em tempo real** ](../real-time-scoring.md) foi a primeira solução de pontuação de alto desempenho. Introduzidos em versões anteriores do SQL Server 2017 e as atualizações posteriores para o SQL Server 2016, a pontuação em tempo real se baseia em bibliotecas CLR que substituir o R e Python para processamento em funções controladas pela Microsoft em RevoScaleR, MicrosoftML (R), revoscalepy, e microsoftml (Python). Bibliotecas CLR são invocadas usando o **sp_rxPredict** procedimento armazenado para gerar pontuações de qualquer tipo de modelo com suporte, sem chamar o tempo de execução de R ou Python.

[**Pontuação nativa** ](../sql-native-scoring.md) é um recurso do SQL Server 2017, implementado como uma biblioteca C++ nativa, mas apenas para modelos de RevoScaleR e revoscalepy. Ele é a abordagem mais rápida e mais segura, mas dá suporte a um conjunto menor de funções em relação a outras metodologias.

## <a name="choose-a-scoring-method"></a>Escolha um método de classificação

Requisitos de plataforma geralmente determinam qual metodologia de pontuação para usar.

| Plataforma e versão do produto | Metodologia |
|------------------------------|-------------|
| SQL Server 2017 no Windows, o SQL Server 2017 Linux e o banco de dados SQL do Azure | **Pontuação nativa** com PREVER o T-SQL |
| SQL Server 2017 (somente Windows), SQL Server 2016 R Services no SP1 ou superior | **Pontuação em tempo real** com o sp\_procedimento armazenado de rxPredict |

É recomendável que a pontuação nativa com a função PREDICT. Usando o sp\_rxPredict requer que você habilitar a integração do SQLCLR. Considere as implicações de segurança antes de você habilitar essa opção.

## <a name="serialization-and-storage"></a>Serialização e armazenamento

Para usar um modelo com qualquer uma das opções rápidas de pontuação, salve o modelo usando um formato serializado especial, que foi otimizado para o tamanho e a eficiência de pontuação.

+ Chame [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) escrever um modelo com suporte para o **brutos** formato.
+ Chame [rxUnserializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)' para reconstituir o modelo para uso em outro código de R ou para exibir o modelo.

**Usando o SQL**

No código SQL, você pode treinar o modelo usando [sp_execute_external_script](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)e inserir diretamente os modelos treinados em uma tabela, em uma coluna do tipo **varbinary (max)**. Para obter um exemplo simple, consulte [criar um modelo preditive no R](../tutorials/rtsql-create-a-predictive-model-r.md)

**Usando o R**

No código R, chame o [rxWriteObject](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxwriteobject) função do pacote RevoScaleR para gravar o modelo diretamente no banco de dados. O **rxWriteObject()** função pode recuperar objetos de R de uma fonte de dados ODBC como o SQL Server ou gravar objetos do SQL Server. A API é modelada de um repositório de chave-valor simples.
  
Se você usar essa função, certifique-se de serializar o modelo usando [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) primeiro. Em seguida, defina as *serializar* argumento **rxWriteObject** como FALSE, para evitar repetir a etapa de serialização.

Serializando um modelo para um formato binário é útil, mas não é necessário se você estiver Pontuando previsões usando o R e Python execute o ambiente de tempo na estrutura de extensibilidade. Você pode salvar um modelo no formato de byte bruto em um arquivo e, em seguida, ler o arquivo para o SQL Server. Essa opção pode ser útil se você estiver movendo ou copiando modelos entre ambientes.

## <a name="scoring-in-related-products"></a>Pontuação em produtos relacionados

Se você estiver usando o [servidor autônomo](r-server-standalone.md) ou um [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), você tem outras opções além de procedimentos armazenados e funções de T-SQL para gerar previsões rapidamente. O servidor autônomo e o Machine Learning Server suportam o conceito de um *serviço web* para implantação de código. Você pode agrupar um R ou Python modelo previamente treinado como um serviço web, chamado em tempo de execução para avaliar as novas entradas de dados. Para obter mais informações, consulte estes tópicos:

+ [Quais são os serviços web no Machine Learning Server?](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services)
+ [O que é operacionalização?](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)
+ [Implantar um modelo de Python como um serviço web com o azureml-modelo-management-sdk](https://docs.microsoft.com/machine-learning-server/operationalize/python/quickstart-deploy-python-web-service)
+ [Publicar um modelo em tempo real ou um bloco de código do R como um novo serviço web](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)
+ [pacote mrsdeploy para R](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)


## <a name="see-also"></a>Confira também

+ [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)  
+ [rxRealTimeScoring](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxrealtimescoring)
+ [sp-rxPredict](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql)
+ [PREVER O T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)