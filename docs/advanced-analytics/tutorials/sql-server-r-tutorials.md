---
title: Visão de geral de tutorial do R do SQL Server - aprendizagem de máquina do SQL Server
description: Introdução para os tutoriais da linguagem R para análise do SQL Server no banco de dados.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 467c9320880f1b113cecd36101345f6ee99f7b75
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961931"
---
# <a name="sql-server-r-language-tutorials"></a>Tutoriais da linguagem R do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve os tutoriais da linguagem R para análise no banco de dados em [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) ou [serviços de aprendizado de máquina do SQL Server 2017](../install/sql-machine-learning-services-windows-install.md).

+ Saiba como encapsular e executar código R em procedimentos armazenados.
+ Serialize e salvar modelos baseados em r em bancos de dados do SQL Server.
+ Saiba mais sobre os contextos de computação local e remoto e quando usá-los.
+ Explore as bibliotecas do Microsoft R para tarefas de aprendizado de máquina e ciência de dados.

<a name="bkmk_sqltutorials"></a>

## <a name="r-quickstarts-and-tutorials"></a>Tutoriais e guias de início rápido R

| Link | Descrição |
|------|-------------|
| [Início Rápido: Usando o R no T-SQL](rtsql-using-r-code-in-transact-sql-quickstart.md) | Primeiro de vários guias de início rápido, com este ilustrando a sintaxe básica para chamar uma função do R usando um editor de consultas T-SQL como o SQL Server Management Studio. |
| [Tutorial: Aprenda a análise de R no banco de dados para cientistas de dados](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) | Para desenvolvedores de R novos no SQL Server, este tutorial explica como executar tarefas comuns de dados ciência no SQL Server. Carregar e visualizar dados, treinar e salvar um modelo para o SQL Server e usar o modelo de análise preditiva. |
| [Tutorial: Aprenda a análise de R no banco de dados para desenvolvedores do SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md) | Criar e implantar uma solução completa de R, usando apenas [!INCLUDE[tsql](../../includes/tsql-md.md)] ferramentas. Concentra-se sobre como mover uma solução para produção. Você aprenderá a encapsular o código R em um procedimento armazenado, salvar um modelo do R em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e fazer chamadas parametrizadas para o modelo do R para previsão. |
| [Tutorial: Aprofundamento RevoScalepR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) | Saiba como usar as funções nos pacotes RevoScaleR. Mover dados entre R e o SQL Server e o comutador contextos de computação para atender a uma determinada tarefa. Criar modelos e gráficos e movê-los entre seu ambiente de desenvolvimento e o servidor de banco de dados. |

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>Exemplos de código

| Link | Descrição |
|------|-------------|
| [Criar um modelo preditivo usando R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | Saiba como uma empresa de aluguel de Esqui pode usar o aprendizado de máquina para prever o futuras locações, que ajuda a equipe e plano de negócios para atender às demandas futuras. |
| [Executar o cliente clustering usando R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | Use o aprendizado sem supervisão para clientes do segmento com base em dados de vendas. |

## <a name="see-also"></a>Confira também

+ [Extensão do R para o SQL Server](../concepts/extension-r.md)
+ [Tutoriais de serviços do SQL Server Machine Learning](machine-learning-services-tutorials.md)

