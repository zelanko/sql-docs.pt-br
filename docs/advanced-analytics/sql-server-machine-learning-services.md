---
title: Documentação de aprendizado de máquina R e Python
description: R e Python no SQL Server, com a modelagem de ciência de dados interna e algoritmos de aprendizado de máquina para análise de dados corporativos em escala.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 8eb391ac4b64c93de255214d748c77f44dccb1b3
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344743"
---
# <a name="sql-server-machine-learning-services"></a>Serviços de SQL Server Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

## <a name="sql-server-machine-learning-services-r-and-python-documentation"></a>Documentação do SQL Server Serviços de Machine Learning (R e Python)

Saiba como usar bibliotecas externas do R e Python e linguagens em dados relacionais residentes com nossos guias de início rápido, tutoriais e artigos de instruções. As bibliotecas R e Python no [SQL Server serviços de Machine Learning](what-is-sql-server-machine-learning.md) incluem distribuições base, modelos de ciência de dados, algoritmos de aprendizado de máquina e funções para realizar análises de alto desempenho em escala, sem precisar transferir dados entre os rede.

::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
> [!NOTE]
> Para obter a documentação sobre Java, consulte a [documentação de extensões de linguagem SQL Server](https://docs.microsoft.com/sql/language-extensions/language-extensions-overview).
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

- [Como instalar Serviços de Machine Learning para SQL Server](install/sql-machine-learning-services-windows-install.md)

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
