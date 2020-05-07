---
title: O que são os Serviços de Machine Learning do SQL Server (Python e R)?
titleSuffix: ''
description: Os Serviços de Machine Learning são um recurso no SQL Server que possibilita executar scripts do Python e do R usando dados relacionais. Você pode usar pacotes e estruturas de software livre, bem como os pacotes do R e do Python da Microsoft para análise preditiva e aprendizado de máquina. Os scripts são executados no banco de dados sem mover dados para fora do SQL Server ou pela rede. Este artigo explica os conceitos básicos dos Serviços de Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 02/06/2020
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: afce689bffe69de78970006aea51ddd49481e614
ms.sourcegitcommit: 9afb612c5303d24b514cb8dba941d05c88f0ca90
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2020
ms.locfileid: "82220651"
---
# <a name="what-is-sql-server-machine-learning-services-python-and-r"></a>O que são os Serviços de Machine Learning do SQL Server (Python e R)?
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Os Serviços de Machine Learning são um recurso no SQL Server que possibilita executar scripts do Python e do R usando dados relacionais. Você pode usar pacotes e estruturas de software livre, bem como os [pacotes do R e do Python da Microsoft](#packages) para análise preditiva e aprendizado de máquina. Os scripts são executados no banco de dados sem mover dados para fora do SQL Server ou pela rede. Este artigo explica os conceitos básicos dos Serviços de Machine Learning do SQL Server.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
> [!NOTE]
> Para executar o Java no SQL Server, confira a [Documentação das extensões de linguagem](../language-extensions/language-extensions-overview.md).
::: moniker-end

## <a name="what-is-machine-learning-services"></a>O que são os Serviços de Machine Learning?

Os Serviços de Machine Learning do SQL Server permitem executar scripts de Python e R no banco de dados. Você pode usá-lo para preparar e limpar dados, fazer engenharia de recursos e treinar, avaliar e implantar modelos de machine learning em um banco de dados. O recurso executa seus scripts onde os dados residem e elimina a transferência dos dados pela rede para outro servidor.

As distribuições base do Python e do R estão incluídas nos Serviços de Machine Learning. Você pode instalar e usar estruturas e pacotes de software livre, como PyTorch, TensorFlow e Scikit-learn, além dos pacotes da Microsoft [revoscalepy](python/ref-py-revoscalepy.md) e [microsoftml](python/ref-py-microsoftml.md) para Python e [RevoScaleR](r/ref-r-revoscaler.md), [MicrosoftML](r/ref-r-microsoftml.md), [olapR](r/ref-r-olapr.md) e [sqlrutils](r/ref-r-sqlrutils.md) para R.

Os Serviços de Machine Learning usam uma estrutura de extensibilidade para executar scripts do R e do Python no SQL Server. Saiba mais sobre como isso funciona:

+ [Estrutura de extensibilidade](concepts/extensibility-framework.md)
+ [Extensão Python](concepts/extension-python.md)
+ [Extensão R](concepts/extension-r.md)

## <a name="what-can-i-do-with-machine-learning-services"></a>O que posso fazer com os Serviços de Machine Learning?

Você pode usar os Serviços de Machine Learning para criar e treinar o aprendizado de máquina e os modelos de aprendizado profundo dentro do SQL Server. Você também pode implantar modelos existentes nos Serviços de Machine Learning e usar dados relacionais para previsões.

Os exemplos do tipo de previsões nas quais você pode usar os Serviços de Machine Learning do SQL Server incluem:

|||
|-|-|
|Classificação/Categorização|Dividir automaticamente os comentários dos clientes em categorias positivas e negativas|
|Regressão/Prever valores contínuos|Prever o preço de residências com base em tamanho e localização|
|Detecção de anomalias|Detectar transações bancárias fraudulentas |
|Recomendações|Sugerir produtos que compradores online talvez queiram comprar com base em suas compras anteriores|

### <a name="how-to-execute-python-and-r-scripts"></a>Como executar scripts do Python e do R

Há duas maneiras de executar scripts do Python e do R nos Serviços de Machine Learning:

+ A maneira mais comum é usar o procedimento armazenado [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) do T-SQL.

+ Você também pode usar seu cliente R ou Python preferencial e gravar scripts que efetuam push da execução (chamada de *contexto de computação remota*) para um SQL Server remoto. Veja como configurar um cliente de ciência de dados para [desenvolvimento em Python](python/setup-python-client-tools-sql.md) e [desenvolvimento em R](r/set-up-a-data-science-client.md) para obter mais informações.

<a name="versions"></a>

## <a name="python-and-r-versions"></a>Versões do Python e do R

Veja as seguintes versões do Python e do R incluídas nos Serviços de Machine Learning com cada versão do SQL Server.

| Versão do SQL Server | Versão do Python | Versão do R |
|-|-|-|
| Microsoft SQL Server 2017 | 3.5.2 | 3.3.3 |
| SQL Server 2019 | 3.7.3 | 3.5.2 |

Para a versão do R no SQL Server 2016, confira a [seção de versão do R em O que é o R Services?](r/sql-server-r-services.md#version)

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

+ [Obter informações sobre o pacote do Python](package-management/python-package-information.md)
+ [Instalar pacotes Python com o sqlmlutils](package-management/install-additional-python-packages-on-sql-server.md)
+ [Obter informações sobre o pacote do R](package-management/r-package-information.md)
+ [Instalar novos pacotes do R com o sqlmlutils](package-management/install-additional-r-packages-on-sql-server.md).

## <a name="how-do-i-get-started-with-machine-learning-services"></a>Como começar a usar os Serviços de Machine Learning?

1. [Instalar os Serviços de Machine Learning do SQL Server](install/sql-machine-learning-services-windows-install.md)

1. Configurar suas ferramentas de desenvolvimento. Você pode usar:

    + [Azure Data Studio](../azure-data-studio/what-is.md) ou [SSMS (SQL Server Management Studio)](../ssms/sql-server-management-studio-ssms.md) para usar o T-SQL e o procedimento armazenado [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para executar o script do R ou Python.
    + Python ou R em seu próprio laptop de desenvolvimento ou estação de trabalho para executar scripts. Você pode efetuar pull de dados localmente ou efetuar push da execução remotamente para o SQL Server com o [revoscalepy](python/ref-py-revoscalepy.md) e o [RevoScaleR](r/ref-r-revoscaler.md). Veja como configurar um cliente de ciência de dados para [desenvolvimento em Python](python/setup-python-client-tools-sql.md) e [desenvolvimento em R](r/set-up-a-data-science-client.md) para obter mais informações.

1. Escrever seu primeiro script do Python ou do R

    + Início Rápido: [Executar scripts simples do Python](tutorials/quickstart-python-create-script.md)
    + Início Rápido: [Executar scripts simples do R](tutorials/quickstart-r-create-script.md)
    + Tutorial: [Usar o Python no T-SQL](tutorials/sqldev-in-database-python-for-sql-developers.md): Explorar dados, executar engenharia de recursos, treinar e implantar modelos e fazer previsões (série de cinco partes)
    + Tutorial: [Usar o R no T-SQL](tutorials/sqldev-in-database-r-for-sql-developers.md): Explorar dados, executar engenharia de recursos, treinar e implantar modelos e fazer previsões (série de cinco partes)

## <a name="next-steps"></a>Próximas etapas

+ [Instalar os Serviços de Machine Learning do SQL Server](install/sql-machine-learning-services-windows-install.md)
+ Configurar um cliente de ciência de dados para [desenvolvimento em Python](python/setup-python-client-tools-sql.md) e [desenvolvimento em R](r/set-up-a-data-science-client.md)
