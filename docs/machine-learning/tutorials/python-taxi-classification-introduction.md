---
title: 'Tutorial do Python: prever as tarifas de táxi de Nova York com a classificação binária'
titleSuffix: SQL machine learning
description: Saiba como inserir código Python em procedimentos armazenados do SQL Server e em funções do T-SQL com o aprendizado de máquina do SQL para prever tarifas de táxi de Nova York usando a classificação binária.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/28/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||>=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 1fc4ea656830eb779b80b22a15a74dfd799781aa
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178564"
---
# <a name="python-tutorial-predict-nyc-taxi-fares-with-binary-classification"></a>Tutorial do Python: prever as tarifas de táxi de Nova York com a classificação binária
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Nesta série de tutoriais em cinco partes para programadores do SQL, você aprenderá sobre a integração do Python nos [Serviços do Machine Learning do SQL Server](../sql-server-machine-learning-services.md) ou nos [Clusters de Big Data](../../big-data-cluster/machine-learning-services.md).
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Nesta série de tutoriais em cinco partes para programadores do SQL, você aprenderá sobre a integração do Python nos [Serviços do Machine Learning do SQL Server](../sql-server-machine-learning-services.md).
::: moniker-end

::: moniker range=">=azuresqldb-mi-current||=sqlallproducts-allversions"
Nesta série de tutoriais em cinco partes para programadores do SQL, você aprenderá sobre a integração do Python nos [Serviços do Machine Learning na Instância Gerenciada de SQL do Azure](/azure/azure-sql/managed-instance/machine-learning-services-overview).
::: moniker-end

Você criará e implantará uma solução de aprendizado de máquina baseada em Python usando um banco de dados de exemplo no SQL Server. Você usará o T-SQL,o Azure Data Studio ou o SQL Server Management Studio e uma instância do banco de dados com o aprendizado de máquina do SQL e o suporte à linguagem Python.

Esta série de tutoriais apresenta as funções do Python usadas em um fluxo de trabalho de modelagem de dados. As partes incluem exploração de dados, criação e treinamento de um modelo de classificação binária e implantação de modelo. Você usará dados de exemplo da Comissão de Táxi e Limusines de Nova York. O modelo que você criará prevê se uma corrida provavelmente resultará em uma gorjeta com base na hora do dia, na distância percorrida e na localização de embarque.

Na primeira parte desta série, você instalará os pré-requisitos e restaurará o banco de dados de exemplo. Nas partes dois e três, você desenvolverá alguns scripts do Python para preparar seus dados e treinar um modelo de machine learning. Em seguida, nas partes quatro e cinco, você executará esses scripts do Python dentro do banco de dados usando procedimentos armazenados do T-SQL.

Neste artigo, você vai:

> [!div class="checklist"]
> + Instalar pré-requisitos
> + Restaurar o banco de dados de exemplo

Na [parte dois](python-taxi-classification-explore-data.md), você explorará os dados de exemplo e gerará alguns gráficos.

Na [parte três](python-taxi-classification-create-features.md), você aprenderá a criar recursos a partir de dados brutos usando uma função Transact-SQL. Você chamará essa função por meio de um procedimento armazenado para criar uma tabela que contém os valores do recurso.

Na [parte quatro](python-taxi-classification-train-model.md), você carregará os módulos e chamará as funções necessárias para criar e treinar o modelo usando um procedimento armazenado do SQL Server.

Na [parte cinco](python-taxi-classification-deploy-model.md), você aprenderá a operacionalizar os modelos treinados e salvos na parte quatro.

> [!NOTE]
> Este tutorial está disponível no R e no Python. Para a versão do R, confira o [Tutorial do R: prever as tarifas de táxi de Nova York com a classificação binária](r-taxi-classification-introduction.md).

## <a name="prerequisites"></a>Pré-requisitos

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
+ Instalar [Serviços de Machine Learning do SQL Server usando o Python](../install/sql-machine-learning-services-windows-install.md#verify-installation)
::: moniker-end

+ [Conceder permissões para executar scripts do Python](../security/user-permission.md)

+ Restaurar o [Banco de dados de demonstração de Táxi de Nova York](demo-data-nyctaxi-in-sql.md)

Todas as tarefas podem ser feitas usando procedimentos armazenados do [!INCLUDE[tsql](../../includes/tsql-md.md)] no Azure Data Studio ou no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

Esta série de tutoriais pressupõe que você tem familiaridade com as operações de banco de dados, como criar bancos de dados e tabelas, importar dados e escrever consultas SQL. Ela não pressupõe que você conhece o Python, e todo o código Python é fornecido.

## <a name="background-for-sql-developers"></a>Contexto para desenvolvedores de SQL

O processo de criação de uma solução de aprendizado de máquina é complexo, podendo envolver várias ferramentas e a coordenação de especialistas do assunto em várias fases:

+ obtenção e limpeza de dados
+ exploração de dados e criação de recursos úteis para modelagem
+ treinamento e ajuste do modelo
+ implantação para produção

O desenvolvimento e teste do código R real serão mais bem executados usando um ambiente de desenvolvimento dedicado. No entanto, depois que o script estiver totalmente testado, você poderá implantá-lo com facilidade no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando os procedimentos armazenados do [!INCLUDE[tsql](../../includes/tsql-md.md)] no ambiente conhecido do Azure Data Studio ou do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. O encapsulamento de código externo em procedimentos armazenados é o principal mecanismo para operacionalização de código no SQL Server.

Depois que o modelo for salvo no banco de dados, você pode usar procedimentos armazenados a fim de chamar o modelo para fazer previsões por meio do [!INCLUDE[tsql](../../includes/tsql-md.md)].

Seja você um programador do SQL não familiarizado com o Python ou um desenvolvedor do Python não familiarizado com o SQL, esta série de tutoriais em cinco partes apresenta um fluxo de trabalho típico para realização de análises internas no banco de dados com Python e SQL Server.

## <a name="next-steps"></a>Próximas etapas

Neste artigo você:

> [!div class="checklist"]
> + Instalou os pré-requisitos
> + Restaurou o banco de dados de exemplo

> [!div class="nextstepaction"]
> [Tutorial do Python: explorar e visualizar dados](python-taxi-classification-explore-data.md)