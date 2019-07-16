---
title: Tutoriais do SQL Server R e Python – Machine Learning do SQL Server
description: Exemplos e tutoriais para R e Python de script em serviços do SQL Server Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 8c8e8ad13ddc34148f1718b7843e00545cd758c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962094"
---
# <a name="sql-server-machine-learning-tutorials-in-r-and-python"></a>Tutoriais do SQL Server Machine Learning em R e Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo fornece uma lista abrangente de tutoriais e exemplos de código que demonstra os recursos de aprendizado de máquina [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) ou [SQL Server 2017 serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md). 

+ Guias de início rápido usam dados internos ou nenhum dado para exploração rápida com o mínimo de esforço.
+ Tutoriais aprofunde mais tarefas, conjuntos de dados maiores e mais explicações.
+ Soluções e exemplos são para os desenvolvedores que preferem para iniciar com o código, trabalhando com versões anteriores para conceitos e as lições para preencher as lacunas de Conhecimento.

Você aprenderá a usar bibliotecas de R e Python com dados relacionais residentes no mesmo contexto operacional, como usar procedimentos armazenados do SQL Server para executar e implantar código personalizado e como chamar o Microsoft R e bibliotecas do Python para dados de alto desempenho tarefas de aprendizado de máquina e ciência.

Como uma primeira etapa, examine os conceitos fundamentais da Microsoft de fazer a integração de R e Python com o SQL Server.

## <a name="concepts"></a>Conceitos

Análise no banco de dados refere-se ao suporte nativo para R e Python no SQL Server quando você instala os serviços de Machine Learning do SQL Server ou SQL Server 2016 R Services (R) como um complemento para o mecanismo de banco de dados. Integração de R e Python inclui distribuições base de código-fonte aberto, além de bibliotecas específicas da Microsoft para análise de alto desempenho.

De um ponto de espera de arquitetura, seu código é executado como um processo externo, na caixa para preservar a integridade do mecanismo de banco de dados. No entanto, todos os dados de acesso e segurança é por meio de funções de banco de dados do SQL Server e permissões, o que significa que qualquer aplicativo com acesso ao SQL Server podem acessar seu script R e Python quando você implantá-lo como um procedimento armazenado, ou serializa e salva um modelo treinado em um SQL Banco de dados do servidor.

Principais diferenças entre R e Python dão suporte no SQL Server em comparação com o suporte a idiomas equivalente em outros produtos da Microsoft e serviços incluem:

+ Capacidade de código de "pacote" em procedimentos armazenados ou como modelos binários.
+ Escreva código que chame as bibliotecas Microsoft R e Python instaladas localmente com arquivos de programa do SQL Server.
+ Aplica a arquitetura de segurança de banco de dados do SQL Server às suas soluções de R e Python.
+ Aproveite a infraestrutura do SQL Server e suporte administrativo para suas soluções personalizadas.

## <a name="quickstarts"></a>Guia de início rápido

Comece aqui para saber como executar R ou Python no T-SQL e como colocar seu código R e Python para um ambiente de produção do SQL em.

+ [Python: Execute o Python usando o T-SQL](run-python-using-t-sql.md)
+ [R: Olá, mundo em R e SQL](rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [R: Lidar com entradas e saídas](rtsql-working-with-inputs-and-outputs.md)
+ [R: Lidar com tipos de dados e objetos](rtsql-r-and-sql-data-types-and-data-objects.md)
+ [R: Usando funções de R](rtsql-using-r-functions-with-sql-server-data.md)
+ [R: Criar um modelo de previsão](rtsql-create-a-predictive-model-r.md)
+ [R: Prever e plotar com base no modelo](rtsql-predict-and-plot-from-model.md)

## <a name="tutorials"></a>Tutoriais

Construir sua primeira experiência com R e Python e T-SQL, levando a examinar mais detalhadamente os pacotes da Microsoft e as operações mais especializadas, como a mudança de local para contextos de computação remota.

+ [Tutoriais do Python](sql-server-python-tutorials.md)
+ [Tutoriais de R](sql-server-r-tutorials.md)

<a name ="bkmk_samples"></a>

## <a name="samples"></a>Exemplos

Esses exemplos e demonstrações fornecidas pela equipe de desenvolvimento do SQL Server e o R Server realçam maneiras que você pode usar a análise inserida em aplicativos do mundo real.

| Link | Descrição | 
|------|-------------|
| [Executar o cliente clustering usando R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | Use o aprendizado sem supervisão para clientes do segmento com base em dados de vendas. Este exemplo usa o algoritmo de rxKmeans escalonável do Microsoft R para criar o modelo de clustering. |
| [Executar o cliente clustering usando o Python e o SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | Saiba como usar o algoritmo Kmeans para executar o clustering sem supervisão de clientes. Este exemplo usa o Python language no banco de dados.| SQL Server 2017 |
| [Criar um modelo preditivo usando R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | Saiba como uma empresa de aluguel de Esqui pode usar o aprendizado de máquina para prever o futuras locações, que ajuda a equipe e plano de negócios para atender às demandas futuras. Este exemplo usa os algoritmos da Microsoft para criar modelos de árvores de decisão e regressão logística. | 
| [Criar um modelo preditivo usando o Python e o SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | Compile o aplicativo de análise de aluguel de Esqui usando o Python, para ajudar a planejar a demanda futura. Este exemplo usa a nova biblioteca de Python **revoscalepy**, para criar um modelo de regressão linear. | 

<a name="bkmk_solutions"></a>

## <a name="solution-templates"></a>Modelos de Solução

A equipe de ciência de dados da Microsoft forneceu os modelos de solução personalizável que podem ser usados para iniciar rapidamente soluções para cenários comuns. Cada solução é adaptada para um problema específico da tarefa ou do setor. A maioria das soluções é projetada para ser executado no SQL Server ou em um ambiente de nuvem como Azure Machine Learning. Outras soluções podem executar no Linux ou em clusters do Hadoop ou Spark, usando o Microsoft R Server ou Machine Learning Server.

Todo o código é fornecido, juntamente com instruções sobre como treinar e implantar um modelo de pontuação usando os procedimentos armazenados do SQL Server.

+ [Detecção de fraudes](https://gallery.cortanaanalytics.com/Tutorial/Online-Fraud-Detection-Template-with-SQL-Server-R-Services-1)
+ [Previsão de variação personalizada](https://gallery.cortanaanalytics.com/Tutorial/Customer-Churn-Prediction-Template-with-SQL-Server-R-Services-1)
+ [Manutenção preditiva](https://gallery.cortanaanalytics.com/Tutorial/Predictive-Maintenance-Template-with-SQL-Server-R-Services-1)
+ [Prever o hospital da permanência](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

