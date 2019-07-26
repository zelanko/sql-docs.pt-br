---
title: Tutoriais de SQL Server R e Python
description: Exemplos e tutoriais para scripts R e Python no SQL Server Serviços de Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: d901d11b11019a19d5e26e12956e9ba520e33e8f
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469623"
---
# <a name="sql-server-machine-learning-tutorials-in-r-and-python"></a>SQL Server Machine Learning tutoriais em R e Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo fornece uma lista abrangente de tutoriais e exemplos de código que demonstram os recursos do Machine Learning do [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) ou [SQL Server 2017 serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md). 

+ Os guias de início rápido usam dados internos ou nenhum dado para rápida exploração com menos esforço.
+ Os tutoriais vão mais fundo com mais tarefas, conjuntos de grandes maiores e explicações mais longas.
+ Exemplos e soluções são para desenvolvedores que preferem começar com código, trabalhando de volta para conceitos e lições para preencher lacunas de conhecimento.

Você aprenderá a usar as bibliotecas do R e do Python com dados relacionais residentes no mesmo contexto operacional, como usar SQL Server procedimentos armazenados para executar e implantar código personalizado e como chamar as bibliotecas do Microsoft R e Python para dados de alto desempenho tarefas de ciência e aprendizado de máquina.

Como uma primeira etapa, examine os conceitos fundamentais fazendo o backup da integração de R e Python da Microsoft com o SQL Server.

## <a name="concepts"></a>Conceitos

A análise no banco de dados refere-se ao suporte nativo para R e Python no SQL Server quando você instala SQL Server Serviços de Machine Learning ou SQL Server serviços de R 2016 (R somente) como um complemento no mecanismo de banco de dados. A integração de R e Python inclui distribuições de software livre base, além de bibliotecas específicas da Microsoft para análise de alto desempenho.

De um ponto de extremidade de arquitetura, seu código é executado como um processo externo na caixa para preservar a integridade do mecanismo de banco de dados. No entanto, todo o acesso a dados e a segurança são por meio de SQL Server funções e permissões de banco de dado, o que significa que qualquer aplicativo com acesso ao SQL Server pode acessar seu script R e Python ao implantá-lo como um procedimento armazenado, ou serializar e salvar um modelo treinado em um SQL Banco de dados do servidor.

As principais diferenças entre o suporte a R e Python em SQL Server versus suporte a idioma equivalente em outros produtos e serviços da Microsoft incluem:

+ Capacidade de "empacotar" código em procedimentos armazenados ou como modelos binários.
+ Escreva o código que chama as bibliotecas Microsoft R e Python instaladas localmente com os arquivos de programas SQL Server.
+ Aplique a arquitetura de segurança do banco de dados do SQL Server às suas soluções de R e Python.
+ Aproveite SQL Server infraestrutura e suporte administrativo para suas soluções personalizadas.

## <a name="quickstarts"></a>Guia de início rápido

Comece aqui para saber como executar R ou Python do T-SQL e como colocar em operação o código de R e Python para um ambiente de produção do SQL.

+ [Python Executar o Python usando o T-SQL](run-python-using-t-sql.md)
+ [D Olá, Mundo em R e SQL](rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [D Manipular entradas e saídas](rtsql-working-with-inputs-and-outputs.md)
+ [D Manipular tipos de dados e objetos](rtsql-r-and-sql-data-types-and-data-objects.md)
+ [D Usando funções do R](rtsql-using-r-functions-with-sql-server-data.md)
+ [D Criar um modelo de previsão](rtsql-create-a-predictive-model-r.md)
+ [D Prever e plotar com base no modelo](rtsql-predict-and-plot-from-model.md)

## <a name="tutorials"></a>Tutoriais

Crie em sua primeira experiência com R e Python e T-SQL examinando mais atentamente os pacotes da Microsoft e operações mais especializadas, como a mudança de contextos de computação locais para remotos.

+ [Tutoriais do Python](sql-server-python-tutorials.md)
+ [Tutoriais de R](sql-server-r-tutorials.md)

<a name ="bkmk_samples"></a>

## <a name="samples"></a>Exemplos

Esses exemplos e demonstrações fornecidos pela equipe de desenvolvimento do SQL Server e do R Server realçam maneiras que você pode usar a análise incorporada em aplicativos do mundo real.

| Link | Descrição | 
|------|-------------|
| [Executar o clustering de clientes usando R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | Use o aprendizado não supervisionado para segmentar clientes com base em dados de vendas. Este exemplo usa o algoritmo rxKmeans escalonável do Microsoft R para criar o modelo de clustering. |
| [Executar o clustering de clientes usando Python e SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | Saiba como usar o algoritmo KMeans para executar o clustering de clientes não supervisionado. Este exemplo usa o idioma do Python no banco de dados.| SQL Server 2017 |
| [Criar um modelo de previsão usando R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | Saiba como uma empresa de aluguel de esqui poderia usar o aprendizado de máquina para prever locações futuras, o que ajuda o plano de negócios e a equipe a atender à demanda futura. Este exemplo usa os algoritmos da Microsoft para criar modelos de regressão logística e árvores de decisão. | 
| [Criar um modelo de previsão usando Python e SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | Crie o aplicativo de análise de aluguel de esqui usando Python, para ajudar a planejar futuras demandas. Este exemplo usa a nova biblioteca do Python, **revoscalepy**, para criar um modelo de regressão linear. | 

<a name="bkmk_solutions"></a>

## <a name="solution-templates"></a>Modelos de Solução

A equipe de ciência de dados da Microsoft forneceu modelos de solução personalizáveis que podem ser usados para dar início a soluções para cenários comuns. Cada solução é adaptada a uma tarefa específica ou a um problema do setor. A maioria das soluções foi projetada para ser executada em SQL Server ou em um ambiente de nuvem, como Azure Machine Learning. Outras soluções podem ser executadas no Linux ou em clusters Spark ou Hadoop, usando Microsoft R Server ou Machine Learning Server.

Todo o código é fornecido, juntamente com instruções sobre como treinar e implantar um modelo de Pontuação usando SQL Server procedimentos armazenados.

+ [Detecção de fraudes](https://gallery.cortanaanalytics.com/Tutorial/Online-Fraud-Detection-Template-with-SQL-Server-R-Services-1)
+ [Previsão de variação personalizada](https://gallery.cortanaanalytics.com/Tutorial/Customer-Churn-Prediction-Template-with-SQL-Server-R-Services-1)
+ [Manutenção preditiva](https://gallery.cortanaanalytics.com/Tutorial/Predictive-Maintenance-Template-with-SQL-Server-R-Services-1)
+ [Prever a duração de permanência do hospital](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

