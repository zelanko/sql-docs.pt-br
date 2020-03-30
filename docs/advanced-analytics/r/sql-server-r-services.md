---
title: O que é o SQL Server 2016 R Services?
titleSuffix: ''
description: O R Services é um recurso do SQL Server 2016 que oferece a capacidade de executar scripts do R usando dados relacionais. Você pode usar pacotes e estruturas de software livre, bem como os pacotes do R da Microsoft para análise preditiva e aprendizado de máquina. Os scripts são executados no banco de dados sem mover dados para fora do SQL Server ou pela rede. Este artigo explica os conceitos básicos do SQL Server R Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/12/2019
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: =sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 48f3b3433d0ca2f4daf08048228989598c5cf36a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "79286080"
---
# <a name="what-is-sql-server-2016-r-services"></a>O que é o SQL Server 2016 R Services?
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O R Services é um recurso do SQL Server 2016 que oferece a capacidade de executar scripts do R usando dados relacionais. Você pode usar pacotes e estruturas de software livre, bem como os [pacotes do R da Microsoft](#packages) para análise preditiva e aprendizado de máquina. Os scripts são executados no banco de dados sem mover dados para fora do SQL Server ou pela rede. Este artigo explica os conceitos básicos do SQL Server R Services.

> [!Note]
> O R Services foi renomeado para [Serviços de Machine Learning](../what-is-sql-server-machine-learning.md) no SQL Server 2017 e posterior e é compatível com Python e R.

## <a name="what-is-r-services"></a>O que são os Serviços R?

O SQL Server R Services permite executar scripts do R no banco de dados. Você pode usá-lo para preparar e limpar dados, fazer engenharia de recursos e treinar, avaliar e implantar modelos de machine learning em um banco de dados. O recurso executa seus scripts onde os dados residem e elimina a transferência dos dados pela rede para outro servidor.

As distribuições base do R estão incluídas no R Services. Você pode usar pacotes e estruturas de software livre além dos pacotes da Microsoft [RevoScaleR](../r/ref-r-revoscaler.md), [MicrosoftML](../r/ref-r-microsoftml.md), [olapR]../r/ref-r-olapr.md) e [sqlrutils](../r/ref-r-sqlrutils.md) para R.

O R Services usa uma estrutura de extensibilidade para executar scripts do R no SQL Server. Saiba mais sobre como isso funciona:

+ [Estrutura de extensibilidade](../concepts/extensibility-framework.md)
+ [Extensão R](../concepts/extension-r.md)

## <a name="what-can-i-do-with-r-services"></a>O que eu posso fazer com o R Services?

Você pode usar o R Services para criar e treinar o aprendizado de máquina e os modelos de aprendizado profundo dentro do SQL Server. Você também pode implantar modelos existentes no R Services e usar dados relacionais para previsões.

Exemplos do tipo de previsões nas quais você pode usar SQL Server R Services incluem:

|||
|-|-|
|Classificação/Categorização|Dividir automaticamente os comentários dos clientes em categorias positivas e negativas|
|Regressão/Prever valores contínuos|Prever o preço de residências com base em tamanho e localização|
|Detecção de anomalias|Detectar transações bancárias fraudulentas |
|Recomendações|Sugerir produtos que compradores online talvez queiram comprar com base em suas compras anteriores|

### <a name="how-to-execute-r-scripts"></a>Como executar scripts do R

Há duas maneiras de executar scripts do R no R Services:

+ A maneira mais comum é usar o procedimento armazenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) do T-SQL.

+ Você também pode usar seu cliente R preferencial e gravar scripts que efetuam push da execução (chamada de *contexto de computação remota*) para um SQL Server remoto. Veja como [configurar um desenvolvimento em R cliente de ciência de dados](../r/set-up-a-data-science-client.md) para obter mais informações.

<a name="version"></a>

## <a name="r-version"></a>Versão do R

A versão R 3.2.2 está incluída no R Services do SQL Server 2016. Para as versões mais recentes de R, use os [Serviços de Machine Learning para SQL Server 2017 e posterior](../what-is-sql-server-machine-learning.md).

<a name="packages"></a>

## <a name="r-packages"></a>Pacotes R

Você pode usar pacotes e estruturas de software livre, além dos pacotes corporativos da Microsoft. Os pacotes do R de software livre mais comuns são pré-instalados no R Services. Os seguintes pacotes do R da Microsoft também estão incluídos:

| Pacote | Descrição |
|-|-|
| [RevoScaleR](../r/ref-r-revoscaler.md) | O pacote primário para R escalonável. Transformações e manipulação de dados, resumo estatístico, visualização e muitas formas de modelagem. Além disso, as funções nesse pacote distribuem automaticamente as cargas de trabalho entre os núcleos disponíveis para processamento paralelo. |
| [MicrosoftML (R)](../r/ref-r-microsoftml.md) | Adiciona algoritmos de aprendizado de máquina para criar modelos personalizados para análise de texto, análise de imagem e análise de sentimentos. |
| [olapR](../r/ref-r-olapr.md) | As funções do R usadas para consultas MDX em um cubo OLAP do SQL Server Analysis Services. |
| [sqlrutils](../r/ref-r-sqlrutils.md) | Um mecanismo para usar scripts do R em um procedimento armazenado do T-SQL, registrar esse procedimento armazenado em um banco de dados e executar procedimento armazenado em um [ambiente de desenvolvimento em R](../r/set-up-a-data-science-client.md). |
| [Microsoft R Open](https://mran.microsoft.com/rro) | O MRO (Microsoft R Open) é a distribuição aprimorada do R da Microsoft. É uma plataforma de software livre completa para análise estatística e ciência de dados. Ela é baseada e totalmente compatível com o R e inclui recursos adicionais para melhorar o desempenho e a capacidade de reprodução. |

## <a name="how-do-i-get-started-with-rservices"></a>Como posso começar a usar o R Services?

1. [Instalar o SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)

1. Configurar suas ferramentas de desenvolvimento. Você pode usar:

    + [Azure Data Studio](../../azure-data-studio/what-is.md) ou [SSMS (SQL Server Management Studio)](../../ssms/sql-server-management-studio-ssms.md) para usar o T-SQL e o procedimento armazenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para executar o script do R.
    + R em seu próprio laptop de desenvolvimento ou estação de trabalho para executar scripts. Você pode efetuar pull de dados localmente ou efetuar push da execução remotamente para o SQL Server com o [RevoScaleR](../r/ref-r-revoscaler.md). Veja como [configurar um desenvolvimento em R cliente de ciência de dados](../r/set-up-a-data-science-client.md) para obter mais informações.

1. Escrever seu primeiro script do R

    + Início Rápido: [Criar e executar scripts do R simples no SQL Server](../tutorials/quickstart-r-create-script.md)
    + Início Rápido: [Criar e treinar um modelo preditivo em R](../tutorials/quickstart-r-train-score-model.md)
    + Tutorial: [Usar o R no T-SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md): Explorar dados, executar engenharia de recursos, treinar e implantar modelos e fazer previsões (série de cinco partes)
    + Tutorial: [Usar o R Services em ferramentas do R](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md): Explorar dados, criar grafos e gráficos, executar engenharia de recursos, treinar e implantar modelos e fazer previsões (série de seis partes)

## <a name="next-steps"></a>Próximas etapas

+ [Instalar o SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [Configurar um cliente de ciência de dados para desenvolvimento em R](../r/set-up-a-data-science-client.md)