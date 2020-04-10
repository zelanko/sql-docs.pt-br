---
title: 'Python + T-SQL: Desenvolver um modelo'
description: Saiba como inserir o código Python em procedimentos armazenados do SQL Server e em funções do T-SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3bafc3a524ec854dc9bf1669660827d5a6bc80f7
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2020
ms.locfileid: "81115989"
---
# <a name="tutorial-python-data-analytics-for-sql-developers"></a>Tutorial: Análise de dados do Python para desenvolvedores de SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Neste tutorial para programadores de SQL, saiba mais sobre a integração do Python ao criar e implantar uma solução de aprendizado de máquina baseada em Python usando um banco de dados [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) no SQL Server. Você usará o T-SQL, o SQL Server Management Studio e uma instância do mecanismo de banco de dados com os [Serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md) e o suporte à linguagem Python.

Este tutorial apresenta as funções do Python usadas em um fluxo de trabalho de modelagem de dados. As etapas incluem exploração de dados, criação e treinamento de um modelo de classificação binária e implantação de modelo. Você usará dados de exemplo da New York City Taxi and Limosine Commission e o modelo que você criará vai prever se uma corrida provavelmente resultará em uma gorjeta com base na hora do dia, na distância percorrida e na localização de embarque. 

Todo o código Python usado neste tutorial é encapsulado em procedimentos armazenados que você cria e executa no Management Studio.

> [!NOTE]
> Este tutorial está disponível no R e no Python. Para a versão do R, confira [Análise interna no banco de dados para desenvolvedores de R](sqldev-in-database-r-for-sql-developers.md).

## <a name="overview"></a>Visão geral

O processo de criação de uma solução de aprendizado de máquina é complexo, podendo envolver várias ferramentas e a coordenação de especialistas do assunto em várias fases:

+ obtenção e limpeza de dados
+ exploração de dados e criação de recursos úteis para modelagem
+ treinamento e ajuste do modelo
+ implantação para produção

O desenvolvimento e teste do código R real serão mais bem executados usando um ambiente de desenvolvimento dedicado. No entanto, depois que o script estiver totalmente testado, você poderá implantá-lo com facilidade no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando os procedimentos armazenados do [!INCLUDE[tsql](../../includes/tsql-md.md)] no ambiente conhecido do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. O encapsulamento de código externo em procedimentos armazenados é o principal mecanismo para operacionalização de código no SQL Server.

Seja você um programador do SQL não familiarizado com o Python ou um desenvolvedor de Python não familiarizado com o SQL, este tutorial de várias partes apresenta um fluxo de trabalho típico para realização de análises internas no banco de dados com Python e SQL Server. 

+ [Lição 1: Explorar e visualizar os dados usando o Python](sqldev-py3-explore-and-visualize-the-data.md)

+ [Lição 2: Criar novos recursos de dados usando funções personalizadas do SQL](sqldev-py4-create-data-features-using-t-sql.md)

+ [Lição 3: Treinar e salvar um modelo do Python usando o T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

+ [Lição 4: Prever os resultados potenciais usando um modelo do Python em um procedimento armazenado](sqldev-py6-operationalize-the-model.md)

Depois que o modelo for salvo no banco de dados, você pode usar procedimentos armazenados a fim de chamar o modelo para fazer previsões por meio do [!INCLUDE[tsql](../../includes/tsql-md.md)].

## <a name="prerequisites"></a>Pré-requisitos

+ [Serviços de Machine Learning do SQL Server usando o Python](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [Permissões](../security/user-permission.md)

+ [Banco de dados de demonstração de Táxi de Nova York](demo-data-nyctaxi-in-sql.md)

Todas as tarefas podem ser feitas usando procedimentos armazenados do [!INCLUDE[tsql](../../includes/tsql-md.md)] no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

Este tutorial pressupõe que você tem familiaridade com as operações de banco de dados, tais como criar bancos de dados e tabelas, importar dados e escrever consultas SQL. Ele não pressupõe que você conheça o Python. Como tal, todo o código Python é fornecido. 

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Explorar e visualizar os dados usando o Python](sqldev-py3-explore-and-visualize-the-data.md)
