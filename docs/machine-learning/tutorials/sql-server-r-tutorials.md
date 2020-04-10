---
title: Tutoriais do R
description: Introdução aos tutoriais da linguagem R para análises internas no banco de dados no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 62264f728fec5b68c3034fb3c6260f04617353b5
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2020
ms.locfileid: "81116109"
---
# <a name="sql-server-r-language-tutorials"></a>Tutoriais da linguagem R do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo descreve os tutoriais da linguagem R para análises internas no banco de dados no [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) ou nos [Serviços de Machine Learning do SQL Server](../install/sql-machine-learning-services-windows-install.md).

+ Saiba como encapsular e executar o código R em procedimentos armazenados.
+ Serialize e salve modelos baseados em R para bancos de dados do SQL Server.
+ Saiba mais sobre os contextos de computação remota e local e quando usá-los.
+ Explore as bibliotecas do Microsoft R para tarefas de ciência de dados e de aprendizado de máquina.

<a name="bkmk_sqltutorials"></a>

## <a name="r-quickstarts-and-tutorials"></a>Guias de início rápido e tutoriais do R

| Link | Descrição |
|------|-------------|
| [Início Rápido: Criar e executar scripts simples do R](quickstart-r-create-script.md) | Primeiro de vários guias de início rápido, com este ilustrando a sintaxe básica para chamar uma função do R usando um editor de consultas T-SQL, tal como o SQL Server Management Studio. |
| [Tutorial: Análise de R interna no banco de dados para cientistas de dados](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) | Para desenvolvedores de R não familiarizados com o SQL Server, este tutorial explica como executar tarefas comuns de ciência de dados no SQL Server. Carregue e visualize dados, treine e salve um modelo para SQL Server e use o modelo para análise preditiva. |
| [Tutorial: Análise de R interna no banco de dados para desenvolvedores de SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md) | Crie e implante uma solução do R completa, usando apenas as ferramentas do [!INCLUDE[tsql](../../includes/tsql-md.md)]. Concentra-se em mover uma solução para produção. Você aprenderá a encapsular o código R em um procedimento armazenado, salvar um modelo do R em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e fazer chamadas parametrizadas para o modelo do R para previsão. |
| [Tutorial: Aprofundamento no RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) | Saiba como usar as funções dos pacotes RevoScaleR. Mova dados entre o R e o SQL Server e alterne entre contextos de computação para se adequar a uma tarefa específica. Crie modelos e gráficos e mova-os entre o ambiente de desenvolvimento e o servidor de banco de dados. |

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>Exemplos de código

| Link | Descrição |
|------|-------------|
| [Criar um modelo de previsão usando o R e o SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | Saiba como uma empresa de aluguel de esqui pode usar o aprendizado de máquina para prever futuras locações, o que ajuda a empresa a se planejar e a preparar uma equipe adequada para atender a demandas futuras. |
| [Executar o clustering de clientes usando o R e o SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | Use o aprendizado não supervisionado para segmentar os clientes com base em dados de vendas. |

## <a name="see-also"></a>Confira também

+ [Extensão do R para o SQL Server](../concepts/extension-r.md)