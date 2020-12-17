---
title: 'Tutorial do R: prever as tarifas de táxi de Nova York com a classificação binária'
titleSuffix: SQL machine learning
description: Nesta série de tutoriais em cinco partes, você aprenderá como incorporar o código R em procedimentos armazenados do SQL Server e funções do T-SQL com o aprendizado de máquina do SQL para prever tarifas de táxi em NYC usando a classificação binária.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/15/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||>=azuresqldb-mi-current'
ms.openlocfilehash: afc692cdd0b7766ff0366f0de5d13e47d6dc27e1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470177"
---
# <a name="r-tutorial-predict-nyc-taxi-fares-with-binary-classification"></a>Tutorial do R: prever as tarifas de táxi de Nova York com a classificação binária
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
Nesta série de tutoriais em cinco partes para programadores do SQL, você aprenderá sobre a integração do R nos [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md) ou nos [Clusters de Big Data](../../big-data-cluster/machine-learning-services.md).
::: moniker-end

::: moniker range="=sql-server-2017"
Nesta série de tutoriais em cinco partes para programadores do SQL, você aprenderá sobre a integração do R nos [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md).
::: moniker-end

::: moniker range="=sql-server-2016"
Nesta série de tutoriais em cinco partes para programadores do SQL, você aprenderá sobre a integração do R no [SQL Server 2016 R Services](../sql-server-machine-learning-services.md).
::: moniker-end

::: moniker range=">=azuresqldb-mi-current"
Nesta série de tutoriais em cinco partes para programadores do SQL, você conhecerá a integração do R nos [Serviços de Machine Learning na Instância Gerenciada de SQL do Azure](/azure/azure-sql/managed-instance/machine-learning-services-overview).
::: moniker-end

Você criará e implantará uma solução de aprendizado de máquina baseada em R usando um banco de dados de exemplo no SQL Server. Você usará o T-SQL, o Azure Data Studio ou o SQL Server Management Studio e uma instância do mecanismo de banco de dados com o aprendizado de máquina do SQL e o suporte à linguagem R

Esta série de tutoriais apresenta as funções do R usadas em um fluxo de trabalho de modelagem de dados. As partes incluem exploração de dados, criação e treinamento de um modelo de classificação binária e implantação de modelo. Você usará dados de exemplo da Comissão de Táxi e Limusines de Nova York. O modelo que você criará prevê se uma corrida provavelmente resultará em uma gorjeta com base na hora do dia, na distância percorrida e na localização de embarque.

Na primeira parte desta série, você instalará os pré-requisitos e restaurará o banco de dados de exemplo. Nas partes dois e três, você desenvolverá alguns scripts do R para preparar seus dados e treinar um modelo de machine learning. Em seguida, nas partes quatro e cinco, você executará esses scripts do R dentro no banco de dados usando procedimentos armazenados do T-SQL.

Neste artigo, você vai:

> [!div class="checklist"]
> + Instalar pré-requisitos
> + Restaurar o banco de dados de exemplo

Na [parte dois](r-taxi-classification-explore-data.md), você explorará os dados de exemplo e gerará alguns gráficos.

Na [parte três](r-taxi-classification-create-features.md), você aprenderá a criar recursos a partir de dados brutos usando uma função do Transact-SQL. Você chamará essa função por meio de um procedimento armazenado para criar uma tabela que contém os valores do recurso.

Na [parte quatro](r-taxi-classification-train-model.md), você carregará os módulos e chamará as funções necessárias para criar e treinar o modelo usando um procedimento armazenado do SQL Server.

Na [parte cinco](r-taxi-classification-deploy-model.md), você aprenderá a operacionalizar os modelos treinados e salvos na parte quatro.

> [!NOTE]
> Este tutorial está disponível no R e no Python. Para a versão do Python, confira [Tutorial do Python: prever as tarifas de táxi de Nova York com a classificação binária](r-taxi-classification-introduction.md).

## <a name="prerequisites"></a>Pré-requisitos

::: moniker range="=sql-server-2016"
+ [Instalar o SQL Server 2016 R Services](../install/sql-r-services-windows-install.md#verify-installation)
::: moniker-end

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15"
+ Instalar os [Serviços de Machine Learning do SQL Server com o R habilitado](../install/sql-machine-learning-services-windows-install.md#verify-installation)
::: moniker-end

+ Instalar [bibliotecas do R](../package-management/r-package-information.md)

+ [Conceder permissões para executar scripts do Python](../security/user-permission.md)

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
+ A partir do SQL Server 2019, o mecanismo de isolamento exige que você conceda as permissões apropriadas ao diretório em que o arquivo de gráfico está armazenado. Confira mais informações sobre como definir essas permissões na [seção Permissões de arquivo em SQL Server 2019 no Windows: alterações de isolamento nos Serviços de Machine Learning](../install/sql-server-machine-learning-services-2019.md#file-permissions).
::: moniker-end

+ Restaurar o [Banco de dados de demonstração de Táxi de Nova York](demo-data-nyctaxi-in-sql.md)

Todas as tarefas podem ser feitas usando procedimentos armazenados do [!INCLUDE[tsql](../../includes/tsql-md.md)] no Azure Data Studio ou no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

Este tutorial pressupõe que você tem familiaridade com as operações de banco de dados, tais como criar bancos de dados e tabelas, importar dados e escrever consultas SQL. Ela não pressupõe que você conhece o R, e todo o código R é fornecido.

## <a name="background-for-sql-developers"></a>Contexto para desenvolvedores de SQL

O processo de criação de uma solução de aprendizado de máquina é complexo, podendo envolver várias ferramentas e a coordenação de especialistas do assunto em várias fases:

+ obtenção e limpeza de dados
+ exploração de dados e criação de recursos úteis para modelagem
+ treinamento e ajuste do modelo
+ implantação para produção

O desenvolvimento e teste do código do R real serão mais bem executados usando um ambiente de desenvolvimento R dedicado. No entanto, depois que o script estiver totalmente testado, você poderá implantá-lo com facilidade no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando os procedimentos armazenados do [!INCLUDE[tsql](../../includes/tsql-md.md)] no ambiente conhecido do Azure Data Studio ou do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. O encapsulamento de código externo em procedimentos armazenados é o principal mecanismo para operacionalização de código no SQL Server.

Depois que o modelo for salvo no banco de dados, você pode usar procedimentos armazenados a fim de chamar o modelo para fazer previsões por meio do [!INCLUDE[tsql](../../includes/tsql-md.md)].

Seja você um programador do SQL não familiarizado com o R ou um desenvolvedor do R não familiarizado com o SQL, esta série de tutoriais em cinco partes apresenta um fluxo de trabalho típico para realização de análises internas no banco de dados com R e SQL Server.

## <a name="next-steps"></a>Próximas etapas

Neste artigo você:

> [!div class="checklist"]
> + Instalou os pré-requisitos
> + Restaurou o banco de dados de exemplo

> [!div class="nextstepaction"]
> [Tutorial do R: explorar e visualizar dados](r-taxi-classification-explore-data.md)