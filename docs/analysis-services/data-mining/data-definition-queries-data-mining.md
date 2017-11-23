---
title: "Consultas de definição de dados (mineração de dados) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 49e02de1-4ffa-401c-8eee-471a9c25b86a
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 04237bba7622a7b6745ff8768ea7a1bc5feda2b5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="data-definition-queries-data-mining"></a>Consultas de definição de dados (mineração de dados)
  Para mineração de dados, a categoria *consulta de definição de dados* significa instruções DMX ou comandos XMLA que fazem o seguinte:  
  
-   Criar, alterar ou manipular objetos de mineração de dados, como um modelo.  
  
-   Definir a origem dos dados a serem usados em treinamento ou para previsão.  
  
-   Exportar ou importar modelos de mineração e estruturas de mineração.  
  
 [Criando consultas de definição de dados](#bkmk_Create)  
  
-   [Consultas de definição de dados nas Ferramentas de Dados do SQL Server](#bkmk_ssdt)  
  
-   [Consultas de definição de dados no SQL Server Management Studio](#bkmk_SSMS)  
  
 [Instruções de definição de dados de script](#bkmk_Scripts)  
  
 [Instruções de definição de dados de script](#bkmk_Export)  
  
##  <a name="bkmk_Create"></a> Criando consultas de definição de dados  
 Você pode criar consultas de definição de dados (instruções) usando o Construtor de Consultas de Previsão no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ou usando a janela Consulta DMX no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. As instruções de definição de dados em DMX fazem parte da DDL (linguagem de definição de dados) do Analysis Services.  
  
 Para obter mais informações sobre a sintaxe de instruções de definição de dados específicos, consulte [Referência de &#40;extensões DMX&#41;](../../dmx/data-mining-extensions-dmx-reference.md).  
  
###  <a name="bkmk_ssdt"></a> Consultas de definição de dados nas Ferramentas de Dados do SQL Server  
 O Assistente de Mineração de Dados é a ferramenta preferida no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para criar e modificar modelos de mineração e estruturas de mineração, e para definir as fontes de dados que são usadas em consultas de previsão e para treinamento.  
  
 No entanto, se você quiser saber quais instruções estão sendo enviadas para o servidor pelo assistente para criar estruturas de dados ou modelos de mineração, você poderá usar o SQL Server Profiler para capturar as instruções de definição de dados. Para obter mais informações, consulte [Use SQL Server Profiler to Monitor Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md).  
  
 Para exibir as instruções usadas para definir fontes de dados usadas para treinamento ou previsão, use a **Exibição SQL** no Construtor de Consultas de Previsão. Muitas vezes ele pode ser útil parar criar consultas básicas para modelos de treinamento e teste usando o Construtor de Consultas de Previsão, para estabelecer a sintaxe correta. Você pode alternar para a **Exibição SQL** e editar a consulta manualmente. Para obter mais informações, consulte [Manually Edit a Prediction Query](../../analysis-services/data-mining/manually-edit-a-prediction-query.md).  
  
###  <a name="bkmk_SSMS"></a> Consultas de definição de dados no SQL Server Management Studio  
 Para objetos de mineração de dados, você pode usar as consultas de definição de dados para executar as seguintes ações:  
  
-   Criar tipos específicos de modelos, como um modelo de clustering ou modelo de árvore de decisão, usando [CREATE MINING MODEL &#40;DMX&#41;](../../dmx/create-mining-model-dmx.md).  
  
-   Alterar uma estrutura de mineração existente adicionando um modelo ou alterando as colunas, usando [ALTER MINING STRUCTURE &#40;DMX&#41;](../../dmx/alter-mining-structure-dmx.md). Observe que você não pode alterar um modelo de mineração usando DMX; você só pode adicionar novos modelos a uma estrutura existente.  
  
-   Faça uma cópia de um modelo de mineração e então altere-o, usando [SELECT INTO &#40;DMX&#41;](../../dmx/select-into-dmx.md).  
  
-   Defina o conjunto de dados usado para treinar um modelo, usando [INSERT INTO &#40;DMX&#41;](../../dmx/insert-into-dmx.md) junto com uma consulta de fonte de dados como OPENROWSET.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fornece modelos de consulta que podem ajudá-lo a criar consultas de definição de dados. Para obter mais informações, consulte [Usar modelos do Analysis Services no SQL Server Management Studio](../../analysis-services/instances/use-analysis-services-templates-in-sql-server-management-studio.md).  
  
 Em geral, os modelos que são fornecidos para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] contêm somente a definição de sintaxe geral que você deve personalizar, ou digitando na janela **Consulta** ou usando a caixa de diálogo fornecida para inserir parâmetros.  
  
 Para ver um exemplo de como inserir parâmetros usando a interface, consulte [Criar uma consulta de previsão Singleton com base em um modelo](../../analysis-services/data-mining/create-a-singleton-prediction-query-from-a-template.md).  
  
###  <a name="bkmk_Scripts"></a> Instruções de definição de dados de script  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece várias linguagens de script e programação que você pode usar para criar ou alterar objetos de mineração de dados ou para definir fontes de dados.  Embora o DMX seja criado para agilizar tarefas de mineração de dados, você também pode usar XMLA e AMO para manipular objetos em scripts ou em código personalizado.  
  
 O Suplemento de Mineração de Dados para o Excel também inclui muitos modelos de consulta e fornece o **Editor de Consulta Avançada**que ajuda a compor instruções DMX complexas. Você pode criar uma consulta interativamente e, em seguida, alterar para a Exibição SQL para capturar a instrução DMX.  
  
##  <a name="bkmk_Export"></a> Exportando e importando modelos  
 Você pode usar instruções de definição de dados no DMX para exportar a definição de um modelo e sua estrutura necessária e fontes de dados e, em seguida, importa essa definição em um servidor diferente. Usar exportação e importação é o modo mais rápido e mais fácil de mover modelos de mineração de dados e estruturas de mineração entre instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obter mais informações, consulte [Gerenciamento de soluções de mineração de dados e objetos](../../analysis-services/data-mining/management-of-data-mining-solutions-and-objects.md).  
  
> [!WARNING]  
>  Se seu modelo estiver baseado em dados de uma fonte de dados de cubo, você não poderá usar o DMX para exportar o modelo, e deve usar backup e restauração em vez disso.  
  
##  <a name="bkmk_Tasks"></a> Tarefas relacionadas  
 A tabela a seguir fornece links para tarefas que estão relacionadas a consultas de definição de dados.  
  
|||  
|-|-|  
|Trabalhar com modelos para consultas DMX.|[Usar modelos do Analysis Services no SQL Server Management Studio](../../analysis-services/instances/use-analysis-services-templates-in-sql-server-management-studio.md)|  
|Criar consultas de todos os tipos, usando Construtor de Consultas de Previsão.|[Criar uma consulta de previsão usando o construtor de consultas de previsão](../../analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)|  
|Capturar definições de consultas usando o SQL Server Profiler e usar rastreamento para monitorar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|[Use SQL Server Profiler to Monitor Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)|  
|Saiba mais sobre as linguagens de scripts e linguagens de programação fornecidas para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|[Referência de XML for Analysis &#40;XMLA&#41;](../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)<br /><br /> [Desenvolvendo com AMO &#40;Objetos de Gerenciamento de Análise&#41;](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)|  
|Saiba como gerenciar modelos no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].|[Exportar e importar objetos de mineração de dados](../../analysis-services/data-mining/export-and-import-data-mining-objects.md)<br /><br /> [EXPORT &#40;DMX&#41;](../../dmx/export-dmx.md)<br /><br /> [IMPORT &#40;DMX&#41;](../../dmx/import-dmx.md)|  
|Saiba mais sobre OPENROWSET e outros modos de consultar dados externos.|[&#60;consulta de dados de origem&#62;](../../dmx/source-data-query.md).|  
  
## <a name="see-also"></a>Consulte também  
 [Assistente de mineração de dados &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-wizard-analysis-services-data-mining.md)  
  
  
