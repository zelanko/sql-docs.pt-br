---
title: R Services no SQL Server 2016 – serviços de aprendizado de máquina do SQL Server
description: R no SQL Server para tarefas de R integradas em dados relacionais, incluindo a ciência de dados e modelagem estatística, análise preditiva, visualização de dados e muito mais.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/10/2018
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: =sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: efc1b939f3231aeca18e0b6547970af6b8eb39cb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962422"
---
# <a name="r-services-in-sql-server-2016"></a>R Services no SQL Server 2016
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

R Services é um complemento para uma instância do mecanismo de banco de dados do SQL Server 2016, usado para executar código R e funções no SQL Server. Código é executado em uma estrutura de extensibilidade, isolados dos principais processos de mecanismo, mas totalmente disponíveis para dados relacionais, como procedimentos armazenados, como o script T-SQL que contém instruções de R ou como código R que contém o T-SQL. 

R Services inclui uma distribuição de base do R, sobreposta com os pacotes de R do enterprise da Microsoft para que você pode carregar e processar grandes quantidades de dados em vários núcleos e agregar os resultados em uma única saída consolidada. Funções de R e algoritmos da Microsoft são desenvolvidos para o dimensionamento e o utilitário: fornecimento de ponta algoritmos de machine learning em um produto de servidor comercial engenharia, modelagem estatística, visualizações de dados e análise preditiva e suporte da Microsoft. 

Incluem bibliotecas do R [ **RevoScaleR**](ref-r-revoscaler.md), [ **MicrosoftML (R)** ](ref-r-microsoftml.md)e outros. Como o R Services é integrado com o mecanismo de banco de dados, você pode manter a análise próxima aos dados e eliminar os custos e riscos de segurança associados à movimentação de dados.

> [!Note]
> R Services foi renomeado no SQL Server 2017 e posterior para [serviços do SQL Server Machine Learning](../what-is-sql-server-machine-learning.md), refletindo a adição do Python.

## <a name="components"></a>Componentes

SQL Server 2016 é apenas o R. A tabela a seguir descreve os recursos no SQL Server 2016.

| Componente | Descrição |
|-----------|-------------|
| Serviço do Launchpad do SQL Server | Um serviço que gerencia a comunicação entre os tempos de execução R externos e a instância do SQL Server. |
| Pacotes do R | [**RevoScaleR** ](ref-r-revoscaler.md) é a biblioteca principal para funções de R. escalonável nessa biblioteca estão entre mais amplamente usados. Transformações de dados e manipulação, resumo estatístico, visualização e muitas formas de modelagem e as análises são encontradas nessas bibliotecas. Além disso, funções nessas bibliotecas distribuir automaticamente as cargas de trabalho entre os núcleos disponíveis para processamento paralelo, com a capacidade de trabalhar em partes de dados que são coordenados e gerenciados pelo mecanismo de cálculo.  <br/>[**MicrosoftML (R)** ](ref-r-microsoftml.md) adiciona algoritmos de aprendizado de máquina para criar modelos personalizados para análise de sentimento, análise de imagem e análise de texto. <br/>[**sqlRUtils** ](ref-r-sqlrutils.md) fornece funções auxiliares para colocar os scripts do R em um procedimento armazenado T-SQL, registrando um procedimento armazenado com um banco de dados e executar o procedimento armazenado de um ambiente de desenvolvimento de R.<br/>[**olapR** ](ref-r-olapr.md) é para especificar consultas MDX em R.|
| Microsoft R Open MRO) | [**MRO** ](https://mran.microsoft.com/open) é a distribuição do código-fonte aberto da Microsoft do R. O pacote e o interpretador são incluídos. Sempre use a versão do MRO instalado pela instalação. |
| Ferramentas do R | Janelas do console de R e prompts de comando são ferramentas padrão em uma distribuição de R.  |
| Exemplos de R e scripts |  Pacotes de R e RevoScaleR do código-fonte aberto incluem conjuntos de dados internos para que você pode criar e executar o script usando os dados previamente instalados |
| Modelos previamente treinados em R | Modelos previamente treinados são criados para casos de uso específicos e mantidos pela equipe de engenharia de ciência de dados na Microsoft. Você pode usar os modelos previamente treinados como-é a pontuação de sentimento negativo positivo em texto ou detectar recursos em imagens usando as novas entradas de dados que você fornecer. Os modelos de execução nos serviços de R, mas não podem ser instalados pela instalação do SQL Server. Para obter mais informações, consulte [Install previamente treinado modelos de machine learning no SQL Server](../install/sql-pretrained-models-install.md). |

## <a name="using-r-services"></a>Usando o R Services

Analistas e desenvolvedores geralmente têm código em execução na parte superior de uma instância do SQL Server local. Adicionando serviços de Machine Learning e habilitar a execução do script externo, você ganha a capacidade de executar código R no modalidades de SQL Server: encapsular o script em procedimentos armazenados, armazenar modelos em uma tabela do SQL Server ou combinar as funções em consultas T-SQL e R.

A abordagem mais comum para análise no banco de dados é usar [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), passando o script R como um parâmetro de entrada.

Interações de cliente-servidor clássico são outra abordagem. De qualquer estação de trabalho cliente que tenha um IDE, você pode instalar [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)e, em seguida, escrever um código que envia por push de execução (conhecido como um *contexto de computação remota*) para dados e operações para um SQL remoto Servidor. 

Por fim, se você estiver usando um [servidor autônomo](r-server-standalone.md) e Developer edition, você pode criar soluções em uma estação de trabalho do cliente usando as mesmas bibliotecas e interpretadores e, em seguida, implantar o código de produção em aprendizado de máquina do SQL Server Serviços (no banco de dados). 

## <a name="how-to-get-started"></a>Como começar

Iniciar com a instalação, anexar os binários a ferramenta de desenvolvimento favorita e escrever seu primeiro script.

**Etapa 1:** Instalar e configurar o software. 

+ [Instalar o SQL Server 2016 R Services (no banco de dados)](../install/sql-r-services-windows-install.md)

**Etapa 2:** Obter experiência prática usando qualquer um destes tutoriais:

+ [Tutorial: Aprenda a análise no banco de dados usando o R](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [Tutorial: Instruções passo a passo de ponta a ponta com R](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

**Etapa 3:** Adicione seus pacotes de R favoritas e usá-los junto com pacotes fornecidos pela Microsoft

+ [Gerenciamento de pacotes de R para SQL Server](install-additional-r-packages-on-sql-server.md)


## <a name="see-also"></a>Confira também

 [Instalar o SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
