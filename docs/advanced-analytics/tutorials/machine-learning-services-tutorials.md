---
title: Tutoriais de serviços de aprendizado de máquina do SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/22/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 08528f3459022bdcb97b97e22d6f6c474c31a715
ms.sourcegitcommit: eddf8cede905d2adb3468d00220a347acd31ae8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/24/2018
ms.locfileid: "49960740"
---
# <a name="tutorials-for-sql-server-machine-learning-services"></a>Tutoriais para serviços do SQL Server Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo fornece uma lista abrangente dos tutoriais, demonstrações e exemplos de aplicativos que usam recursos de aprendizado de máquina no SQL Server 2016 ou SQL Server 2017. Comece aqui para saber como executar R ou Python no T-SQL, como usar contextos de computação local e remoto e como colocar seu código R e Python para um ambiente de produção do SQL em.

+ [Tutoriais do Python](../tutorials/sql-server-python-tutorials.md)

+ [Tutoriais de R](../tutorials/sql-server-r-tutorials.md)

## <a name ="bkmk_samples"></a>Exemplos de R e Python

Esses exemplos e demonstrações fornecidas pela equipe de desenvolvimento do SQL Server e o R Server realçam maneiras que você pode usar a análise inserida em aplicativos do mundo real.

| Link | Description | Aplica-se a |
|------|-------------|------------|
| [Executar o cliente clustering usando R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | Use o aprendizado sem supervisão para clientes do segmento com base em dados de vendas. Este exemplo usa o algoritmo de rxKmeans escalonável do Microsoft R para criar o modelo de clustering. | SQL Server 2016 ou o SQL Server 2017 |
| [Executar o cliente clustering usando o Python e o SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | Saiba como usar o algoritmo Kmeans para executar o clustering sem supervisão de clientes. Este exemplo usa o Python language no banco de dados.| SQL Server 2017 |
| [Criar um modelo preditivo usando R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | Saiba como uma empresa de aluguel de Esqui pode usar o aprendizado de máquina para prever o futuras locações, que ajuda a equipe e plano de negócios para atender às demandas futuras. Este exemplo usa os algoritmos da Microsoft para criar modelos de árvores de decisão e regressão logística. | SQL Server 2016 ou o SQL Server 2017 |
| [Criar um modelo preditivo usando o Python e o SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | Compile o aplicativo de análise de aluguel de Esqui usando o Python, para ajudar a planejar a demanda futura. Este exemplo usa a nova biblioteca de Python **revoscalepy**, para criar um modelo de regressão linear. | SQL Server 2017 |
| [Como usar o Tableau com serviços do SQL Server Machine Learning](https://blogs.msdn.microsoft.com/mlserver/2017/12/14/how-to-use-tableau-with-sql-server-machine-learning-services-with-r-and-python/) | Analisar mídia social e criar gráficos Tableau, usando o SQL Server e R. | SQL Server 2016 ou o SQL Server 2017 |

## <a name="bkmk_solutions"></a>Modelos de solução

A equipe de ciência de dados da Microsoft forneceu os modelos de solução personalizável que podem ser usados para iniciar rapidamente soluções para cenários comuns. Cada solução é adaptada para um problema específico da tarefa ou do setor. A maioria das soluções é projetada para ser executado no SQL Server ou em um ambiente de nuvem como Azure Machine Learning. Outras soluções podem executar no Linux ou em clusters do Hadoop ou Spark, usando o Microsoft R Server ou Machine Learning Server.

Todo o código é fornecido, juntamente com instruções sobre como treinar e implantar um modelo de pontuação usando os procedimentos armazenados do SQL Server.

+ [Detecção de fraudes](https://gallery.cortanaanalytics.com/Tutorial/Online-Fraud-Detection-Template-with-SQL-Server-R-Services-1)
+ [Previsão de variação personalizada](https://gallery.cortanaanalytics.com/Tutorial/Customer-Churn-Prediction-Template-with-SQL-Server-R-Services-1)
+ [Manutenção preditiva](https://gallery.cortanaanalytics.com/Tutorial/Predictive-Maintenance-Template-with-SQL-Server-R-Services-1)
+ [Prever o hospital da permanência](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

Para obter mais informações, consulte [Modelos de aprendizado de máquina com o SQL Server 2016 R Services](https://blogs.technet.microsoft.com/machinelearning/2016/03/23/machine-learning-templates-with-sql-server-2016-r-services/).

## <a name="recommended-reading"></a>Leitura recomendada

+ [Por que o criamos?](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/01/10/sql-server-r-services-why-did-we-build-it/)

    Deseja saber a verdadeira história por trás do R Services? Leia este artigo da equipe de PM que explica a origem e os objetivos do SQL Server R Services e o desenvolvimento.

+ [Tutoriais e dados de exemplo para o Microsoft R](https://docs.microsoft.com/machine-learning-server/r/tutorial-introduction)

    Saiba mais sobre o Microsoft R, e o que o pacote RevoScaleR oferece nesta coleção de tutoriais rápidos. Saiba como escrever código R de uma vez e implante em qualquer lugar, usando fontes de dados de RevoScaleR e contextos de computação remota.

+ [Introdução ao MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package)

  Saiba como usar os novos algoritmos do pacote MicrosoftML para modelagem avançada e transformações de dados escalonável, otimizadas para vários contextos de computação.
