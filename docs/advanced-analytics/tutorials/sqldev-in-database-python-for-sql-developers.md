---
title: No banco de dados análise do Python para desenvolvedores do SQL | Microsoft Docs
description: Saiba como incorporar código Python em procedimentos armazenados do SQL Server e funções T-SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 8c992cbda06d158bec0b76d6d46d71157a08cf3e
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51032983"
---
# <a name="tutorial-in-database-python-analytics-for-sql-developers"></a>Tutorial: Análise do Python no banco de dados para desenvolvedores do SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Neste tutorial para programadores SQL, saiba mais sobre a integração do Python criando e implantando uma solução usando de aprendizado de máquina baseada em Python uma [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) banco de dados no SQL Server. 

Este tutorial apresenta funções Python usadas em um fluxo de trabalho de modelagem de dados. As etapas incluem a exploração de dados, criar e treinar um modelo de classificação binária e a implantação de modelo. Você usará os dados de exemplo do táxi de Nova York e Limosine comissão e o modelo que você irá criar prevê se uma corrida é provavelmente resultará em uma dica com base na hora do dia, distância percorreu e coleta local. Todo o código Python usado neste tutorial é encapsulado em procedimentos armazenados que você criar e executar no Management Studio.

> [!NOTE]
> Este tutorial está disponível em R e Python. Para a versão do R, consulte [no banco de dados do analytics para os desenvolvedores do R](sqldev-in-database-r-for-sql-developers.md).

## <a name="overview"></a>Visão geral

O processo de criação de uma solução de aprendizado de máquina é um complexo que pode envolver várias ferramentas e a coordenação de especialistas no assunto em várias fases:

+ obtenção e limpeza de dados
+ explorar os dados e criação de recursos úteis para a modelagem
+ treinamento e o modelo de ajuste
+ implantação na produção

Desenvolvimento e teste do código real é mais bem executados usando um ambiente de desenvolvimento dedicado. No entanto, depois que o script é totalmente testado, você pode facilmente implantá-lo para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimentos armazenados no ambiente familiar do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Encapsular o código externo em procedimentos armazenados é o principal mecanismo para operacionalizar código no SQL Server.

Se você for um programador SQL novo Python ou o desenvolvedor Python novidade no SQL, este tutorial com várias partes introduz um fluxo de trabalho típico para realizar a análise no banco de dados com Python e o SQL Server. 

+ [Lição 1: Explorar e visualizar os dados usando o Python](sqldev-py3-explore-and-visualize-the-data.md)

+ [Lição 2: Criar dados de recursos usando funções personalizadas do SQL](sqldev-py4-create-data-features-using-t-sql.md)

+ [Lição 3: Treinar e salvar um modelo de Python usando o T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

+ [Lição 4: Prever resultados possíveis, usando um modelo de Python em um procedimento armazenado](sqldev-py6-operationalize-the-model.md)

Depois que o modelo foi salvo no banco de dados, você pode chamar o modelo para previsões de [!INCLUDE[tsql](../../includes/tsql-md.md)] usando procedimentos armazenados.

## <a name="prerequisites"></a>Prerequisites

+ [Serviços de aprendizado de máquina do SQL Server 2017 com o Python](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [Permissões](../security/user-permission.md)

+ [Banco de dados de demonstração de táxi de NYC](demo-data-nyctaxi-in-sql.md)

Todas as tarefas podem ser feitas usando [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimentos armazenados no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

Este tutorial presume familiaridade com operações de banco de dados básico, como criação de tabelas e bancos de dados, importação de dados e escrever consultas SQL. Ele pressupõe que conheça o Python. Assim, todo o código Python é fornecido. 

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Explorar e visualizar os dados usando o Python](sqldev-py3-explore-and-visualize-the-data.md)
