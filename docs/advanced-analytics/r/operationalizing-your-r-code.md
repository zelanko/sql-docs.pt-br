---
title: Utilizar o código R no aprendizado de máquina do SQL Server Services | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: f5fa7806ad70c37c7d51c5ae2cc9606191560e58
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="operationalize-r-code-machine-learning-services"></a>Utilizar o código de R (serviços de aprendizado de máquina)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Os desenvolvedores de banco de dados são responsáveis por integrar várias tecnologias e reunir os resultados para que possam ser compartilhados por toda a empresa. O desenvolvedor de banco de dados funciona com os desenvolvedores de aplicativos, os desenvolvedores do SQL e os cientistas de dados para criar e implantar soluções.

Este artigo resume os pontos-chave para o desenvolvedor de banco de dados a serem considerados ao operacionalização do código R usando o SQL Server.

## <a name="get-started-with-r-code-in-sql-server"></a>Introdução ao código de R no SQL Server

Tradicionalmente, integração de soluções de aprendizado de máquina tem significava recodificar abrangente para dar suporte à integração e desempenho. No entanto, mover o código R e Python para um ambiente de produção é muito mais fácil nos serviços de aprendizado de máquina do SQL Server, porque o código pode ser executado no SQL Server e chamado usando procedimentos armazenados. Você pode continuar a usar as ferramentas familiares e não é necessário instalar um ambiente de desenvolvimento de R. 

Para obter mais informações sobre a sintaxe básica, consulte:

+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)
+ [Usando o código R no SQL](../../advanced-analytics/tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md).

Para obter um exemplo de como você pode implantar o código R em produção, usando procedimentos armazenados, consulte:

+ [No banco de dados Analytics para desenvolvedores em SQL](../../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md).

## <a name="optimize-your-r-code"></a>Otimizar seu código R

Obviamente, é mais fácil se algumas otimizações são feitas com antecedência no código de R ou Python convertendo seu código R no SQL. Isso inclui evitando tipos de dados que causam problemas, evitando conversões de dados desnecessários e reescrever o código de R como uma única chamada de função que pode ser facilmente parametrizada. Para obter mais informações, consulte:

+ [Tipos de dados e bibliotecas do R](r-libraries-and-data-types.md)

+ [Converter o código de R para uso em serviços de R](converting-r-code-for-use-in-sql-server.md)

+ [Gerar um R procedimento armazenado usando sqlrutils](generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)

## <a name="integrate-r-and-python-with-applications"></a>Integrar o R e Python com aplicativos

Como você pode iniciar os serviços de aprendizado de máquina de um procedimento armazenado, você pode executar scripts R ou Python de qualquer aplicativo que possa enviar uma instrução T-SQL e lidar com os resultados.

Por exemplo, você pode treinar novamente um modelo em um agendamento usando a tarefa executar T-SQL no Integration Services, ou usar outro Agendador de trabalho que pode executar um procedimento armazenado.

A pontuação é uma tarefa importante que pode facilmente ser automatizada ou iniciada a partir de aplicativos externos. Treinar o modelo com antecedência, usando o R ou Python ou um procedimento armazenado e salve o modelo em formato binário em uma tabela. Em seguida, o modelo pode ser carregado em uma variável como parte de uma chamada de procedimento armazenado, usando uma das seguintes opções para pontuação do T-SQL:

+ [Em tempo real](../real-time-scoring.md) pontuação, otimizado para lotes pequenos
+ Pontuação de chamada de um aplicativo de linha única
+ [Pontuação nativo](../sql-native-scoring.md), para previsão de lote rápido do SQL Server sem chamar o R

Este passo a passo fornece exemplos de pontuação usando um procedimento armazenado no lote e modos de única linha:

+ [Ponta a ponta passo a passo de ciência de dados para R no SQL Server](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

Consulte esses modelos de solução para obter exemplos de como integrar um aplicativo de pontuação:

+ [Previsão de varejo](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/RetailForecasting/Introduction.md)
+ [Detecção de fraudes](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/FraudDetection/Introduction.md)
+ [Clustering de cliente](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/getting-started/customer-clustering)

## <a name="boost-performance-and-scale"></a>Aumentar o desempenho e escala

Embora a linguagem R de software livre tenha limitações, o pacote RevoScaleR APIs podem operar em grandes conjuntos de dados e se beneficiar de cálculos no banco de dados de vários segmentos, com vários núcleos e vários processos.

Se sua solução R usa agregações complexas ou envolve grandes conjuntos de dados, você pode aproveitar as agregações do altamente eficientes na memória e índices columnstore do SQL Server e permitem que o código R tratar os cálculos estatísticos e pontuação.

Para obter mais informações sobre como melhorar o desempenho no aprendizado de máquina do SQL Server, consulte:

+ [Ajuste de desempenho do SQL Server R Services](../../advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [Truques e dicas de otimização do desempenho](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>Adaptar o código de R para outras plataformas ou contextos de computação

O mesmo código R executado nos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados podem ser usados em outras fontes de dados, como o Hadoop e em outros contextos de computação.

Para obter mais informações sobre as plataformas com suporte pelo Microsoft R, consulte:

+ [Introdução ao Microsoft R](https://docs.microsoft.com/r-server/)

+ [Explorar o RevoScaleR](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

Para obter mais informações sobre como você pode otimizar suas soluções do Microsoft R para execução em várias plataformas ou de dados grandes, consulte:

+ [Algoritmos de agrupamento de gravação](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ [Computação intensa dados em R](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)

+ [Desenvolver seu próprio algoritmo em paralelo](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

