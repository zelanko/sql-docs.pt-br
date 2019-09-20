---
title: O que é SQL Server Serviços de Machine Learning (Python e R)?
titleSuffix: ''
description: Serviços de Machine Learning é um recurso no SQL Server que oferece a capacidade de executar scripts do Python e do R com dados relacionais. Você pode usar pacotes e estruturas de software livre e os pacotes do Microsoft Python e do R para análise preditiva e aprendizado de máquina. Os scripts são executados no banco de dados sem mover dados para fora do SQL Server ou pela rede. Este artigo explica os conceitos básicos do SQL Server Serviços de Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/07/2019
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 634f9f62a3ff1de70be84fd5a7721d8efed891bf
ms.sourcegitcommit: 1661c3e1bb38ed12f8485c3860fc2d2b97dd2c9d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/20/2019
ms.locfileid: "71149934"
---
# <a name="what-is-sql-server-machine-learning-services-python-and-r"></a>O que é SQL Server Serviços de Machine Learning (Python e R)?
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Serviços de Machine Learning é um recurso no SQL Server que oferece a capacidade de executar scripts do Python e do R com dados relacionais. Você pode usar pacotes e estruturas de software livre e os pacotes do [Microsoft Python e do R](#packages) para análise preditiva e aprendizado de máquina. Os scripts são executados no banco de dados sem mover dados para fora do SQL Server ou pela rede. Este artigo explica os conceitos básicos do SQL Server Serviços de Machine Learning.

No banco de dados SQL do Azure, o [serviços de Machine Learning](https://docs.microsoft.com/azure/sql-database/sql-database-machine-learning-services-overview) está atualmente em visualização pública.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
> [!NOTE]
> Para executar o Java no SQL Server, consulte a [documentação de extensões de linguagem](../language-extensions/language-extensions-overview.md).
::: moniker-end

## <a name="what-is-machine-learning-services"></a>O que é Serviços de Machine Learning?

SQL Server Serviços de Machine Learning permite executar scripts do Python e do R no banco de dados. Você pode usá-lo para preparar e limpar dados, fazer engenharia de recursos e treinar, avaliar e implantar modelos de aprendizado de máquina em um banco de dados. O recurso executa seus scripts onde os dados residem e elimina a transferência dos dados pela rede para outro servidor.

As distribuições base do Python e do R estão incluídas no Serviços de Machine Learning. Você pode instalar e usar estruturas e pacotes de software livre, como PyTorch, TensorFlow e scikit-learn, além dos pacotes Microsoft [revoscalepy](python/ref-py-revoscalepy.md) e [microsoftml](python/ref-py-microsoftml.md) para Python e [RevoScaleR](r/ref-r-revoscaler.md), [microsoftml](r/ref-r-microsoftml.md), [olapr](r/ref-r-olapr.md)e [sqlrutils](r/ref-r-sqlrutils.md) para R.

Serviços de Machine Learning usa uma estrutura de extensibilidade para executar scripts de Python e R em SQL Server. Saiba mais sobre como isso funciona:

+ [Estrutura de extensibilidade](concepts/extensibility-framework.md)
+ [Extensão do Python](concepts/extension-python.md)
+ [Extensão de R](concepts/extension-r.md)

## <a name="what-can-i-do-with-machine-learning-services"></a>O que posso fazer com Serviços de Machine Learning?

Você pode usar Serviços de Machine Learning para criar e treinar modelos de aprendizado de máquina e aprendizado profundo no SQL Server. Você também pode implantar modelos existentes para Serviços de Machine Learning e usar dados relacionais para previsões.

Exemplos do tipo de previsões que você pode usar SQL Server Serviços de Machine Learning para, incluem:

|||
|-|-|
|Classificação/categorização|Dividir automaticamente os comentários do cliente em categorias positivas e negativas|
|Regressão/previsão de valores contínuos|Prever o preço de casas com base no tamanho e no local|
|Detecção de anomalias|Detectar transações bancárias fraudulentas |
|Recomendações|Sugira produtos que os compradores online podem querer comprar, com base em suas compras anteriores|

### <a name="how-to-execute-python-and-r-scripts"></a>Como executar scripts do Python e do R

Há duas maneiras de executar scripts do Python e do R no Serviços de Machine Learning:

+ A maneira mais comum é usar o procedimento armazenado T-SQL [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

+ Você também pode usar seu cliente do Python ou do R preferencial e gravar scripts que enviam por push a execução (conhecida como um *contexto de computação remota*) para um SQL Server remoto. Consulte como configurar um cliente de ciência de dados para [desenvolvimento em Python](python/setup-python-client-tools-sql.md) e desenvolvimento em [R](r/set-up-a-data-science-client.md) para obter mais informações.

<a name="packages"></a>

## <a name="python-and-r-packages"></a>Pacotes do Python e do R

Você pode usar pacotes e estruturas de software livre, além dos pacotes corporativos da Microsoft. Os pacotes python e R mais comuns de software livre são pré-instalados em Serviços de Machine Learning. Os seguintes pacotes do Python e do R da Microsoft também estão incluídos:

| Idioma | Pacote | Descrição |
|-|-|-|
| Python | [revoscalepy](python/ref-py-revoscalepy.md) | O pacote principal para Python escalonável. Transformações e manipulação de dados, Resumo Estatístico, visualização e muitas formas de modelagem. Além disso, as funções nesse pacote distribuem automaticamente as cargas de trabalho entre os núcleos disponíveis para processamento paralelo. |
| Python | [microsoftml](python/ref-py-microsoftml.md) | Adiciona algoritmos de aprendizado de máquina para criar modelos personalizados para análise de texto, análise de imagem e análise de sentimentos. | 
| R | [RevoScaleR](r/ref-r-revoscaler.md) | O pacote primário para transformações e manipulação de R. Data escalonáveis, Resumo Estatístico, visualização e muitas formas de modelagem. Além disso, as funções nesse pacote distribuem automaticamente as cargas de trabalho entre os núcleos disponíveis para processamento paralelo. |
| R | [MicrosoftML (R)](r/ref-r-microsoftml.md) | Adiciona algoritmos de aprendizado de máquina para criar modelos personalizados para análise de texto, análise de imagem e análise de sentimentos. |
| R | [olapR](r/ref-r-olapr.md) | Funções do R usadas para consultas MDX em um SQL Server Analysis Services cubo OLAP. |
| R | [sqlrutils](r/ref-r-sqlrutils.md) | Um mecanismo para usar scripts R em um procedimento armazenado T-SQL, registrar esse procedimento armazenado em um banco de dados e executar o procedimento armazenado de um [ambiente de desenvolvimento de R](r/set-up-a-data-science-client.md). |
| R | [Microsoft R Open](https://mran.microsoft.com/rro) | O Microsoft R Open (MRO) é a distribuição aprimorada do R da Microsoft. É uma plataforma de software livre completa para análise estatística e ciência de dados. Ele é baseado em e 100% compatível com o R e inclui recursos adicionais para melhorar o desempenho e o reprodução. |

Para obter mais informações sobre quais pacotes são instalados com Serviços de Machine Learning e como instalar outros pacotes, consulte:

+ [Obter informações do pacote do Python](package-management/python-package-information.md)
+ [Instalar pacotes do Python com o sqlmlutils](package-management/install-additional-python-packages-on-sql-server.md)
+ [Obter informações do pacote do R](package-management/r-package-information.md)
+ [Instale novos pacotes de R com sqlmlutils](package-management/install-additional-r-packages-on-sql-server.md).

## <a name="how-do-i-get-started-with-machine-learning-services"></a>Como fazer introdução ao Serviços de Machine Learning?

1. [Instalar SQL Server Serviços de Machine Learning](install/sql-machine-learning-services-windows-install.md)

1. Configure suas ferramentas de desenvolvimento. Você pode usar:

    + [Azure Data Studio](../azure-data-studio/what-is.md) ou [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md) para usar o T-SQL e o procedimento armazenado [Sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para executar seu script Python ou R.
    + Python ou R em seu próprio laptop de desenvolvimento ou estação de trabalho para executar scripts. Você pode efetuar pull de dados localmente ou enviar a execução remotamente para SQL Server com [revoscalepy](python/ref-py-revoscalepy.md) e [RevoScaleR](r/ref-r-revoscaler.md). Consulte como configurar um cliente de ciência de dados para [desenvolvimento em Python](python/setup-python-client-tools-sql.md) e desenvolvimento em [R](r/set-up-a-data-science-client.md) para obter mais informações.

1. Escreva seu primeiro script Python ou R

    + Início Rápido: [Criar e executar scripts R simples no SQL](tutorials/quickstart-r-create-script.md)
    + Início Rápido: [Criar e treinar um modelo de previsão em R](tutorials/quickstart-r-train-score-model.md)
    + Tutorial: [Usar o Python no T-SQL](tutorials/sqldev-in-database-python-for-sql-developers.md): Explorar dados, executar a engenharia de recursos, treinar e implantar modelos e fazer previsões (série de cinco partes)
    + Tutorial: [Use o R no T-SQL](tutorials/sqldev-in-database-r-for-sql-developers.md): Explorar dados, executar a engenharia de recursos, treinar e implantar modelos e fazer previsões (série de cinco partes)
    + Tutorial: [Use serviços de Machine Learning em ferramentas de R](tutorials/walkthrough-data-science-end-to-end-walkthrough.md): Explorar dados, criar gráficos e plotagens, executar a engenharia de recursos, treinar e implantar modelos e fazer previsões (série de seis partes)

## <a name="next-steps"></a>Próximas etapas

+ [Instalar SQL Server Serviços de Machine Learning](install/sql-machine-learning-services-windows-install.md)
+ Configure um cliente de ciência de dados para [desenvolvimento em Python](python/setup-python-client-tools-sql.md) e desenvolvimento de [R](r/set-up-a-data-science-client.md)
