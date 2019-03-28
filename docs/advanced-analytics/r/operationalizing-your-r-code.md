---
title: Operacionalizar o código R usando procedimentos armazenados – serviços do SQL Server Machine Learning
description: Inserir o código de idioma R em um procedimento armazenado do SQL Server para torná-lo disponível para qualquer aplicativo cliente que têm acesso a um banco de dados do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/15/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 2d00e96162b492d28f0c0ec107612023c8e15e48
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58512593"
---
# <a name="operationalize-r-code-using-stored-procedures-in-sql-server-machine-learning-services"></a>Operacionalizar o código R usando procedimentos armazenados no SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Ao usar os recursos de R e Python em serviços do SQL Server Machine Learning, a abordagem mais comum para mover as soluções para um ambiente de produção está inserindo o código em procedimentos armazenados. Este artigo resume os principais pontos para o desenvolvedor do SQL a considerar ao operacionalização código R usando o SQL Server.

## <a name="deploy-production-ready-script-using-t-sql-and-stored-procedures"></a>Implantar o script pronta para produção usando o T-SQL e procedimentos armazenados

Integração de soluções de ciência de dados tem significado tradicionalmente recodificar extensivo para dar suporte a desempenho e a integração. Serviços do SQL Server Machine Learning simplifica essa tarefa, pois o código R e Python pode ser executado no SQL Server e chamado usando procedimentos armazenados. Para obter mais informações sobre a mecânica de incorporação de código em procedimentos armazenados, consulte:

+ [Guia de início rápido: Script de R "Hello world" no SQL Server](../../advanced-analytics/tutorials//quickstart-r-run-using-tsql.md)
+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

Um exemplo mais completo de implantar o código R em produção, usando procedimentos armazenados pode ser encontrado em [Tutorial: Análise de dados de R para desenvolvedores do SQL](../../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

## <a name="guidelines-for-optimizing-r-code-for-sql"></a>Diretrizes para otimizar o código R para SQl

Convertendo seu código R no SQL é mais fácil se algumas otimizações são feitas com antecedência no código R ou Python. Eles incluem evitando os tipos de dados que causam problemas, evitando as conversões de dados desnecessários e reescrever o código de R como uma única chamada de função que pode ser facilmente parametrizada. Para obter mais informações, consulte:

+ [Tipos de dados e bibliotecas do R](r-libraries-and-data-types.md)
+ [Convertendo código R para uso no R Services](converting-r-code-for-use-in-sql-server.md)
+ [Usar funções auxiliares de sqlrutils](ref-r-sqlrutils.md)

## <a name="integrate-r-and-python-with-applications"></a>Integrar o R e Python com aplicativos

Como R ou Python pode ser executado de um procedimento armazenado, você pode executar scripts em qualquer aplicativo que possa enviar uma instrução T-SQL e lidar com os resultados. Por exemplo, você pode treinar novamente um modelo em um agendamento usando o [tarefa executar T-SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) no Integration Services, ou usando outro Agendador de trabalho que pode executar um procedimento armazenado.

A pontuação é uma tarefa importante que pode facilmente ser automatizada ou iniciada a partir de aplicativos externos. Treinar o modelo com antecedência, usando o R ou Python ou um procedimento armazenado, e [salvar o modelo em formato binário](../tutorials/walkthrough-build-and-save-the-model.md) a uma tabela. Em seguida, o modelo pode ser carregado em uma variável como parte de uma chamada de procedimento armazenado, usando uma destas opções para a pontuação do T-SQL:

+ [Em tempo real](../real-time-scoring.md) pontuação, otimizado para pequenos lotes
+ Pontuação, para chamar a partir de um aplicativo de linha única
+ [Pontuação nativa](../sql-native-scoring.md), para previsão de lote rápida do SQL Server sem chamar o R

Este passo a passo fornece exemplos de pontuação usando um procedimento armazenado no lote e modos de única linha:

+ [Ponta a ponta passo a passo de ciência de dados para R no SQL Server](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

Vejam esses modelos de solução para obter exemplos de como integrar um aplicativo de pontuação:

+ [Previsão de varejo](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/RetailForecasting/Introduction.md)
+ [Detecção de fraudes](https://github.com/Microsoft/r-server-fraud-detection)
+ [Clustering de cliente](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/getting-started/customer-clustering)

## <a name="boost-performance-and-scale"></a>Aumentar o desempenho e escala

Embora a linguagem R de software livre tenha limitações em relação a grandes conjuntos de dados, o [APIs do pacote RevoScaleR](ref-r-revoscaler.md) incluído com o serviço do SQL Server Machine Learning podem operar em grandes conjuntos de dados e se beneficiar com multithread , cálculos de no banco de dados de vários núcleos e vários processos.

Se sua solução R usa agregações complexas ou envolve grandes conjuntos de dados, você pode aproveitar as agregações de altamente eficientes em memória e índices columnstore do SQL Server e deixar que o código R tratar os cálculos estatísticos e de pontuação.

Para obter mais informações sobre como melhorar o desempenho no SQL Server Machine Learning, consulte:

+ [Ajuste de desempenho para o SQL Server R Services](../../advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [Truques e dicas de otimização do desempenho](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>Adaptar o código de R para outras plataformas ou contextos de computação

O mesmo código R executado nos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados podem ser usados em outras fontes de dados, como o Spark em HDFS, quando você usa o [opção de servidor autônoma](../install/sql-machine-learning-standalone-windows-install.md) na instalação do SQL Server ou quando você instala o produto com marca de não-SQL, Microsoft Machine Learning Server (anteriormente conhecida como **Microsoft R Server**):

+ [Documentação do servidor do Machine Learning](https://docs.microsoft.com/r-server/)

+ [Explorar R para RevoScaleR](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

+ [Algoritmos de agrupamento de gravação](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ [Computação com big data em R](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)

+ [Desenvolver seu próprio algoritmo paralelo](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

