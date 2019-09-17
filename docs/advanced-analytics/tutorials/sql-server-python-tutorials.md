---
title: Tutoriais do Python
description: Este artigo descreve os tutoriais do Python para SQL Server Serviços de Machine Learning. Saiba como executar scripts Python. Crie, treine e implante modelos do Python para SQL Server. Saiba mais sobre os contextos de computação local e remoto. Explore os pacotes python da Microsoft para ciência de dados e aprendizado de máquina.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/04/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: cd458727fad637414d7c71865b2633f3caf80175
ms.sourcegitcommit: 949e55b32eff6610087819a93160a35af0c5f1c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2019
ms.locfileid: "70383553"
---
# <a name="python-tutorials-for-sql-server-machine-learning-services"></a>Tutoriais do Python para SQL Server Serviços de Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo descreve os tutoriais e os guias de início rápido do Python para [SQL Server serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md).

+ Saiba como executar scripts Python.
+ Crie, treine e implante modelos do Python para SQL Server.
+ Saiba mais sobre os contextos de computação local e remoto.
+ Explore os pacotes python da Microsoft para ciência de dados e aprendizado de máquina.

<a name="bkmk_pythontutorials"></a>

## <a name="python-tutorials"></a>Tutoriais do Python

| Tutorial | Descrição |
|-|-|
| [Prever aluguel de esqui com regressão linear](python-ski-rental-linear-regression.md) | Use o Python e a regressão linear para prever o número de locações de esqui. Use blocos de anotações no Azure Data Studio para preparar dados e treinar o modelo e o T-SQL para implantação de modelo. |
| [Categorizando clientes que usam clustering k-means](python-clustering-model.md) | Use o Python para desenvolver e implantar um modelo de clustering K-means para categorizar os clientes. Use blocos de anotações no Azure Data Studio para preparar dados e treinar o modelo e o T-SQL para implantação de modelo. |
| [Criar um modelo usando revoscalepy](use-python-revoscalepy-to-create-model.md) | Demonstra como executar o código de um cliente Python remoto usando SQL Server como contexto de computação. O tutorial cria um modelo usando **rxLinMod** da biblioteca **revoscalepy** . |
| [Análise de dados do Python para desenvolvedores do SQL](sqldev-in-database-python-for-sql-developers.md) | Este passo a passos de ponta a ponta demonstra o processo de criação de uma solução completa do Python usando o T-SQL. |

## <a name="python-quickstarts"></a>Guias de início rápido do Python

Se você for novo no SQL Server Serviços de Machine Learning, também poderá experimentar os guias de início rápido do Python.

| Início rápido | Descrição |
|-|-|
| [Olá, Mundo em Python e SQL Server](quickstart-python-run-using-t-sql.md) | Aprenda as noções básicas de como chamar o Python no T-SQL. |
| [Manipular entradas e saídas usando o Python no SQL Server](quickstart-python-inputs-and-outputs.md) | Saiba como lidar com entradas e saídas para Python no [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). |
| [Estruturas de dados do Python no SQL Server](quickstart-python-data-structures.md) | Mostra como SQL Server usa o pacote Python pandas para lidar com estruturas de dados. |
| [Treine e use seu primeiro modelo](quickstart-python-train-score-in-tsql.md) | Explica como criar, treinar e usar um modelo Python para prever novos dados. |

## <a name="next-steps"></a>Próximas etapas

+ [O que é SQL Server Serviços de Machine Learning (Python e R)?](../what-is-sql-server-machine-learning.md)
+ [Extensão do Python para SQL Server](../concepts/extension-python.md)