---
title: Tarefa Consulta de Mineração de Dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataminingquerytask.f1
helpviewer_keywords:
- prediction queries [Integration Services]
- Data Mining Query task [Integration Services]
ms.assetid: f489348c-2008-4f66-8c2c-c07c3029439a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f11f2eac6d1d44ed361324f2b5e25cea80df8768
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68890405"
---
# <a name="data-mining-query-task"></a>Data Mining Query Task
  A tarefa Consulta de Mineração de Dados executa consultas de previsão com base em modelos internos de mineração de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. A consulta de previsão cria uma previsão para novos dados usando modelos de mineração. Por exemplo, uma consulta de previsão pode prever quantos veleiros serão vendidos durante os meses de verão ou gerar uma lista de possíveis clientes para a compra de um veleiro.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece tarefas que desempenham outras operações de business intelligence, como executar instruções DDL (linguagem de definição de dados) e objetos de análise de processamento.  
  
 Para obter mais informações sobre outras tarefas de business intelligence, clique em um dos tópicos a seguir:  
  
-   [Tarefa Executar DDL do Analysis Services](analysis-services-execute-ddl-task.md)  
  
-   [Tarefa Processamento do Analysis Services](analysis-services-processing-task.md)  
  
## <a name="prediction-queries"></a>Consultas de previsão  
 A consulta é uma instrução DMX (Data Mining Extensions). A linguagem DMX é uma extensão da linguagem SQL que fornece suporte ao trabalho com modelos de mineração. Para obter mais informações sobre como usar a linguagem DMX, consulte [Referência de extensões de Data Mining &#40;Extensão de Data Mining&#41;](/sql/dmx/data-mining-extensions-dmx-reference).  
  
 A tarefa pode consultar múltiplos modelos de mineração criados com a mesma estrutura de mineração. Um modelo de mineração é criado com um dos algoritmos de mineração de dados que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece. A estrutura de mineração a que a tarefa Consulta de Mineração de Dados faz referência pode incluir vários modelos de mineração, criados com algoritmos diferentes. Para obter mais informações, consulte [Estruturas de Mineração &#40;Analysis Services – Data Mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/mining-structures-analysis-services-data-mining) e [Algoritmos de Data Mining &#40;Analysis Services – Data Mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining).  
  
 A consulta de previsão que a tarefa Consulta de Mineração de Dados executa retorna um resultado que é uma única linha ou um conjunto de dados. Uma consulta que retorna uma única linha é chamada consulta singleton: por exemplo, a consulta que prevê quantos veleiros serão vendidos durante os meses de verão retorna um número. Para obter mais informações sobre consultas de previsão que retornam uma única linha, consulte [interfaces de consulta de mineração de dados](https://docs.microsoft.com/analysis-services/data-mining/data-mining-query-tools).  
  
 Os resultados da consulta são salvos nas tabelas. Se uma tabela com o nome que a tarefa Consulta de Mineração de Dados especifica já existir, a tarefa poderá criar uma nova tabela usando o mesmo nome com um número anexado ou poderá substituir o conteúdo da tabela.  
  
 Se os resultados incluírem aninhamento, o resultado será simplificado antes de ser salvo. A simplificação de um resultado altera um resultado aninhado definido para uma tabela. Por exemplo, simplificar um resultado aninhado com uma coluna **Cliente** e uma coluna aninhada **Produto** adiciona linhas à coluna **Cliente** para fazer uma tabela que inclui dados de produto para cada cliente. Por exemplo, um cliente com três produtos diferentes transforma-se em uma tabela com três linhas, repetindo o cliente em cada linha e incluindo um produto diferente em cada linha. Se a palavra-chave FLATTENED for omitida, a tabela conterá só a coluna **Cliente** e só uma linha por cliente. Para obter mais informações, consulte [SELECT &#40;DMX&#41;](/sql/dmx/select-dmx).  
  
## <a name="configuration-of-the-data-mining-query-task"></a>Configuração da tarefa Consulta de Mineração de Dados  
 A tarefa Consulta de Mineração de Dados requer duas conexões. A primeira conexão é um gerenciador de conexões do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se conecta a uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou a um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contém a estrutura de mineração e o modelo de mineração. A segunda conexão é um gerenciador de conexões OLE DB que se conecta ao banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que contém a tabela na qual a tarefa é gravada. Para obter mais informações, consulte [Analysis Services Connection Manager](../connection-manager/analysis-services-connection-manager.md) e [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md).  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer, clique em um dos seguintes tópicos:  
  
-   [Editor da Tarefa Consulta de Mineração de Dados &#40;Guia Modelo de Mineração&#41;](../data-mining-query-task-editor-mining-model-tab.md)  
  
-   [Editor da Tarefa Consulta de Mineração de Dados &#40;Guia Consulta&#41;](../data-mining-query-task-editor-query-tab.md)  
  
-   [Editor da Tarefa Consulta de Mineração de Dados &#40;Guia Saída&#41;](../data-mining-query-task-editor-output-tab.md)  
  
> [!NOTE]  
>  O Editor de Consultas de Mineração de Dados não tem nenhuma página Expressões. Em vez disso, use a janela **Propriedades** para acessar as ferramentas de criação e gerenciamento de expressões de propriedade para as propriedades da tarefa Consulta de Mineração de Dados.  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou de um contêiner](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-data-mining-query-task"></a>Configuração programática da tarefa Consulta de Mineração de Dados  
 Para obter mais informações sobre como definir essas propriedades programaticamente, clique em um dos tópicos a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.DMQueryTask.DMQueryTask>  
  
  
