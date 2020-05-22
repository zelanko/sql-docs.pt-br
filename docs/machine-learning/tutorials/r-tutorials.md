---
title: Tutoriais do R
titleSuffix: SQL machine learning
description: Este artigo descreve os tutoriais do R para aprendizado de máquina do SQL. Saiba como executar scripts e criar modelos de machine learning.
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: cawrites
ms.author: chadam
ms.reviewer: garye, davidph
ms.date: 05/04/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 63c271c4e1d59c9446495607b42b0b5ad13ea246
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83606902"
---
# <a name="r-tutorials-for-sql-machine-learning"></a>Tutoriais do R para aprendizado de máquina do SQL

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Este artigo descreve os tutoriais e guias de início rápido do R para os [Serviços de Machine Learning no SQL Server](../sql-server-machine-learning-services.md) e nos [Clusters de Big Data](../../big-data-cluster/machine-learning-services.md).
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Este artigo descreve os tutoriais e guias de início rápido de R para os [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md).
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Este artigo descreve os tutoriais e guias de início rápido do R para o [SQL Server 2016 R Services](../r/sql-server-r-services.md).
::: moniker-end

<a name="bkmk_sqltutorials"></a>

## <a name="r-tutorials"></a>Tutoriais do R

| Tutorial | Descrição |
|------|-------------|
| [Prever aluguel de esquis com árvore de decisão](r-predictive-model-introduction.md) | Use o R e um modelo de árvore de decisão para prever o número de futuros aluguéis de esqui. Use notebooks no Azure Data Studio para preparar dados e treinar o modelo e o T-SQL para implantação de modelo. |
| [Categorizar clientes usando cluster K-means](r-clustering-model-introduction.md) | Use o R para desenvolver e implantar um modelo de cluster K-means para categorizar os clientes. Use notebooks no Azure Data Studio para preparar dados e treinar o modelo e o T-SQL para implantação de modelo. |
| [Análise do R no banco de dados para cientistas de dados](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) | Para desenvolvedores de R não familiarizados com o SQL Server, este tutorial explica como executar tarefas comuns de ciência de dados no SQL Server. Carregue e visualize dados, treine e salve um modelo para SQL Server e use o modelo para análise preditiva. |
| [Análise do R no banco de dados para desenvolvedores do SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md) | Crie e implante uma solução do R completa, usando apenas as ferramentas do [!INCLUDE[tsql](../../includes/tsql-md.md)]. Concentra-se em mover uma solução para produção. Você aprenderá a encapsular o código R em um procedimento armazenado, salvar um modelo do R em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e fazer chamadas parametrizadas para o modelo do R para previsão. |

## <a name="r-quickstarts"></a>Inícios rápidos do R

Se você não estiver familiarizado com o aprendizado de máquina do SQL, também poderá experimentar os guias de início rápido do R.

| Guia de Início Rápido | Descrição |
|-|-|
| [Executar scripts simples do R](quickstart-r-create-script.md) | Obtenha as noções básicas de como chamar o R no T-SQL usando [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). |
| [Objetos e estruturas de dados usando R](quickstart-r-data-types-and-objects.md) | Mostra como o SQL usa o R para manipular estruturas de dados. |
| [Criar e pontuar um modelo preditivo no R](quickstart-r-data-types-and-objects.md) | Explica como criar, treinar e usar um modelo do R para fazer previsões usando novos dados. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais detalhes técnicos sobre o R no SQL Server, confira [Extensão da linguagem R no SQL Server](../concepts/extension-r.md).
