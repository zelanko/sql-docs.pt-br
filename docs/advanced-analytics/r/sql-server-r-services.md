---
title: O que é SQL Server R Services 2016?
titleSuffix: ''
description: O R Services é um recurso do SQL Server 2016 que oferece a capacidade de executar scripts do R com dados relacionais. Você pode usar pacotes e estruturas de software livre e os pacotes do Microsoft R para análise preditiva e aprendizado de máquina. Os scripts são executados no banco de dados sem mover dados para fora do SQL Server ou pela rede. Este artigo explica os conceitos básicos do SQL Server R Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/12/2019
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: =sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 973c09be9cff6e66043b056e1a772ab8974cebb4
ms.sourcegitcommit: 12b7e3447ca2154ec2782fddcf207b903f82c2c0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/12/2019
ms.locfileid: "68957486"
---
# <a name="what-is-sql-server-2016-r-services"></a>O que é SQL Server R Services 2016?
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O R Services é um recurso do SQL Server 2016 que oferece a capacidade de executar scripts do R com dados relacionais. Você pode usar pacotes e estruturas de software livre e os pacotes do [Microsoft R](#packages) para análise preditiva e aprendizado de máquina. Os scripts são executados no banco de dados sem mover dados para fora do SQL Server ou pela rede. Este artigo explica os conceitos básicos do SQL Server R Services.

> [!Note]
> O R Services foi renomeado para [serviços de Machine Learning](../what-is-sql-server-machine-learning.md) no SQL Server 2017 e posterior e dá suporte ao Python e ao R.

## <a name="what-is-r-services"></a>O que são os Serviços R?

SQL Server R Services permite executar scripts R no banco de dados. Você pode usá-lo para preparar e limpar dados, fazer engenharia de recursos e treinar, avaliar e implantar modelos de aprendizado de máquina em um banco de dados. O recurso executa seus scripts onde os dados residem e elimina a transferência dos dados pela rede para outro servidor.

As distribuições base do R são incluídas no R Services. Você pode usar pacotes e estruturas de software livre além dos pacotes Microsoft [RevoScaleR](../r/ref-r-revoscaler.md), [MicrosoftML](../r/ref-r-microsoftml.md), [olapr].. /r/ref-r-olapr.MD) e [sqlrutils](../r/ref-r-sqlrutils.md) para r.

O R Services usa uma estrutura de extensibilidade para executar scripts R no SQL Server. Saiba mais sobre como isso funciona:

+ [Estrutura de extensibilidade](../concepts/extensibility-framework.md)
+ [Extensão de R](../concepts/extension-r.md)

## <a name="what-can-i-do-with-r-services"></a>O que posso fazer com o R Services?

Você pode usar o R Services para criar e treinar o aprendizado de máquina e modelos de aprendizado profundo dentro de SQL Server. Você também pode implantar modelos existentes no R Services e usar dados relacionais para previsões.

Exemplos do tipo de previsões que você pode usar SQL Server R Services para, incluem:

|||
|-|-|
|Classificação/categorização|Dividir automaticamente os comentários do cliente em categorias positivas e negativas|
|Regressão/previsão de valores contínuos|Prever o preço de casas com base no tamanho e no local|
|Detecção de anomalias|Detectar transações bancárias fraudulentas |
|Recomendações|Sugira produtos que os compradores online podem querer comprar, com base em suas compras anteriores|

### <a name="how-to-execute-r-scripts"></a>Como executar scripts do R

Há duas maneiras de executar scripts R no R Services:

+ A maneira mais comum é usar o procedimento armazenado T-SQL [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

+ Você também pode usar seu cliente R preferencial e gravar scripts que enviam por push a execução (conhecida como um *contexto de computação remota*) para um SQL Server remoto. Consulte como [configurar um desenvolvimento de R para cliente de ciência de dados](../r/set-up-a-data-science-client.md) para obter mais informações.

<a name="packages"></a>

## <a name="r-packages"></a>Pacotes do R

Você pode usar pacotes e estruturas de software livre, além dos pacotes corporativos da Microsoft. Os pacotes de R de software livre mais comuns são pré-instalados no R Services. Os seguintes pacotes do R da Microsoft também estão incluídos:

| Pacote | Descrição |
|-|-|
| [RevoScaleR](../r/ref-r-revoscaler.md) | O pacote primário para transformações e manipulação de R. Data escalonáveis, Resumo Estatístico, visualização e muitas formas de modelagem. Além disso, as funções nesse pacote distribuem automaticamente as cargas de trabalho entre os núcleos disponíveis para processamento paralelo. |
| [MicrosoftML (R)](../r/ref-r-microsoftml.md) | Adiciona algoritmos de aprendizado de máquina para criar modelos personalizados para análise de texto, análise de imagem e análise de sentimentos. |
| [olapR](../r/ref-r-olapr.md) | Funções do R usadas para consultas MDX em um SQL Server Analysis Services cubo OLAP. |
| [sqlrutils](../r/ref-r-sqlrutils.md) | Um mecanismo para usar scripts R em um procedimento armazenado T-SQL, registrar esse procedimento armazenado em um banco de dados e executar o procedimento armazenado de um [ambiente de desenvolvimento de R](../r/set-up-a-data-science-client.md). |
| [Microsoft R Open](https://mran.microsoft.com/rro) | O Microsoft R Open (MRO) é a distribuição aprimorada do R da Microsoft. É uma plataforma de software livre completa para análise estatística e ciência de dados. Ele é baseado em e 100% compatível com o R e inclui recursos adicionais para melhorar o desempenho e o reprodução. |

## <a name="how-do-i-get-started-with-rservices"></a>Como fazer introdução ao RServices?

1. [Instalar o SQL Server R Services 2016](../install/sql-r-services-windows-install.md)

1. Configure suas ferramentas de desenvolvimento. Você pode usar:

    + [Azure Data Studio](../../azure-data-studio/what-is.md) ou [SQL Server Management Studio (SSMS)](../../ssms/sql-server-management-studio-ssms.md) para usar o T-SQL e o procedimento armazenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para executar o script do R.
    + R em seu próprio laptop de desenvolvimento ou estação de trabalho para executar scripts. Você pode efetuar pull de dados localmente ou enviar a execução remotamente para SQL Server com [RevoScaleR](../r/ref-r-revoscaler.md). Consulte como [configurar um desenvolvimento de R para cliente de ciência de dados](../r/set-up-a-data-science-client.md) para obter mais informações.

1. Escreva seu primeiro script R

    + Início Rápido: [Executar um script "Olá, mundo" em R](../tutorials/quickstart-r-run-using-tsql.md)
    + Início Rápido: [Criar um modelo preditivo em R](../tutorials/quickstart-r-create-predictive-model.md)
    + Tutorial: [Use o R no T-SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md): Explorar dados, executar a engenharia de recursos, treinar e implantar modelos e fazer previsões (série de cinco partes)
    + Tutorial: [Use r Services em ferramentas de r](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md): Explorar dados, criar gráficos e plotagens, executar a engenharia de recursos, treinar e implantar modelos e fazer previsões (série de seis partes)

## <a name="next-steps"></a>Próximas etapas

+ [Instalar o SQL Server R Services 2016](../install/sql-r-services-windows-install.md)
+ [Configurar um cliente de ciência de dados para desenvolvimento em R](../r/set-up-a-data-science-client.md)