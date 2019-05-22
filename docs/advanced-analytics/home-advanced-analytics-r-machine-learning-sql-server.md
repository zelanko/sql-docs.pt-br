---
title: Documentação - serviços de aprendizado de máquina do SQL Server de aprendizado de máquina de R e Python
description: R e Python no SQL Server, com a modelagem de ciência de dados interna e algoritmos de aprendizado de máquina para análise de dados corporativos em escala.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/22/2019
ms.topic: overview
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: e93d9ad5fd6415b6d8c1b6208857e81d60de2bd0
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65994125"
---
# <a name="sql-server-machine-learning-services"></a>Serviços de SQL Server Machine Learning

## <a name="sql-server-machine-learning-services-r-and-python-documentation"></a>Documentação dos serviços (R e Python) de aprendizado de máquina do SQL Server

Saiba como usar bibliotecas externas do R e Python e linguagens em dados relacionais residentes com nossos guias de início rápido, tutoriais e artigos de instruções. As bibliotecas de R e Python no [Machine Learning do SQL Server](what-is-sql-server-machine-learning.md) incluem distribuições de base, modelos de ciência de dados, algoritmos de aprendizado de máquina e funções para conduzir a análise de alto desempenho em escala, sem precisar transferir dados pela rede.

::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
> [!NOTE]
> Para a documentação do Java, consulte o [documentação de extensões de linguagem do SQL Server](https://docs.microsoft.com/sql/language-extensions/language-extensions-overview).
::: moniker-end

|   |   |
|---|:--|
| ![Logotipo do R](media/index/logo_r.png) | R de software livre, estendido com [RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) e algoritmos da IA da Microsoft no [MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package). Essas bibliotecas fornecem modelos de previsão, análise estatística, visualização e manipulação de dados em escala.<br/>A integração do R começa no [SQL Server 2016](install/sql-r-services-windows-install.md) e também está no [SQL Server 2017](install/sql-machine-learning-services-windows-install.md). |
| ![Logotipo do Python](media/index/logo_python.png) | Os desenvolvedores de Python podem usar as bibliotecas [revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) e [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) da Microsoft para análise preditiva e aprendizado de máquina em escala. As bibliotecas compatíveis com Anaconda e Python 3.5 são a distribuição de linha de base.<br/>A integração do Python começa no [SQL Server 2017](install/sql-machine-learning-services-windows-install.md). |
| &nbsp; | &nbsp; |

## <a name="5-minute-quickstarts"></a>Guias de início rápido de cinco minutos

- [Criar um modelo preditivo em R](tutorials/rtsql-create-a-predictive-model-r.md)

- [Prever e plotar com base no modelo usando R](tutorials/rtsql-predict-and-plot-from-model.md)

## <a name="step-by-step-tutorials"></a>Tutoriais passo a passo

- [Como adicionar o aprendizado de máquina e a estrutura de extensibilidade ao SQL Server](install/sql-machine-learning-services-windows-install.md)

- [Como executar o R do T-SQL e procedimentos armazenados](tutorials/sqldev-in-database-r-for-sql-developers.md)

- [Como usar a análise integrada no Python](tutorials/sqldev-in-database-python-for-sql-developers.md)

## <a name="video-introduction"></a>Introdução de vídeo

> [!VIDEO https://www.youtube.com/embed/ACejZ9optCQ]

## <a name="reference"></a>Referência

| Pacote | Idioma | Descrição |
|:--------|:---------|:------------|
| [RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) | R | Processamento paralelo e distribuído para tarefas do R: transformação de dados, exploração, visualização, estatística e análise preditiva. |
| [MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package) | R | Funções com base em algoritmos de IA da Microsoft, adaptado para R. |
| [olapR](/machine-learning-server/r-reference/olapr/olapr) | R | Importa dados de cubos OLAP. |
| [sqlRUtils](/machine-learning-server/r-reference/sqlrutils/sqlrutils) | R | Funções de auxiliar para encapsular o R e T-SQL. |
[revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | Python | Processamento paralelo e distribuído para tarefas do Python: transformação de dados, exploração, visualização, estatística e análise preditiva. |
| [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) | Python | Funções com base em algoritmos de IA da Microsoft, adaptado para Python. |
| &nbsp; | &nbsp; | &nbsp; |
