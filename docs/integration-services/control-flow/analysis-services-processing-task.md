---
title: Tarefa Processamento do Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.asprocessingtask.f1
- sql13.dts.designer.asprocessingtask.general.f1
- sql13.dts.designer.asprocessingtask.as.f1
helpviewer_keywords:
- Analysis Services Processing task
- processing objects [Integration Services]
ms.assetid: e5748836-b4ce-4e17-ab6b-617a336f02f4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 92e0656fd3625f2b93a1e097d2f81291056d01cf
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71298465"
---
# <a name="analysis-services-processing-task"></a>Tarefa Processamento do Analysis Services

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  A tarefa Processamento do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] processa objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , como modelos tabulares, cubos, dimensões e modelos de mineração.  
  
 Lembre-se do seguinte quando for processar modelos tabulares:  
  
-   Você não pode executar a análise de impacto em modelos tabulares.  
  
-   Algumas opções de processamento para modo tabular não são expostas, como Processar Desfragmentação e Processar Recálculo. Você pode executar essas funções usando a tarefa Executar DDL.  
  
-   As opções Índice de Processo e Atualização de Processo não são apropriadas para modelos tabulares e não devem ser usadas.  
  
-   As configurações de lote para modelos tabulares são ignoradas.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui diversas tarefas que desempenham operações de business intelligence, como execução de instruções DDL (linguagem de definição de dados) e consultas de previsão de mineração de dados. Para obter mais informações sobre tarefas de business intelligence relacionadas, clique em um dos tópicos a seguir:  
  
-   [Tarefa Executar DDL do Analysis Services](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)  
  
-   [Tarefa Consulta de Mineração de Dados](../../integration-services/control-flow/data-mining-query-task.md)  
  
## <a name="object-processing"></a>Processamento de objetos  
 É possível processar vários objetos ao mesmo tempo. Ao processar vários objetos, você define configurações que se aplicam ao processamento de todos os objetos no lote.  
  
 Os objetos de um lote podem ser processados em sequência ou em paralelo. Se o lote não contiver objetos para os quais a sequência de processamento seja importante, o processamento paralelo poderá acelerar o processamento. Se objetos no lote forem processados em paralelo, você poderá configurar a tarefa para deixá-la determinar o número de objetos a serem processados em paralelo ou pode especificar manualmente o número de objetos a ser processado ao mesmo tempo. Se os objetos forem processados em sequência, será possível definir um atributo de transação no lote inscrevendo todos os objetos em uma transação, ou usando uma transação separada para cada objeto do lote.  
  
 Quando você processa objetos analíticos, também convém processar os objetos que dependem deles. A tarefa Processamento do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] inclui uma opção para processar qualquer objeto dependente além dos objetos selecionados.  
  
 Em geral, você processa tabelas de dimensões antes de processar tabelas de fatos. Você poderá encontrar erros se tentar processar tabelas de fatos antes de processar as tabelas de dimensões.  
  
 Essa tarefa também permite configurar a manipulação de erros em chaves de dimensão. Por exemplo, a tarefa pode ignorar erros ou pode parar depois da ocorrência de um determinado número de erros. A tarefa pode usar a configuração de erro padrão, ou você pode construir uma configuração de erro personalizada. Na configuração de erro personalizada, você especifica como a tarefa controla erros e as condições de erro. Por exemplo, você pode especificar se a tarefa deve parar de executar quando ocorrer o quarto erro, ou pode especificar como a tarefa deve controlar valores chave **Nulos** . A configuração de erro personalizada também pode incluir o caminho de um log de erros.  
  
> [!NOTE]  
>  A tarefa Processamento do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] só pode processar objetos analíticos criados pelas ferramentas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Essa tarefa é frequentemente usada em combinação com uma tarefa Inserção em Massa que carrega dados em uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou uma tarefa de Fluxo de Dados que implementa um fluxo de dados que carrega dados em uma tabela. Por exemplo, a tarefa de Fluxo de Dados pode ter um fluxo de dados que extrai dados de um banco de dados OLTP (Online Transactional Database) e o carrega em uma tabela de fatos do data warehouse, após o qual a tarefa Processamento do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é chamada para processar o cubo criado no data warehouse.  
  
 A tarefa Processamento do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa um gerenciador de conexões [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para se conectar a uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obter mais informações, consulte [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md).  
  
## <a name="error-handling"></a>Tratamento de erros  
  
## <a name="configuration-of-the-analysis-services-processing-task"></a>Configuração da tarefa Processamento do Analysis Services  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-analysis-services-processing-task"></a>Configuração programática da tarefa Processamento do Analysis Services  
 Para obter mais informações sobre como definir essas propriedades programaticamente, clique no tópico a seguir:  
  
-   <xref:Microsoft.DataTransformationServices.Tasks.DTSProcessingTask.DTSProcessingTask>  
  
## <a name="analysis-services-processing-task-editor-general-page"></a>Editor da Tarefa Processamento do Analysis Services (Página Geral)
  Use a página **Geral** da caixa de diálogo **Editor da Tarefa Processamento do Analysis Services** para nomear e descrever a tarefa Processamento do Analysis Service.  
  
### <a name="options"></a>Opções  
 **Nome**  
 Forneça um nome exclusivo para a tarefa Processamento do Analysis Services. Esse nome é usado como rótulo no ícone de tarefa.  
  
> [!NOTE]  
>  Os nomes das tarefas devem ser exclusivos em um pacote.  
  
 **Descrição**  
 Digite uma descrição da tarefa Processamento do Analysis Services.  
  
## <a name="analysis-services-processing-task-editor-analysis-services-page"></a>Editor da Tarefa Processamento do Analysis Services (página Analysis Services)
  Use a página **Analysis Services** da caixa de diálogo **Editor da Tarefa Processamento do Analysis Services** para especificar um gerenciador de conexões do Analysis Services, selecione os objetos analíticos a serem processados e defina as opções de processamento e manipulação de erros.  
  
 Lembre-se do seguinte quando for processar modelos tabulares:  
  
1.  Você não pode executar a análise de impacto em modelos tabulares.  
  
2.  Algumas opções de processamento para modo tabular não são expostas, como Processar Desfragmentação e Processar Recálculo. Você pode executar essas funções usando a tarefa Executar DDL.  
  
3.  Algumas opções de processamento fornecidas, como índices de processo, não são apropriadas para modelos tabulares e não devem ser usadas.  
  
4.  As configurações de lote para modelos tabulares são ignoradas.  
  
### <a name="options"></a>Opções  
 **Gerenciador de conexões do Analysis Services**  
 Selecione na lista um gerenciador de conexões do Analysis Services existente ou clique em **Novo** para criar um novo gerenciador de conexões.  
  
 **Novo**  
 Cria um novo gerenciador de conexões do Analysis Services  
  
 **Tópicos relacionados:** [Gerenciador de Conexão do Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md), [Referência da interface do usuário da caixa de diálogo Adicionar Gerenciador de Conexões do Analysis Services](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 **Lista de objetos**  
 |Propriedade|Descrição|  
|--------------|-----------------|  
|**Object Name**|Lista os nomes de objeto especificados.|  
|**Tipo**|Lista os tipos dos objetos especificados.|  
|**Opções de Processo**|Selecione uma opção de processamento na lista.<br /><br /> **Tópicos relacionados**: [Processando um modelo multidimensional &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services)|  
|**Configurações**|Lista configurações de processamento para os objetos especificados.|  
  
 **Adicionar**  
 Adicione à lista um objeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 **Remover**  
 Selecione um objeto e clique em **Excluir**.  
  
 **Análise de Impacto**  
 Execute uma análise de impacto no objeto selecionado.  
  
 **Tópicos relacionados:** [Caixa de diálogo Análise de Impacto &#40;Analysis Services - Dados Multidimensionais&#41;](https://msdn.microsoft.com/library/208268eb-4e14-44db-9c64-6f74b776adb6)  
  
 **Resumo de Configurações de Lote**  
 |Propriedade|Descrição|  
|--------------|-----------------|  
|**Ordem de processamento**|Especifica se os objetos são processados em sequência ou em um lote; se for usado o processamento paralelo, especifica o número de objetos a serem processados simultaneamente.|  
|**Modo de transação**|Especifica o modo da transação para processamento sequencial.|  
|**Erros de dimensão**|Especifica o comportamento da tarefa quando ocorrem erros.|  
|**Caminho do log de erros da chave de dimensão**|Especifica o caminho do arquivo no qual são feitos logs de erros.|  
|**Objetos afetados pelo processo**|Indica se também são processados objetos dependentes ou afetados.|  
  
 **Alterar Configurações**  
 Altere as opções de processamento e a manipulação de erros em chaves de dimensão.  
  
 **Tópicos relacionados:** [Caixa de diálogo Alterar Configurações &#40;Analysis Services – Dados Multidimensionais&#41;](https://msdn.microsoft.com/library/0041e042-d7ce-48f9-a690-a6dc65471ff3)  
  
