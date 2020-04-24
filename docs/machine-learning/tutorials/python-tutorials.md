---
title: Tutoriais do Python
description: Este artigo descreve os tutoriais de Python para os Serviços de Machine Learning do SQL Server. Saiba como executar scripts e criar modelos de machine learning no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/04/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e3733f12ed93d7c84a86259742b6996333c3900f
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487346"
---
# <a name="python-tutorials-for-sql-server-machine-learning-services"></a>Tutoriais de Python para os Serviços de Machine Learning do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo descreve os tutoriais e guias de início rápido de Python para os [Serviços de Machine Learning do SQL Server](../install/sql-machine-learning-services-windows-install.md).

+ Saiba como executar scripts de Python.
+ Crie, treine e implante modelos de Python para o SQL Server.
+ Saiba mais sobre os contextos de computação local e remoto.
+ Explore os pacotes de Python da Microsoft para ciência de dados e aprendizado de máquina.

<a name="bkmk_pythontutorials"></a>

## <a name="python-tutorials"></a>Tutoriais do Python

| Tutorial | Descrição |
|-|-|
| [Prever aluguel de esqui com regressão linear](python-ski-rental-linear-regression.md) | Use Python e regressão linear para prever o número de locações de esqui. Use notebooks no Azure Data Studio para preparar dados e treinar o modelo e o T-SQL para implantação de modelo. |
| [Categorizar clientes usando cluster K-means](python-clustering-model.md) | Use Python para desenvolver e implantar um modelo de cluster K-means para categorizar os clientes. Use notebooks no Azure Data Studio para preparar dados e treinar o modelo e o T-SQL para implantação de modelo. |
| [Criar um modelo usando revoscalepy](use-python-revoscalepy-to-create-model.md) | Demonstra como executar código de um cliente de Python remoto usando o SQL Server como contexto de computação. O tutorial cria um modelo usando **rxLinMod** da biblioteca **revoscalepy**. |
| [Análise de dados do Python para desenvolvedores de SQL](sqldev-in-database-python-for-sql-developers.md) | Este passo a passo de ponta a ponta demonstra o processo de criação de uma solução completa em Python usando T-SQL. |

## <a name="python-quickstarts"></a>Guias de início rápido de Python

Se você não estiver familiarizado com os Serviços de Machine Learning do SQL Server, também poderá experimentar os guias de início rápido de Python.

| Guia de Início Rápido | Descrição |
|-|-|
| [Olá, Mundo em Python e no SQL Server](quickstart-python-create-script.md) | Aprenda as noções básicas de como chamar o Python no T-SQL usando [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). |
| [Manipular tipos de dados e objetos usando Python no SQL Server](quickstart-python-data-structures.md) | Mostra como o SQL Server usa o pacote Pandas do Python para lidar com estruturas de dados. |
| [Criar e pontuar um modelo preditivo no Python](quickstart-python-train-score-model.md) | Explica como criar, treinar e usar um modelo de Python para fazer previsões usando novos dados. |

## <a name="next-steps"></a>Próximas etapas

+ [O que são os Serviços de Machine Learning do SQL Server (Python e R)?](../sql-server-machine-learning-services.md)
+ [Extensão de Python para o SQL Server](../concepts/extension-python.md)