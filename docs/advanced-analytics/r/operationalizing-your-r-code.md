---
title: Colocar o código R em operação usando procedimentos armazenados
description: Insira o código de linguagem R em um procedimento armazenado SQL Server para disponibilizá-lo a qualquer aplicativo cliente que tenha acesso a um banco de dados SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/15/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: adcac48bc7d90aae5f05a9b671f05e34cc8cf554
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715682"
---
# <a name="operationalize-r-code-using-stored-procedures-in-sql-server-machine-learning-services"></a>Colocar o código R em operação usando procedimentos armazenados no SQL Server Serviços de Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Ao usar os recursos de R e Python no SQL Server Serviços de Machine Learning, a abordagem mais comum para mover soluções para um ambiente de produção é inserindo o código em procedimentos armazenados. Este artigo resume os principais pontos para o desenvolvedor do SQL considerar ao colocar o código R em operação usando SQL Server.

## <a name="deploy-production-ready-script-using-t-sql-and-stored-procedures"></a>Implantar o script pronto para produção usando o T-SQL e procedimentos armazenados

Tradicionalmente, a integração de soluções de ciência de dados significava uma recodificação extensiva para dar suporte ao desempenho e à integração. SQL Server Serviços de Machine Learning simplifica essa tarefa porque o código do R e do Python pode ser executado em SQL Server e chamado usando procedimentos armazenados. Para obter mais informações sobre a mecânica de inserção de código em procedimentos armazenados, consulte:

+ [Início Rápido: Script R "Olá mundo" no SQL Server](../../advanced-analytics/tutorials//quickstart-r-run-using-tsql.md)
+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

Um exemplo mais abrangente de implantação do código R em produção usando procedimentos armazenados pode ser encontrado em [tutorial: Análise de dados do R para desenvolvedores do SQL](../../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

## <a name="guidelines-for-optimizing-r-code-for-sql"></a>Diretrizes para otimizar o código R para SQl

A conversão do código R no SQL será mais fácil se algumas otimizações forem feitas com antecedência no código R ou Python. Isso inclui evitar tipos de dados que causam problemas, evitar conversões de dados desnecessárias e reescrever o código R como uma única chamada de função que pode ser facilmente parametrizada. Para obter mais informações, consulte:

+ [Tipos de dados e bibliotecas do R](r-libraries-and-data-types.md)
+ [Convertendo código R para uso em R Services](converting-r-code-for-use-in-sql-server.md)
+ [Usar funções auxiliares sqlrutils](ref-r-sqlrutils.md)

## <a name="integrate-r-and-python-with-applications"></a>Integre R e Python com aplicativos

Como você pode executar R ou Python de um procedimento armazenado, você pode executar scripts de qualquer aplicativo que possa enviar uma instrução T-SQL e manipular os resultados. Por exemplo, você pode treinar novamente um modelo em um agendamento usando a [tarefa Executar T-SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) no Integration Services ou usando outro Agendador de trabalho que pode executar um procedimento armazenado.

A pontuação é uma tarefa importante que pode ser facilmente automatizada ou iniciada a partir de aplicativos externos. Você treina o modelo com antecedência, usando R ou Python ou um procedimento armazenado e [salva o modelo em formato binário](../tutorials/walkthrough-build-and-save-the-model.md) em uma tabela. Em seguida, o modelo pode ser carregado em uma variável como parte de uma chamada de procedimento armazenado, usando uma destas opções de Pontuação do T-SQL:

+ [Pontuação em tempo real, otimizado para lotes pequenos
+ Pontuação de linha única, para chamar de um aplicativo
+ [Pontuação nativa](../sql-native-scoring.md), para previsão de lote rápida de SQL Server sem chamar R

Este tutorial fornece exemplos de Pontuação usando um procedimento armazenado nos modos de lote e de linha única:

+ [Instruções de ciência de dados de ponta a ponta para R no SQL Server](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

Consulte estes modelos de solução para obter exemplos de como integrar a pontuação em um aplicativo:

+ [Previsão de varejo](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/RetailForecasting/Introduction.md)
+ [Detecção de fraudes](https://github.com/Microsoft/r-server-fraud-detection)
+ [Clustering de clientes](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/getting-started/customer-clustering)

## <a name="boost-performance-and-scale"></a>Aumente o desempenho e a escala

Embora a linguagem R de software livre tenha limitações conhecidas com relação a grandes conjuntos de dados, as [APIs de pacote RevoScaleR](ref-r-revoscaler.md) incluídas com o serviço de Machine Learning SQL Server podem operar em grandes conjuntos e se beneficiarem de vários threads, vários núcleos, cálculos no banco de dados de vários processos.

Se sua solução de R usa agregações complexas ou envolve grandes conjuntos de altos, você pode aproveitar as agregações de memória e índices columnstore altamente eficientes da SQL Server e permitir que o código R manipule os cálculos e a pontuação estatísticos.

Para obter mais informações sobre como melhorar o desempenho no Machine Learning SQL Server, consulte:

+ [Ajuste de desempenho para SQL Server R Services](../../advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [Dicas e truques de otimização de desempenho](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>Adaptar o código R para outras plataformas ou contextos de computação

O mesmo código R que você executa nos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados pode ser usado em relação a outras fontes de dados, como o Spark over HDFS, quando você usa a [opção de servidor autônomo](../install/sql-machine-learning-standalone-windows-install.md) na instalação do SQL Server ou quando instala o produto com marca não SQL, o Microsoft Machine Learning Servidor (anteriormente conhecido como **Microsoft R Server**):

+ [Documentação do Machine Learning Server](https://docs.microsoft.com/r-server/)

+ [Explorar R para RevoScaleR](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

+ [Gravar algoritmos de agrupamento](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ [Computando com Big Data em R](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)

+ [Desenvolver seu próprio algoritmo paralelo](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

