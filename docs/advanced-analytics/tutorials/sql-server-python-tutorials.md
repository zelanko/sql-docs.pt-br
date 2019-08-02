---
title: Visão geral do tutorial do Python SQL Server 2017
description: Introdução aos tutoriais do Python para SQL Server análise no banco de dados 2017.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 65dd2197d9fb079da116908871d931ad19370cf5
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714776"
---
# <a name="sql-server-2017-python-tutorials"></a>SQL Server tutoriais do Python 2017
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo descreve os tutoriais do Python para análise no banco de dados no [SQL Server serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md). 

+ Saiba como encapsular e executar o código Python em procedimentos armazenados.
+ Serialize e salve modelos baseados em Python para SQL Server bancos de dados.
+ Saiba mais sobre os contextos de computação local e remoto e quando usá-los.
+ Explore os módulos de Python da Microsoft para tarefas de ciência de dados e aprendizado de máquina.

<a name="bkmk_pythontutorials"></a>

## <a name="python-quickstarts-and-tutorials"></a>Guias de início rápido e tutoriais do Python

| Link | Descrição |
|------|-------------|
| [Início Rápido: Script do Python "Olá, mundo" no SQL Server](quickstart-python-run-using-t-sql.md) | Aprenda as noções básicas de como chamar o Python no T-SQL. |
| [Início Rápido: Criar, treinar e usar um modelo Python com procedimentos armazenados no SQL Server](quickstart-python-train-score-in-tsql.md) | Explica a mecânica de inserção de código Python em um procedimento armazenado, fornecendo entradas e execução de procedimento armazenado. |
| [Tutorial: Criar um modelo usando revoscalepy](use-python-revoscalepy-to-create-model.md) | Demonstra como executar o código de um terminal Python remoto, usando SQL Server contexto de computação. Você deve estar um pouco familiarizado com as ferramentas e os ambientes do Python. É fornecido um código de exemplo que cria um modelo usando **rxLinMod**, da nova biblioteca **revoscalepy** . |
| [Tutorial: Aprenda a análise do Python no banco de dados para desenvolvedores do SQL](sqldev-in-database-python-for-sql-developers.md) | Este passo a passos de ponta a ponta demonstra o processo de criação de uma solução completa do Python usando procedimentos armazenados do T-SQL. Todo o código Python está incluído.|

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>Exemplos de código

Esses exemplos e demonstrações fornecidos pela equipe de desenvolvimento de SQL Server realçam maneiras que você pode usar a análise incorporada em aplicativos do mundo real.

| Link | Descrição |
|------|-------------|
| [Criar um modelo de previsão usando Python e SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | Saiba como uma empresa de aluguel de esqui poderia usar o aprendizado de máquina para prever locações futuras, o que ajuda o plano de negócios e a equipe a atender à demanda futura. |
| [Executar o clustering de clientes usando Python e SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | Saiba como usar o algoritmo KMeans para executar o clustering de clientes não supervisionado. |

## <a name="see-also"></a>Confira também

+ [Extensão do Python para SQL Server](../concepts/extension-python.md)
+ [SQL Server Serviços de Machine Learning tutoriais](machine-learning-services-tutorials.md)
