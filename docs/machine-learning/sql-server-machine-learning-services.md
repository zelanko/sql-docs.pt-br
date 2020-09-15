---
title: O que são os Serviços de Machine Learning do SQL Server (Python e R)?
titleSuffix: ''
description: Os Serviços de Machine Learning são um recurso no SQL Server que possibilita executar scripts do Python e do R usando dados relacionais. Você pode usar pacotes e estruturas de software livre, bem como os pacotes do R e do Python da Microsoft para análise preditiva e aprendizado de máquina. Os scripts são executados no banco de dados sem mover dados para fora do SQL Server ou pela rede. Este artigo explica os conceitos básicos dos Serviços de Machine Learning do SQL Server e como começar.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 06/19/2020
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: be0e80a5d6a54726fd77b753c9910764bf5f600d
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88180363"
---
# <a name="what-is-sql-server-machine-learning-services-python-and-r"></a>O que são os Serviços de Machine Learning do SQL Server (Python e R)?
[!INCLUDE [SQL Server 2017](../includes/applies-to-version/sqlserver2017.md)]

Os Serviços de Machine Learning são um recurso no SQL Server que possibilita executar scripts do Python e do R usando dados relacionais. Você pode usar pacotes e estruturas de software livre, bem como os [pacotes do R e do Python da Microsoft](#packages) para análise preditiva e aprendizado de máquina. Os scripts são executados no banco de dados sem mover dados para fora do SQL Server ou pela rede. Este artigo explica os conceitos básicos dos Serviços de Machine Learning do SQL Server e como começar.

Para aprendizado de máquina em outras plataformas do SQL, confira a [documentação do aprendizado de máquina do SQL](index.yml).

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
> [!NOTE]
> Para executar o Java no SQL Server, confira a [Documentação das extensões de linguagem](../language-extensions/language-extensions-overview.md).
::: moniker-end

## <a name="execute-python-and-r-scripts-in-sql-server"></a>Executar scripts do Python e do R no SQL Server

Os Serviços de Machine Learning do SQL Server permitem executar scripts de Python e R no banco de dados. Você pode usá-lo para preparar e limpar dados, fazer engenharia de recursos e treinar, avaliar e implantar modelos de machine learning em um banco de dados. O recurso executa seus scripts onde os dados residem e elimina a transferência dos dados pela rede para outro servidor.

Você pode executar scripts de Python e R em uma instância do SQL Server com o procedimento armazenado [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

As distribuições base do Python e do R estão incluídas nos Serviços de Machine Learning. Você pode instalar e usar estruturas e pacotes de software livre, como PyTorch, TensorFlow e scikit-learn, além dos pacotes da Microsoft.

Os Serviços de Machine Learning usam uma estrutura de extensibilidade para executar scripts do R e do Python no SQL Server. Saiba mais sobre como isso funciona:

+ [Estrutura de extensibilidade](concepts/extensibility-framework.md)
+ [Extensão Python](concepts/extension-python.md)
+ [Extensão R](concepts/extension-r.md)

## <a name="get-started-with-machine-learning-services"></a>Introdução aos Serviços de Machine Learning

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
1. [Instalar Serviços de Machine Learning do SQL Server no Windows](install/sql-machine-learning-services-windows-install.md) ou [no Linux](../linux/sql-server-linux-setup-machine-learning.md?toc=/sql/machine-learning/toc.json). Você também pode usar [Serviços de Machine Learning em Clusters de Big Data](../big-data-cluster/machine-learning-services.md).

1. Configurar suas ferramentas de desenvolvimento. Você pode usar [executar scripts de Python e R em notebooks do Azure Data Studio](install/sql-machine-learning-azure-data-studio.md). Você também pode executar o T-SQL no [Azure Data Studio](../azure-data-studio/what-is.md).

1. Escreva seu primeiro script do Python ou R.

    + [Tutoriais do Python para aprendizado de máquina do SQL](tutorials/python-tutorials.md)
    + [Tutoriais do R para aprendizado de máquina do SQL](tutorials/r-tutorials.md)
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
1. [Instalar Serviços de Machine Learning do SQL Server no Windows](install/sql-machine-learning-services-windows-install.md).

1. Configurar suas ferramentas de desenvolvimento. Você pode usar [executar scripts de Python e R em notebooks do Azure Data Studio](install/sql-machine-learning-azure-data-studio.md). Você também pode usar o T-SQL no [Azure Data Studio](../azure-data-studio/what-is.md).

1. Escreva seu primeiro script do Python ou R.

    + [Tutoriais do Python para aprendizado de máquina do SQL](tutorials/python-tutorials.md)
    + [Tutoriais do R para aprendizado de máquina do SQL](tutorials/r-tutorials.md)
::: moniker-end

<a name="versions"></a>

## <a name="python-and-r-versions"></a>Versões do Python e do R

Confira a seguir as versões do Python e do R incluídas nos Serviços de Machine Learning.

| Versão do SQL Server | Versão do Python | Versão do R |
|-|-|-|
| Microsoft SQL Server 2017 | 3.5.2 | 3.3.3 |
| SQL Server 2019 | 3.7.3 | 3.5.2 |

Para a versão do R no SQL Server 2016, confira a [seção de versão do R em O que é o R Services?](r/sql-server-r-services.md?view=sql-server-2016#version)

<a name="packages"></a>

## <a name="python-and-r-packages"></a>Pacotes do Python e do R

Você pode usar pacotes e estruturas de software livre, além dos pacotes corporativos da Microsoft. Os pacotes de software livre do Python e do R mais comuns são pré-instalados nos Serviços de Machine Learning. Os seguintes pacotes do R e do Python da Microsoft também estão incluídos:

| Linguagem | Pacote | Descrição |
|-|-|-|
| Python | [revoscalepy](python/ref-py-revoscalepy.md) | O pacote principal para Python escalonável. Transformações e manipulação de dados, resumo estatístico, visualização e muitas formas de modelagem. Além disso, as funções nesse pacote distribuem automaticamente as cargas de trabalho entre os núcleos disponíveis para processamento paralelo. |
| Python | [microsoftml](python/ref-py-microsoftml.md) | Adiciona algoritmos de aprendizado de máquina para criar modelos personalizados para análise de texto, análise de imagem e análise de sentimentos. | 
| R | [RevoScaleR](r/ref-r-revoscaler.md) | O pacote primário para R escalonável. Transformações e manipulação de dados, resumo estatístico, visualização e muitas formas de modelagem. Além disso, as funções nesse pacote distribuem automaticamente as cargas de trabalho entre os núcleos disponíveis para processamento paralelo. |
| R | [MicrosoftML (R)](r/ref-r-microsoftml.md) | Adiciona algoritmos de aprendizado de máquina para criar modelos personalizados para análise de texto, análise de imagem e análise de sentimentos. |
| R | [olapR](r/ref-r-olapr.md) | As funções do R usadas para consultas MDX em um cubo OLAP do SQL Server Analysis Services. |
| R | [sqlrutils](r/ref-r-sqlrutils.md) | Um mecanismo para usar scripts do R em um procedimento armazenado do T-SQL, registrar esse procedimento armazenado em um banco de dados e executar procedimento armazenado em um [ambiente de desenvolvimento em R](r/set-up-a-data-science-client.md). |
| R | [Microsoft R Open](https://mran.microsoft.com/rro) | O MRO (Microsoft R Open) é a distribuição aprimorada do R da Microsoft. É uma plataforma de software livre completa para análise estatística e ciência de dados. Ela é baseada e totalmente compatível com o R e inclui recursos adicionais para melhorar o desempenho e a capacidade de reprodução. |

Para obter mais informações sobre quais pacotes são instalados com os Serviços de Machine Learning e como instalar outros pacotes, confira:

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
+ [Obter informações sobre o pacote do Python](package-management/python-package-information.md)
+ [Instalar pacotes Python com o sqlmlutils](package-management/install-additional-python-packages-on-sql-server.md)
+ [Obter informações sobre o pacote do R](package-management/r-package-information.md)
+ [Instalar novos pacotes do R com o sqlmlutils](package-management/install-additional-r-packages-on-sql-server.md).
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
+ [Obter informações sobre o pacote do Python](package-management/python-package-information.md)
+ [Instalar pacotes com ferramentas do Python no SQL Server](package-management/install-python-packages-standard-tools.md)
+ [Obter informações sobre o pacote do R](package-management/r-package-information.md)
+ [Usar o T-SQL (CRIAR BIBLIOTECA EXTERNA) para instalar pacotes do R no SQL Server](package-management/install-r-packages-with-tsql.md).
::: moniker-end

## <a name="next-steps"></a>Próximas etapas

+ [Instalar os Serviços de Machine Learning do SQL Server no Windows](install/sql-machine-learning-services-windows-install.md) ou [no Linux](../linux/sql-server-linux-setup-machine-learning.md?toc=/sql/machine-learning/toc.json)
+ [Tutoriais do Python para aprendizado de máquina do SQL](tutorials/python-tutorials.md)
+ [Tutoriais do R para aprendizado de máquina do SQL](tutorials/r-tutorials.md)
