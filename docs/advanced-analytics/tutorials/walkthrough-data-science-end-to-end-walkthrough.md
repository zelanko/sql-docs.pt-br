---
title: "Passo a passo de ciência de dados de ponta a ponta para R e SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 08/22/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: edd76ae9-4125-45a8-bf42-47a85b9d9a32
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 9d6654109e3cb5ff2e2c174dc37fd02bfc02dcb3
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2017
---
# <a name="end-to-end-data-science-walkthrough-for-r-and-sql-server"></a>Passo a passo de ciência de dados de ponta a ponta para R e SQL Server

Neste passo a passo, você deve desenvolver uma solução de ponta a ponta para modelagem de previsão com base no Microsoft R com o SQL Server 2016 ou 2017 do SQL Server.

Este passo a passo baseia-se em um conjunto de dados público conhecido, o conjunto de dados de táxi de Nova York. Usar uma combinação de código R, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados e funções personalizadas do SQL para criar um modelo de classificação que indica a probabilidade de que o driver pode obter uma dica em uma viagem de táxi específico. Você também implantar o modelo de R para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e usar dados do servidor para gerar pontuações com base no modelo.

Este exemplo pode ser estendido para todos os tipos de problemas reais, como prever as respostas do cliente para campanhas de vendas ou prever gastos ou participação em eventos. Porque o modelo pode ser chamado de um procedimento armazenado, você pode inseri-lo facilmente em um aplicativo.

Como o passo a passo é projetada para apresentar os desenvolvedores de R [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], R é usado sempre que possível. No entanto, isso não significa que R é necessariamente a melhor ferramenta para cada tarefa. Em muitos casos, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderá fornecer um desempenho melhor, especialmente para tarefas como agregação de dados e engenharia de recursos.  Essas tarefas podem se beneficiar particularmente dos novos recursos do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], como índices columnstore com otimização de memória. Tentamos indicar possíveis otimizações ao longo do caminho.

> [!NOTE]
> O passo a passo foi originalmente desenvolvido para SQL Server 2016 e testado nele. No entanto, as capturas de tela e procedimentos foram atualizados para usar a versão mais recente do SQL Server Management Studio, que funciona com o SQL Server 2017.

## <a name="overview"></a>Visão geral

O estimado vezes não incluem a instalação. Para obter mais informações, consulte [pré-requisitos para o passo a passo](../tutorials/walkthrough-prerequisites-for-data-science-walkthroughs.md).

|Lista de tópicos|Tempo estimado|
|-|------------------------------|
|[Preparar os dados de instruções passo a passo de R](../tutorials/walkthrough-prepare-the-data.md) <br /><br />Obter os dados usados para criar um modelo. Baixe um conjunto de dados público e carregue-o em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|30 minutos|
|[Explorar os dados usando o SQL](../tutorials/walkthrough-view-and-explore-the-data.md) <br /><br />Compreenda os dados usando ferramentas SQL e resumos.|10 minutos|
|[Resumir os dados usando o R](../tutorials/walkthrough-view-and-summarize-data-using-r.md) <br /><br />Use o R para explorar os dados e gerar resumos.|10 minutos|
|[Criar gráficos usando o R no SQL Server](../tutorials/walkthrough-create-graphs-and-plots-using-r.md) <br /><br />Crie gráficos em contextos de computação local e remoto pela combinação de R e SQL.|10 minutos|
|[Criar recursos de dados usando R e T-SQL)](../tutorials/walkthrough-create-data-features.md) <br /><br />Execute a engenharia de recursos usando funções personalizadas no R e no [!INCLUDE[tsql](../../includes/tsql-md.md)]. Compare o desempenho de R e do T-SQL para tarefas de personalização. |10 minutos|
|[Criar um modelo de R e salvá-lo no SQL Server](../tutorials/walkthrough-build-and-save-the-model.md) <br /><br />Treine e ajuste um modelo preditivo. Avalie o desempenho do modelo. Este passo a passo cria um modelo de classificação. Plote a precisão do modelo usando o R.|15 minutos|
|[Implantar o modelo de R usando o SQL Server](../tutorials/walkthrough-deploy-and-use-the-model.md) <br /><br />Implante o modelo em produção, salvando-o em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Chame o modelo em um procedimento armazenado para gerar previsões.|10 minutos|

### <a name="intended-audience"></a>Público-alvo

Este passo a passo é destinado a desenvolvedores do R ou do SQL. Ele fornece uma introdução sobre como o R pode ser integrado em fluxos de trabalho empresariais usando [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].  Você deve estar familiarizado com as operações de banco de dados, como criação de tabelas e bancos de dados, a importação de dados e execução de consultas.

+ Todos os scripts SQL e R são incluídos.
+ Você precisará modificar cadeias de caracteres em scripts, para ser executado em seu ambiente. Você pode fazer isso com um editor de código, como [código do Visual Studio](https://code.visualstudio.com/Download).

### <a name="prerequisites"></a>Prerequisites

+ Você deve ter acesso a uma instância do SQL Server 2016 ou uma versão de avaliação do SQL Server 2017.
+ Pelo menos uma instância no computador do SQL Server deve ter o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] instalado.
+ Se você deseja executar comandos de R de um computador remoto, como um laptop ou outro computador na rede, você deve instalar as bibliotecas Microsoft R Open. Você pode instalar o cliente do Microsoft R ou Microsoft R Server. O computador remoto deve ser capaz de se conectar para a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância.
+ Se você precisa colocar o cliente e servidor no mesmo computador, certifique-se de instalar um conjunto separado de bibliotecas do Microsoft R para uso na enviando script R de um cliente "remoto". Não use as bibliotecas de R que estão instaladas para uso pela instância do SQL Server para essa finalidade.

Para obter detalhes sobre como configurar esses ambientes de servidor e cliente, consulte [pré-requisitos para explicação de ciência de dados R e SQL Server](../tutorials/walkthrough-prerequisites-for-data-science-walkthroughs.md).

## <a name="next-lesson"></a>Próxima lição

[Preparar os dados de instruções passo a passo de R](../tutorials/walkthrough-prepare-the-data.md)
