---
title: Visão de geral de tutorial do Python de 2017 do SQL Server - aprendizagem de máquina do SQL Server
description: Introdução para os tutoriais do Python para análise de no banco de dados do SQL Server 2017.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: f31da296bf55b7da55a4e5a8398d411bc5a5b0ea
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510313"
---
# <a name="sql-server-2017-python-tutorials"></a>Tutoriais do Python do SQL Server 2017
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve os tutoriais do Python para análise no banco de dados em [serviços de aprendizado de máquina do SQL Server 2017](../install/sql-machine-learning-services-windows-install.md). 

+ Saiba como encapsular e executar o código Python em procedimentos armazenados.
+ Serialize e salvar modelos com base em Python em bancos de dados do SQL Server.
+ Saiba mais sobre os contextos de computação local e remoto e quando usá-los.
+ Explore os módulos de Python de Microsoft para tarefas de aprendizado de máquina e ciência de dados.

<a name="bkmk_pythontutorials"></a>

## <a name="python-quickstarts-and-tutorials"></a>Tutoriais e inícios rápidos do Python

| Link | Descrição |
|------|-------------|
| [Guia de início rápido: Script de Python de "Hello world" no SQL Server](quickstart-python-run-using-t-sql.md) | Conheça os fundamentos de como chamar o Python no T-SQL. |
| [Guia de início rápido: Criar, treinar e usar um modelo de Python com procedimentos armazenados no SQL Server](quickstart-python-train-score-in-tsql.md) | Explica a mecânica de incorporar código Python em um procedimento armazenado, fornecendo entradas e a execução do procedimento armazenado. |
| [Tutorial: Criar um modelo usando revoscalepy](use-python-revoscalepy-to-create-model.md) | Demonstra como executar código em um terminal de Python remoto, usando o contexto de computação do SQL Server. Você deve ser um pouco familiarizado com os ambientes e ferramentas do Python. Código de exemplo é fornecido que cria um modelo usando **rxLinMod**, da nova **revoscalepy** biblioteca. |
| [Tutorial: Aprenda a análise de Python no banco de dados para desenvolvedores do SQL](sqldev-in-database-python-for-sql-developers.md) | Este passo a passo de ponta a ponta demonstra o processo de criação de uma solução completa do Python usando procedimentos armazenados T-SQL. Todo o código Python é incluído.|

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>Exemplos de código

Esses exemplos e demonstrações fornecidas pela equipe de desenvolvimento do SQL Server realçam maneiras que você pode usar a análise inserida em aplicativos do mundo real.

| Link | Descrição |
|------|-------------|
| [Criar um modelo preditivo usando o Python e o SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | Saiba como uma empresa de aluguel de Esqui pode usar o aprendizado de máquina para prever o futuras locações, que ajuda a equipe e plano de negócios para atender às demandas futuras. |
| [Executar o cliente clustering usando o Python e o SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | Saiba como usar o algoritmo Kmeans para executar o clustering sem supervisão de clientes. |

## <a name="see-also"></a>Confira também

+ [Extensão do Python para o SQL Server](../concepts/extension-python.md)
+ [Tutoriais de serviços do SQL Server Machine Learning](machine-learning-services-tutorials.md)
