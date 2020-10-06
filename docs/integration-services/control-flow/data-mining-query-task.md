---
description: Data Mining Query Task
title: Tarefa Consulta de Mineração de Dados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataminingquerytask.f1
- sql13.dts.designer.dmquerytask.miningmodel.f1
- sql13.dts.designer.dmquerytask.query.f1
- sql13.dts.designer.dmquerytask.output.f1
helpviewer_keywords:
- prediction queries [Integration Services]
- Data Mining Query task [Integration Services]
ms.assetid: f489348c-2008-4f66-8c2c-c07c3029439a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1af5f497be96f5c8b9808878aea9e5275c77ddf7
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727568"
---
# <a name="data-mining-query-task"></a>Data Mining Query Task

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  A tarefa Consulta de Mineração de Dados executa consultas de previsão com base em modelos internos de mineração de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. A consulta de previsão cria uma previsão para novos dados usando modelos de mineração. Por exemplo, uma consulta de previsão pode prever quantos veleiros serão vendidos durante os meses de verão ou gerar uma lista de possíveis clientes para a compra de um veleiro.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece tarefas que desempenham outras operações de business intelligence, como executar instruções DDL (linguagem de definição de dados) e objetos de análise de processamento.  
  
 Para obter mais informações sobre outras tarefas de business intelligence, clique em um dos tópicos a seguir:  
  
-   [Tarefa Executar DDL do Analysis Services](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)  
  
-   [Tarefa Processamento do Analysis Services](../../integration-services/control-flow/analysis-services-processing-task.md)  
  
## <a name="prediction-queries"></a>Consultas de previsão  
 A consulta é uma instrução DMX (Data Mining Extensions). A linguagem DMX é uma extensão da linguagem SQL que fornece suporte ao trabalho com modelos de mineração. Para obter mais informações sobre como usar a linguagem DMX, consulte [Referência de extensões de Data Mining &#40;Extensão de Data Mining&#41;](../../dmx/data-mining-extensions-dmx-reference.md).  
  
 A tarefa pode consultar múltiplos modelos de mineração criados com a mesma estrutura de mineração. Um modelo de mineração é criado com um dos algoritmos de mineração de dados que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece. A estrutura de mineração a que a tarefa Consulta de Mineração de Dados faz referência pode incluir vários modelos de mineração, criados com algoritmos diferentes. Para obter mais informações, consulte [Estruturas de Mineração &#40;Analysis Services – Data Mining&#41;](/analysis-services/data-mining/mining-structures-analysis-services-data-mining) e [Algoritmos de Data Mining &#40;Analysis Services – Data Mining&#41;](/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining).  
  
 A consulta de previsão que a tarefa Consulta de Mineração de Dados executa retorna um resultado que é uma única linha ou um conjunto de dados. Uma consulta que retorna uma única linha é chamada consulta singleton: por exemplo, a consulta que prevê quantos veleiros serão vendidos durante os meses de verão retorna um número. Para obter mais informações sobre consultas de previsão que retornam uma única linha, consulte [Ferramentas de Consulta de Data Mining](/analysis-services/data-mining/data-mining-query-tools).  
  
 Os resultados da consulta são salvos nas tabelas. Se uma tabela com o nome que a tarefa Consulta de Mineração de Dados especifica já existir, a tarefa poderá criar uma nova tabela usando o mesmo nome com um número anexado ou poderá substituir o conteúdo da tabela.  
  
 Se os resultados incluírem aninhamento, o resultado será simplificado antes de ser salvo. A simplificação de um resultado altera um resultado aninhado definido para uma tabela. Por exemplo, simplificar um resultado aninhado com uma coluna **Cliente** e uma coluna aninhada **Produto** adiciona linhas à coluna **Cliente** para fazer uma tabela que inclui dados de produto para cada cliente. Por exemplo, um cliente com três produtos diferentes transforma-se em uma tabela com três linhas, repetindo o cliente em cada linha e incluindo um produto diferente em cada linha. Se a palavra-chave FLATTENED for omitida, a tabela conterá só a coluna **Cliente** e só uma linha por cliente. Para obter mais informações, consulte [SELECT &#40;DMX&#41;](../../dmx/select-dmx.md).  
  
## <a name="configuration-of-the-data-mining-query-task"></a>Configuração da tarefa Consulta de Mineração de Dados  
 A tarefa Consulta de Mineração de Dados requer duas conexões. A primeira conexão é um gerenciador de conexões do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se conecta a uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou a um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contém a estrutura de mineração e o modelo de mineração. A segunda conexão é um gerenciador de conexões OLE DB que se conecta ao banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contém a tabela na qual a tarefa é gravada. Para obter mais informações, consulte [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md) e [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
> [!NOTE]  
>  O Editor de Consultas de Mineração de Dados não tem nenhuma página Expressões. Em vez disso, use a janela **Propriedades** para acessar as ferramentas de criação e gerenciamento de expressões de propriedade para as propriedades da tarefa Consulta de Mineração de Dados.  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](./add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
## <a name="programmatic-configuration-of-data-mining-query-task"></a>Configuração programática da tarefa Consulta de Mineração de Dados  
 Para obter mais informações sobre como definir essas propriedades programaticamente, clique em um dos tópicos a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.DMQueryTask.DMQueryTask>  
  
## <a name="data-mining-query-task-editor-mining-model-tab"></a>Editor da Tarefa Consulta de Mineração de Dados (guia Modelo de Mineração)
  Use a guia **Modelo de Mineração** da caixa de diálogo **Tarefa Consulta de Mineração de Dados** para especificar a estrutura e o modelo de mineração a serem usados.  
  
 Para saber mais sobre como implementar a mineração de dados em pacotes, consulte [Tarefa Consulta de mineração de dados](../../integration-services/control-flow/data-mining-query-task.md) e [Soluções de mineração de dados](/analysis-services/data-mining/data-mining-solutions).  
  
### <a name="general-options"></a>Opções gerais  
 **Nome**  
 Forneça um nome exclusivo para a tarefa Consulta de Mineração de Dados. Esse nome é usado como rótulo no ícone de tarefa.  
  
> [!NOTE]  
>  Os nomes das tarefas devem ser exclusivos em um pacote.  
  
 **Descrição**  
 Digite uma descrição para a tarefa Consulta de Mineração de Dados.  
  
### <a name="mining-model-tab-options"></a>Opções da guia Modelo de Mineração  
 **Conexão**  
 Selecione um gerenciador de conexões do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] na lista, ou clique em **Novo** para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:**  [Gerenciador de conexões do Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md)  
  
 **Novo**  
 Crie um novo gerenciador de conexões do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 **Tópicos relacionados:** [Referência da interface do usuário da caixa de diálogo Adicionar Gerenciador de Conexões do Analysis Services](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 **Estrutura de mineração**  
 Selecione uma estrutura de mineração na lista.  
  
 **Modelos de mineração**  
 Selecione um modelo de mineração com base na estrutura de mineração selecionada.  

## <a name="data-mining-query-task-editor-query-tab"></a>Editor da Tarefa Consulta de Mineração de Dados (guia Consulta)
  Use a guia **Consulta** da caixa de diálogo **Tarefa Consulta de Mineração de Dados** para criar consultas de previsão baseadas em um modelo de mineração. Nessa caixa de diálogo, você também pode associar parâmetros e conjuntos de resultados a variáveis.  
  
 Para saber mais sobre como implementar a mineração de dados em pacotes, consulte [Tarefa Consulta de mineração de dados](../../integration-services/control-flow/data-mining-query-task.md) e [Soluções de mineração de dados](/analysis-services/data-mining/data-mining-solutions).  
  
### <a name="general-options"></a>Opções gerais  
 **Nome**  
 Forneça um nome exclusivo para a tarefa Consulta de Mineração de Dados. Esse nome é usado como rótulo no ícone de tarefa.  
  
> [!NOTE]  
>  Os nomes das tarefas devem ser exclusivos em um pacote.  
  
 **Descrição**  
 Digite uma descrição para a tarefa Consulta de Mineração de Dados.  
  
### <a name="build-query-tab-options"></a>Opções da guia Construir Consulta  
 **Consulta de mineração de dados**  
 Digite uma consulta de mineração de dados.  
  
 **Tópicos relacionados:**  [Referência de &#40;extensões DMX&#41;](../../dmx/data-mining-extensions-dmx-reference.md)  
  
 **Construir Nova Consulta**  
 Crie a consulta de mineração de dados usando uma ferramenta gráfica.  
  
 **Tópicos relacionados:** [Data Mining Query](../../integration-services/control-flow/data-mining-query.md)  
  
### <a name="parameter-mapping-tab-options"></a>Opções da guia Mapeamento de Parâmetros  
 **Nome do parâmetro**  
 Opcionalmente, atualize o nome de parâmetro. Mapeie o parâmetro para uma variável, selecionando uma variável na lista **Nome da Variável** .  
  
 **Nome da Variável**  
 Selecione uma variável na lista para mapeá-la para o parâmetro.  
  
 **Adicionar**  
 Adicione um parâmetro à lista.  
  
 **Remover**  
 Selecione um parâmetro e clique em **Remover**.  
  
### <a name="result-set-tab-options"></a>Opções da guia Conjunto de Resultados  
 **Nome do Resultado**  
 Opcionalmente, atualize o nome do conjunto de resultados. Mapeie o resultado para uma variável, selecionando uma variável na lista **Nome da Variável** .  
  
 Depois que você adicionar um resultado, clicando em **Adicionar**, forneça um nome exclusivo para o resultado.  
  
 **Nome da Variável**  
 Selecione uma variável na lista para mapeá-la para o conjunto de resultados.  
  
 **Tipo de Resultado**  
 Indique se deve ser retornada uma única linha ou um conjunto de resultados completo.  
  
 **Adicionar**  
 Adicione um conjunto de resultados à lista.  
  
 **Remover**  
 Selecione um resultado e clique em **Remover**.  
## <a name="data-mining-query-task-editor-output-tab"></a>Editor da Tarefa Consulta de Mineração de Dados (guia Saída)
  Use a guia **Saída** da caixa de diálogo **Editor da Tarefa Consulta de Mineração de Dados** para especificar o destino da consulta de previsão.  
  
 Para saber mais sobre como implementar a mineração de dados em pacotes, consulte [Tarefa Consulta de mineração de dados](../../integration-services/control-flow/data-mining-query-task.md) e [Soluções de mineração de dados](/analysis-services/data-mining/data-mining-solutions).  
  
### <a name="general-options"></a>Opções gerais  
 **Nome**  
 Forneça um nome exclusivo para a tarefa Consulta de Mineração de Dados. Esse nome é usado como rótulo no ícone de tarefa.  
  
> [!NOTE]  
>  Os nomes das tarefas devem ser exclusivos em um pacote.  
  
 **Descrição**  
 Digite uma descrição para a tarefa Consulta de Mineração de Dados.  
  
### <a name="output-tab-options"></a>Opções da guia Saída  
 **Conexão**  
 Selecione um gerenciador de conexões na lista ou clique em **Novo** para criar um novo gerenciador de conexões.  
  
 **Novo**  
 Crie um novo gerenciador de conexões. Só podem ser usados os tipos de gerenciador de conexões ADO.NET e OLE DB.  
  
 **Tabela de saída**  
 Especifique a tabela na qual a consulta de previsão deve gravar seus resultados.  
  
 **Ignorar e recriar tabela de saída**  
 Indique se a consulta de previsão deve substituir o conteúdo na tabela de destino, ignorando e, em seguida, recriando a tabela.  
