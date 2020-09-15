---
title: Tutoriais do Python
titleSuffix: SQL machine learning
description: Este artigo descreve os tutoriais de Python com o aprendizado de máquina do SQL. Saiba como executar scripts e criar modelos de machine learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/21/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: f417a92a00b290f06326433b24b73137a0a424fa
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178543"
---
# <a name="python-tutorials-for-sql-machine-learning"></a>Tutoriais do Python para aprendizado de máquina do SQL
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Este artigo descreve os tutoriais e guias de início rápido do Python para os [Serviços de Machine Learning no SQL Server](../sql-server-machine-learning-services.md) e nos [Clusters de Big Data](../../big-data-cluster/machine-learning-services.md).
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Este artigo descreve os tutoriais e guias de início rápido de Python para os [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md).
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
Este artigo descreve os tutoriais e guias de início rápido de Python para os [Serviços de Machine Learning da Instância Gerenciada de SQL do Azure](/azure/azure-sql/managed-instance/machine-learning-services-overview).
::: moniker-end

<a name="bkmk_pythontutorials"></a>

## <a name="python-tutorials"></a>Tutoriais do Python

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
| Tutorial | Descrição |
|-|-|
| [Prever aluguel de esqui com regressão linear](python-ski-rental-linear-regression.md) | Use Python e regressão linear para prever o número de locações de esqui. Use notebooks no Azure Data Studio para preparar dados e treinar o modelo e o T-SQL para implantação de modelo. |
| [Categorizar clientes usando cluster K-means](python-clustering-model.md) | Use Python para desenvolver e implantar um modelo de cluster K-means para categorizar os clientes. Use notebooks no Azure Data Studio para preparar dados e treinar o modelo e o T-SQL para implantação de modelo. |
| [Criar um modelo usando revoscalepy](use-python-revoscalepy-to-create-model.md) | Demonstra como executar código de um cliente de Python remoto usando o SQL Server como contexto de computação. O tutorial cria um modelo usando **rxLinMod** da biblioteca **revoscalepy**. |
| [Análise de dados do Python para desenvolvedores de SQL](python-taxi-classification-introduction.md) | Este passo a passo de ponta a ponta demonstra o processo de criação de uma solução completa em Python usando T-SQL. |
::: moniker-end
::: moniker range="=azuresqldb-mi-current"
| Tutorial | Descrição |
|-|-|
| [Prever aluguel de esqui com regressão linear](python-ski-rental-linear-regression.md) | Use Python e regressão linear para prever o número de locações de esqui. Use notebooks no Azure Data Studio para preparar dados e treinar o modelo e o T-SQL para implantação de modelo. |
| [Categorizar clientes usando cluster K-means](python-clustering-model.md) | Use Python para desenvolver e implantar um modelo de cluster K-means para categorizar os clientes. Use notebooks no Azure Data Studio para preparar dados e treinar o modelo e o T-SQL para implantação de modelo. |
::: moniker-end

## <a name="python-quickstarts"></a>Guias de início rápido de Python

Se você não estiver familiarizado com o aprendizado de máquina do SQL, também poderá experimentar os guias de início rápido do Python.

| Guia de Início Rápido | Descrição |
|-|-|
| [Executar scripts simples do Python](quickstart-python-create-script.md) | Aprenda as noções básicas de como chamar o Python no T-SQL usando [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). |
| [Objetos e estruturas de dados usando Python](quickstart-python-data-structures.md) | Mostra como o SQL usa o pacote Pandas do Python para lidar com estruturas de dados. |
| [Criar e pontuar um modelo preditivo no Python](quickstart-python-train-score-model.md) | Explica como criar, treinar e usar um modelo de Python para fazer previsões usando novos dados. |

## <a name="next-steps"></a>Próximas etapas

+ [Extensão do Python no SQL Server](../concepts/extension-python.md)
