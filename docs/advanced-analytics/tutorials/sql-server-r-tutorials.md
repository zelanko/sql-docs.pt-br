---
title: Visão geral do tutorial do SQL Server R
description: Introdução aos tutoriais da linguagem R para SQL Server análise no banco de dados.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: a020478cc59ceb1688f2c93f64c69685ab74972f
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345947"
---
# <a name="sql-server-r-language-tutorials"></a>TUTORIAIS da linguagem SQL Server R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve os tutoriais da linguagem R para análise no banco de dados no [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) ou [SQL Server 2017 serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md).

+ Saiba como encapsular e executar o código R em procedimentos armazenados.
+ Serialize e salve modelos baseados em r para SQL Server bancos de dados.
+ Saiba mais sobre os contextos de computação local e remoto e quando usá-los.
+ Explore as bibliotecas do Microsoft R para tarefas de ciência de dados e aprendizado de máquina.

<a name="bkmk_sqltutorials"></a>

## <a name="r-quickstarts-and-tutorials"></a>Guias de início rápido e tutoriais do R

| Link | Descrição |
|------|-------------|
| [Início Rápido: Usando o R no T-SQL](rtsql-using-r-code-in-transact-sql-quickstart.md) | Primeiro de vários guias de início rápido, com este ilustrando a sintaxe básica para chamar uma função de R usando um editor de consultas T-SQL, como SQL Server Management Studio. |
| [Tutorial: Aprenda a análise de R para cientistas de dados](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) | Para desenvolvedores de R novos para SQL Server, este tutorial explica como percontra tarefas comuns de ciência de dados no SQL Server. Carregar e Visualizar dados, treinar e salvar um modelo para SQL Server e usar o modelo para análise preditiva. |
| [Tutorial: Aprenda a análise de R no banco de dados para desenvolvedores do SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md) | Crie e implante uma solução de R completa, usando [!INCLUDE[tsql](../../includes/tsql-md.md)] apenas as ferramentas. Concentra-se em mover uma solução para produção. Você aprenderá a encapsular o código R em um procedimento armazenado, salvar um modelo do R em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e fazer chamadas parametrizadas para o modelo do R para previsão. |
| [Tutorial: Aprofundamento RevoScalepR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) | Saiba como usar as funções nos pacotes RevoScaleR. Mover dados entre R e SQL Server e alternar contextos de computação para se adequar a uma tarefa específica. Crie modelos e plotagens e mova-os entre o ambiente de desenvolvimento e o servidor de banco de dados. |

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>Exemplos de código

| Link | Descrição |
|------|-------------|
| [Criar um modelo de previsão usando R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | Saiba como uma empresa de aluguel de esqui poderia usar o aprendizado de máquina para prever locações futuras, o que ajuda o plano de negócios e a equipe a atender à demanda futura. |
| [Executar o clustering de clientes usando R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | Use o aprendizado não supervisionado para segmentar clientes com base em dados de vendas. |

## <a name="see-also"></a>Confira também

+ [Extensão de R para SQL Server](../concepts/extension-r.md)
+ [SQL Server Serviços de Machine Learning tutoriais](machine-learning-services-tutorials.md)

