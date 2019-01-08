---
title: Operacionalizar o código R usando procedimentos armazenados – serviços do SQL Server Machine Learning
description: Inserir o código de idioma R em um procedimento armazenado do SQL Server para torná-lo disponível para qualquer aplicativo cliente que têm acesso a um banco de dados do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 3fc96e57fffb3e000a7e1a19887ed27651df9009
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432179"
---
# <a name="operationalize-r-code-machine-learning-services"></a>Operacionalizar o código de R (serviços de Machine Learning)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Os desenvolvedores de banco de dados são responsáveis por integrar várias tecnologias e reunir os resultados para que possam ser compartilhados por toda a empresa. O desenvolvedor de banco de dados funciona com os desenvolvedores de aplicativos, os desenvolvedores SQL e os cientistas de dados para projetar e implantar soluções.

Este artigo resume os principais pontos para o desenvolvedor de banco de dados a serem considerados ao operacionalização código R usando o SQL Server.

## <a name="get-started-with-r-code-in-sql-server"></a>Introdução ao código R no SQL Server

Tradicionalmente, integração de soluções de aprendizado de máquina tem significava recodificar extensivo para dar suporte a desempenho e a integração. No entanto, mover o código R e Python em um ambiente de produção é muito mais fácil no SQL Server Machine Learning Services, porque o código pode ser executado no SQL Server e chamado usando procedimentos armazenados. Você pode continuar a usar ferramentas familiares e não precisa instalar um ambiente de desenvolvimento de R. 

Para obter mais informações sobre a sintaxe básica, consulte:

+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)
+ [Usando o código R no SQL](../../advanced-analytics/tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md).

Para obter um exemplo de como você pode implantar o código R em produção, usando procedimentos armazenados, consulte:

+ [No banco de dados do Analytics para desenvolvedores do SQL](../../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md).

## <a name="optimize-your-r-code"></a>Otimizar seu código R

É claro, convertendo seu código R no SQL é mais fácil se algumas otimizações são feitas com antecedência no código R ou Python. Eles incluem evitando os tipos de dados que causam problemas, evitando as conversões de dados desnecessários e reescrever o código de R como uma única chamada de função que pode ser facilmente parametrizada. Para obter mais informações, consulte:

+ [Tipos de dados e bibliotecas do R](r-libraries-and-data-types.md)

+ [Convertendo código R para uso no R Services](converting-r-code-for-use-in-sql-server.md)

+ [Usar funções auxiliares de sqlrutils](ref-r-sqlrutils.md)

## <a name="integrate-r-and-python-with-applications"></a>Integrar o R e Python com aplicativos

Porque você pode iniciar os serviços de aprendizado de máquina de um procedimento armazenado, você pode executar scripts R ou Python de qualquer aplicativo que possa enviar uma instrução T-SQL e lidar com os resultados.

Por exemplo, você pode treinar novamente um modelo em um agendamento usando a tarefa executar T-SQL no Integration Services, ou usar outro Agendador de trabalho que pode executar um procedimento armazenado.

A pontuação é uma tarefa importante que pode facilmente ser automatizada ou iniciada a partir de aplicativos externos. Treinar o modelo com antecedência, usando o R ou Python ou um procedimento armazenado e salvar o modelo em formato binário em uma tabela. Em seguida, o modelo pode ser carregado em uma variável como parte de uma chamada de procedimento armazenado, usando uma destas opções para a pontuação do T-SQL:

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

Embora a linguagem R de software livre tenha limitações, o pacote RevoScaleR APIs podem operar em grandes conjuntos de dados e se beneficiar de cálculos no banco de dados de vários segmentos, com vários núcleos e vários processos.

Se sua solução R usa agregações complexas ou envolve grandes conjuntos de dados, você pode aproveitar as agregações de altamente eficientes em memória e índices columnstore do SQL Server e deixar que o código R tratar os cálculos estatísticos e de pontuação.

Para obter mais informações sobre como melhorar o desempenho no SQL Server Machine Learning, consulte:

+ [Ajuste de desempenho para o SQL Server R Services](../../advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [Truques e dicas de otimização do desempenho](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>Adaptar o código de R para outras plataformas ou contextos de computação

O mesmo código R executado nos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados podem ser usados em outras fontes de dados, como Hadoop e em outros contextos de computação.

Para obter mais informações sobre as plataformas com suporte pelo Microsoft R, consulte:

+ [Introdução ao Microsoft R](https://docs.microsoft.com/r-server/)

+ [Explore o RevoScaleR](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

Para obter mais informações sobre como você pode otimizar suas soluções do Microsoft R para execução em várias plataformas ou de dados grandes, consulte:

+ [Algoritmos de agrupamento de gravação](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ [Computação com big data em R](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)

+ [Desenvolver seu próprio algoritmo paralelo](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

