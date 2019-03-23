---
title: Tarefa Processamento do Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.asprocessingtask.f1
helpviewer_keywords:
- Analysis Services Processing task
- processing objects [Integration Services]
ms.assetid: e5748836-b4ce-4e17-ab6b-617a336f02f4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 02023482a2f3537872b50ac70f8bfd68d2128e1b
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58379124"
---
# <a name="analysis-services-processing-task"></a>Tarefa Processamento do Analysis Services
  A tarefa Processamento do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] processa objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , como modelos tabulares, cubos, dimensões e modelos de mineração.  
  
 Lembre-se do seguinte quando for processar modelos tabulares:  
  
-   Você não pode executar a análise de impacto em modelos tabulares.  
  
-   Algumas opções de processamento para modo tabular não são expostas, como Processar Desfragmentação e Processar Recálculo. Você pode executar essas funções usando a tarefa Executar DDL.  
  
-   As opções Índice de Processo e Atualização de Processo não são apropriadas para modelos tabulares e não devem ser usadas.  
  
-   As configurações de lote para modelos tabulares são ignoradas.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui diversas tarefas que desempenham operações de business intelligence, como execução de instruções DDL (linguagem de definição de dados) e consultas de previsão de mineração de dados. Para obter mais informações sobre tarefas de business intelligence relacionadas, clique em um dos tópicos a seguir:  
  
-   [Tarefa Executar DDL do Analysis Services](analysis-services-execute-ddl-task.md)  
  
-   [Tarefa Consulta de Mineração de Dados](data-mining-query-task.md)  
  
## <a name="object-processing"></a>Processamento de objetos  
 É possível processar vários objetos ao mesmo tempo. Ao processar vários objetos, você define configurações que se aplicam ao processamento de todos os objetos no lote.  
  
 Os objetos de um lote podem ser processados em sequência ou em paralelo. Se o lote não contiver objetos para os quais a sequência de processamento seja importante, o processamento paralelo poderá acelerar o processamento. Se objetos no lote forem processados em paralelo, você poderá configurar a tarefa para deixá-la determinar o número de objetos a serem processados em paralelo ou pode especificar manualmente o número de objetos a ser processado ao mesmo tempo. Se os objetos forem processados em sequência, será possível definir um atributo de transação no lote inscrevendo todos os objetos em uma transação, ou usando uma transação separada para cada objeto do lote.  
  
 Quando você processa objetos analíticos, também convém processar os objetos que dependem deles. A tarefa Processamento do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] inclui uma opção para processar qualquer objeto dependente além dos objetos selecionados.  
  
 Em geral, você processa tabelas de dimensões antes de processar tabelas de fatos. Você poderá encontrar erros se tentar processar tabelas de fatos antes de processar as tabelas de dimensões.  
  
 Essa tarefa também permite configurar a manipulação de erros em chaves de dimensão. Por exemplo, a tarefa pode ignorar erros ou pode parar depois da ocorrência de um determinado número de erros. A tarefa pode usar a configuração de erro padrão, ou você pode construir uma configuração de erro personalizada. Na configuração de erro personalizada, você especifica como a tarefa controla erros e as condições de erro. Por exemplo, você pode especificar se a tarefa deve parar de executar quando ocorrer o quarto erro, ou pode especificar como a tarefa deve controlar valores chave **Nulos** . A configuração de erro personalizada também pode incluir o caminho de um log de erros.  
  
> [!NOTE]  
>  A tarefa Processamento do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] só pode processar objetos analíticos criados pelas ferramentas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Essa tarefa é frequentemente usada em combinação com uma tarefa Inserção em Massa que carrega dados em uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou uma tarefa de Fluxo de Dados que implementa um fluxo de dados que carrega dados em uma tabela. Por exemplo, a tarefa de Fluxo de Dados pode ter um fluxo de dados que extrai dados de um banco de dados OLTP (Online Transactional Database) e o carrega em uma tabela de fatos do data warehouse, após o qual a tarefa Processamento do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é chamada para processar o cubo criado no data warehouse.  
  
 A tarefa Processamento do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa um gerenciador de conexões [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para se conectar a uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obter mais informações, consulte [Analysis Services Connection Manager](../connection-manager/analysis-services-connection-manager.md).  
  
## <a name="error-handling"></a>Tratamento de erros  
  
## <a name="configuration-of-the-analysis-services-processing-task"></a>Configuração da tarefa Processamento do Analysis Services  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos seguintes tópicos:  
  
-   [Editor da Tarefa Processamento do Analysis Services &#40;Página Geral&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor da Tarefa Processamento do Analysis Services &#40;Página Analysis Services&#41;](../analysis-services-processing-task-editor-analysis-services-page.md)  
  
-   [Página Expressões](../expressions/expressions-page.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-analysis-services-processing-task"></a>Configuração programática da tarefa Processamento do Analysis Services  
 Para obter mais informações sobre como definir essas propriedades programaticamente, clique em um dos tópicos a seguir:  
  
-   <xref:Microsoft.DataTransformationServices.Tasks.DTSProcessingTask.DTSProcessingTask>  
  
  
