---
title: Serviços de R no SQL Server 2016
description: R em SQL Server para tarefas de R integradas em dados relacionais, incluindo a ciência de dados e a modelagem estatística, análise preditiva, visualização de dados e muito mais.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/10/2018
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: =sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 32487d8c1a6c87c9ad916e4cfd517f9ba4cba6e2
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469903"
---
# <a name="r-services-in-sql-server-2016"></a>Serviços de R no SQL Server 2016
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O R Services é um complemento a uma instância do mecanismo de banco de dados SQL Server 2016, usada para executar o código R e as funções no SQL Server. O código é executado em uma estrutura de extensibilidade, isolada dos processos principais do mecanismo, mas totalmente disponível para dados relacionais como procedimentos armazenados, como um script T-SQL que contém instruções de R ou como código R que contém T-SQL. 

O r Services inclui uma distribuição básica de R, sobrepostas com pacotes de R Enterprise da Microsoft para que você possa carregar e processar grandes quantidades de dados em vários núcleos e agregar os resultados em uma única saída consolidada. As funções e os algoritmos do R da Microsoft são projetados para escala e utilitário: entrega de análise preditiva, modelagem estatística, visualizações de dados e algoritmos de aprendizado de máquina de ponta em um produto de servidor comercial projetado e com suporte da Microsoft. 

As bibliotecas do R incluem [**RevoScaleR**](ref-r-revoscaler.md), [**MicrosoftML (R)** ](ref-r-microsoftml.md)e outras. Como os serviços de R são integrados ao mecanismo de banco de dados, você pode manter a análise próxima ao dado e eliminar os custos e os riscos de segurança associados à movimentação de dados.

> [!Note]
> O R Services foi renomeado no SQL Server 2017 e posterior para [SQL Server serviços de Machine Learning](../what-is-sql-server-machine-learning.md), refletindo a adição do Python.

## <a name="components"></a>Componentes

SQL Server 2016 é somente R. A tabela a seguir descreve os recursos do SQL Server 2016.

| Componente | Descrição |
|-----------|-------------|
| Serviço de SQL Server Launchpad | Um serviço que gerencia as comunicações entre os tempos de execução externos do R e a instância de SQL Server. |
| Pacotes do R | [**RevoScaleR**](ref-r-revoscaler.md) é a biblioteca principal para R escalonáveis. as funções nessa biblioteca estão entre as mais amplamente usadas. Transformações e manipulação de dados, Resumo Estatístico, visualização e muitas formas de modelagem e análise são encontrados nessas bibliotecas. Além disso, as funções nessas bibliotecas distribuem automaticamente cargas de trabalho entre núcleos disponíveis para processamento paralelo, com a capacidade de trabalhar em partes de dados que são coordenadas e gerenciadas pelo mecanismo de cálculo.  <br/>O [**MicrosoftML (R)** ](ref-r-microsoftml.md) adiciona algoritmos de aprendizado de máquina para criar modelos personalizados para análise de texto, análise de imagem e análise de sentimentos. <br/>o [**sqlRUtils**](ref-r-sqlrutils.md) fornece funções auxiliares para colocar scripts R em um procedimento armazenado T-SQL, registrar um procedimento armazenado com um banco de dados e executar o procedimento armazenado de um ambiente de desenvolvimento de R.<br/>[**olapr**](ref-r-olapr.md) é para especificar consultas MDX em R.|
| Microsoft R Open (MRO) | [**MRO**](https://mran.microsoft.com/open) é a distribuição de R de código aberto da Microsoft. O pacote e o intérprete estão incluídos. Sempre use a versão do MRO instalada pela instalação. |
| Ferramentas de R | As janelas do console R e os prompts de comando são ferramentas padrão em uma distribuição do R.  |
| Scripts e exemplos de R |  Pacotes R e RevoScaleR de software livre incluem conjuntos de dados internos para que você possa criar e executar scripts usando dados pré-instalados |
| Modelos pré-treinados em R | Modelos pré-treinados são criados para casos de uso específicos e mantidos pela equipe de engenharia de ciência de dados na Microsoft. Você pode usar os modelos pré-treinados como estão para pontuar sentimentos positivos e negativos no texto ou detectar recursos em imagens, usando novas entradas de dados que você fornecer. Os modelos são executados no R Services, mas não podem ser instalados por meio da instalação do SQL Server. Para obter mais informações, consulte [instalar modelos de aprendizado de máquina pré-treinados em SQL Server](../install/sql-pretrained-models-install.md). |

## <a name="using-r-services"></a>Usando o R Services

Os desenvolvedores e analistas geralmente têm código em execução sobre uma instância de SQL Server local. Ao adicionar Serviços de Machine Learning e habilitar a execução de script externo, você obterá a capacidade de executar o código R em SQL Server modalidades: encapsulando o script em procedimentos armazenados, armazenando modelos em uma tabela SQL Server ou combinando funções T-SQL e R em consultas.

A abordagem mais comum para análise no banco de dados é usar o [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), passando o script R como um parâmetro de entrada.

As interações clássicas de cliente-servidor são outra abordagem. Em qualquer estação de trabalho cliente que tenha um IDE, você pode instalar [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)e, em seguida, escrever o código que envia a execução (conhecida como um *contexto de computação remota*) para dados e operações em um SQL Server remoto. 

Por fim, se você estiver usando um [servidor autônomo](r-server-standalone.md) e a edição Developer, poderá criar soluções em uma estação de trabalho cliente usando as mesmas bibliotecas e intérpretes e, em seguida, implantar o código de produção em SQL Server serviços de Machine Learning (no banco de dados). 

## <a name="how-to-get-started"></a>Como começar

Inicie a instalação, anexe os binários à sua ferramenta de desenvolvimento favorita e escreva seu primeiro script.

**Etapa 1:** Instale e configure o software. 

+ [Instalar o SQL Server R Services 2016 (no banco de dados)](../install/sql-r-services-windows-install.md)

**Etapa 2:** Tenha experiência prática usando um destes tutoriais:

+ [Tutorial: Aprenda sobre análise no banco de dados usando o R](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [Tutorial: Instruções completas de ponta a ponta com R](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

**Etapa 3:** Adicione seus pacotes de R favoritos e use-os junto com os pacotes fornecidos pela Microsoft

+ [Gerenciamento de pacotes R para SQL Server](install-additional-r-packages-on-sql-server.md)


## <a name="see-also"></a>Confira também

 [Instalar o SQL Server R Services 2016](../install/sql-r-services-windows-install.md)
