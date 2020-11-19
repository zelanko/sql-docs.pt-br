---
title: Tutoriais do R
titleSuffix: SQL machine learning
description: Este artigo descreve os tutoriais do R para aprendizado de máquina do SQL. Saiba como executar scripts e criar modelos de machine learning.
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.reviewer: garye, davidph
ms.date: 05/21/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: aee6dcfce5e07b62d53420328221999bed0f887f
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870254"
---
# <a name="r-tutorials-for-sql-machine-learning"></a>Tutoriais do R para aprendizado de máquina do SQL
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Este artigo descreve os tutoriais e guias de início rápido do R para os [Serviços de Machine Learning no SQL Server](../sql-server-machine-learning-services.md) e nos [Clusters de Big Data](../../big-data-cluster/machine-learning-services.md).
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Este artigo descreve os tutoriais e guias de início rápido de R para os [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md).
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Este artigo descreve os tutoriais e guias de início rápido do R para o [SQL Server 2016 R Services](../r/sql-server-r-services.md).
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
Este artigo descreve os tutoriais e guias de início rápido de Python para os [Serviços de Machine Learning da Instância Gerenciada de SQL do Azure](/azure/azure-sql/managed-instance/machine-learning-services-overview).
::: moniker-end

<a name="bkmk_sqltutorials"></a>

## <a name="r-tutorials"></a>Tutoriais do R

::: moniker range=">=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions"
| Tutorial | Descrição |
|------|-------------|
| [Prever aluguel de esquis com árvore de decisão](r-predictive-model-introduction.md) | Use o R e um modelo de árvore de decisão para prever o número de futuros aluguéis de esqui. Use notebooks no Azure Data Studio para preparar dados e treinar o modelo e o T-SQL para implantação de modelo. |
| [Categorizar clientes usando cluster K-means](r-clustering-model-introduction.md) | Use o R para desenvolver e implantar um modelo de cluster K-means para categorizar os clientes. Use notebooks no Azure Data Studio para preparar dados e treinar o modelo e o T-SQL para implantação de modelo. |
| [Análise do R no banco de dados para cientistas de dados](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) | Para desenvolvedores de R não familiarizados com machine learning do SQL, este tutorial explica como executar tarefas comuns de ciência de dados no SQL. Carregue e visualize dados, treine e salve um modelo em um banco de dados e use o modelo para análise preditiva. |
| [Análise do R no banco de dados para desenvolvedores do SQL](../tutorials/r-taxi-classification-introduction.md) | Crie e implante uma solução do R completa, usando apenas ferramentas do SQL. Concentra-se em mover uma solução para produção. Você aprenderá a encapsular o código do R em um procedimento armazenado, salvar um modelo do R em um banco de dados e fazer chamadas parametrizadas ao modelo do R para previsão. |
::: moniker-end
::: moniker range="=azuresqldb-mi-current"
| Tutorial | Descrição |
|------|-------------|
| [Prever aluguel de esquis com árvore de decisão](r-predictive-model-introduction.md) | Use o R e um modelo de árvore de decisão para prever o número de futuros aluguéis de esqui. Use notebooks no Azure Data Studio para preparar dados e treinar o modelo e o T-SQL para implantação de modelo. |
| [Categorizar clientes usando cluster K-means](r-clustering-model-introduction.md) | Use o R para desenvolver e implantar um modelo de cluster K-means para categorizar os clientes. Use notebooks no Azure Data Studio para preparar dados e treinar o modelo e o T-SQL para implantação de modelo. |
::: moniker-end

## <a name="r-quickstarts"></a>Inícios rápidos do R

Se você não estiver familiarizado com o aprendizado de máquina do SQL, também poderá experimentar os guias de início rápido do R.

| Guia de Início Rápido | Descrição |
|-|-|
| [Executar scripts simples do R](quickstart-r-create-script.md) | Obtenha as noções básicas de como chamar o R no T-SQL usando [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). |
| [Objetos e estruturas de dados usando R](quickstart-r-data-types-and-objects.md) | Mostra como o SQL usa o R para manipular estruturas de dados. |
| [Criar e pontuar um modelo preditivo no R](quickstart-r-data-types-and-objects.md) | Explica como criar, treinar e usar um modelo do R para fazer previsões usando novos dados. |

## <a name="next-steps"></a>Próximas etapas

+ [Extensão do Python no SQL Server](../concepts/extension-r.md)
