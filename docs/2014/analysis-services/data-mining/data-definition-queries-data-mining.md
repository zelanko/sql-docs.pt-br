---
title: Consultas de definição de dados (mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 49e02de1-4ffa-401c-8eee-471a9c25b86a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9a67cadab4ee67bb3f81776ccb658c66fe6a67d9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66085157"
---
# <a name="data-definition-queries-data-mining"></a>Consultas de definição de dados (mineração de dados)
  Para mineração de dados, a categoria *consulta de definição de dados* significa instruções DMX ou comandos XMLA que fazem o seguinte:  
  
-   Criar, alterar ou manipular objetos de mineração de dados, como um modelo.  
  
-   Definir a origem dos dados a serem usados em treinamento ou para previsão.  
  
-   Exportar ou importar modelos de mineração e estruturas de mineração.  
  
 [Criando consultas de definição de dados](#bkmk_Create)  
  
-   [Consultas de definição de dados no SQL Server Data Tools](#bkmk_ssdt)  
  
-   [Consultas de definição de dados no SQL Server Management Studio](#bkmk_SSMS)  
  
 [Instruções de definição de dados de script](#bkmk_Scripts)  
  
 [Instruções de definição de dados de script](#bkmk_Export)  
  
##  <a name="bkmk_Create"></a>Criando consultas de definição de dados  
 Você pode criar consultas de definição de dados (instruções) usando o Construtor de Consultas de Previsão no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ou usando a janela Consulta DMX no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. As instruções de definição de dados em DMX fazem parte da DDL (linguagem de definição de dados) do Analysis Services.  
  
 Para obter mais informações sobre a sintaxe de instruções de definição de dados específicos, consulte [Referência de &#40;extensões DMX&#41;](/sql/dmx/data-mining-extensions-dmx-reference).  
  
###  <a name="bkmk_ssdt"></a>Consultas de definição de dados no SQL Server Data Tools  
 O Assistente de Mineração de Dados é a ferramenta preferida no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para criar e modificar modelos de mineração e estruturas de mineração, e para definir as fontes de dados que são usadas em consultas de previsão e para treinamento.  
  
 No entanto, se você quiser saber quais instruções estão sendo enviadas para o servidor pelo assistente para criar estruturas de dados ou modelos de mineração, você poderá usar o SQL Server Profiler para capturar as instruções de definição de dados. Para obter mais informações, consulte [Use SQL Server Profiler to Monitor Analysis Services](../instances/use-sql-server-profiler-to-monitor-analysis-services.md).  
  
 Para exibir as instruções usadas para definir fontes de dados usadas para treinamento ou previsão, use a **Exibição SQL** no Construtor de Consultas de Previsão. Muitas vezes ele pode ser útil parar criar consultas básicas para modelos de treinamento e teste usando o Construtor de Consultas de Previsão, para estabelecer a sintaxe correta. Você pode alternar para a **Exibição SQL** e editar a consulta manualmente. Para obter mais informações, consulte [Manually Edit a Prediction Query](manually-edit-a-prediction-query.md).  
  
###  <a name="bkmk_SSMS"></a>Consultas de definição de dados no SQL Server Management Studio  
 Para objetos de mineração de dados, você pode usar as consultas de definição de dados para executar as seguintes ações:  
  
-   Criar tipos específicos de modelos, como um modelo de clustering ou modelo de árvore de decisão, usando [CREATE MINING MODEL &#40;DMX&#41;](/sql/dmx/create-mining-model-dmx).  
  
-   Alterar uma estrutura de mineração existente adicionando um modelo ou alterando as colunas, usando [ALTER MINING STRUCTURE &#40;DMX&#41;](/sql/dmx/alter-mining-structure-dmx). Observe que você não pode alterar um modelo de mineração usando DMX; você só pode adicionar novos modelos a uma estrutura existente.  
  
-   Faça uma cópia de um modelo de mineração e então altere-o, usando [SELECT INTO &#40;DMX&#41;](/sql/dmx/select-into-dmx).  
  
-   Defina o conjunto de dados usado para treinar um modelo, usando [INSERT INTO &#40;DMX&#41;](/sql/dmx/insert-into-dmx) junto com uma consulta de fonte de dados como OPENROWSET.  
  
 
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fornece modelos de consulta que podem ajudá-lo a criar consultas de definição de dados. Para obter mais informações, consulte [Usar modelos do Analysis Services no SQL Server Management Studio](../instances/use-analysis-services-templates-in-sql-server-management-studio.md).  
  
 Em geral, os modelos que são fornecidos para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] contêm somente a definição de sintaxe geral que você deve personalizar, ou digitando na janela **Consulta** ou usando a caixa de diálogo fornecida para inserir parâmetros.  
  
 Para ver um exemplo de como inserir parâmetros usando a interface, consulte [Criar uma consulta de previsão Singleton com base em um modelo](create-a-singleton-prediction-query-from-a-template.md).  
  
###  <a name="bkmk_Scripts"></a>Instruções de definição de dados de script  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece várias linguagens de script e programação que você pode usar para criar ou alterar objetos de mineração de dados ou para definir fontes de dados.  Embora o DMX seja criado para agilizar tarefas de mineração de dados, você também pode usar XMLA e AMO para manipular objetos em scripts ou em código personalizado.  
  
 O Suplemento de Mineração de Dados para o Excel também inclui muitos modelos de consulta e fornece o **Editor de Consulta Avançada**que ajuda a compor instruções DMX complexas. Você pode criar uma consulta interativamente e, em seguida, alterar para a Exibição SQL para capturar a instrução DMX.  
  
##  <a name="bkmk_Export"></a>Exportando e importando modelos  
 Você pode usar instruções de definição de dados no DMX para exportar a definição de um modelo e sua estrutura necessária e fontes de dados e, em seguida, importa essa definição em um servidor diferente. Usar exportação e importação é o modo mais rápido e mais fácil de mover modelos de mineração de dados e estruturas de mineração entre instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obter mais informações, consulte [Gerenciamento de soluções e objetos de mineração de dados](management-of-data-mining-solutions-and-objects.md).  
  
> [!WARNING]  
>  Se seu modelo estiver baseado em dados de uma fonte de dados de cubo, você não poderá usar o DMX para exportar o modelo, e deve usar backup e restauração em vez disso.  
  
##  <a name="bkmk_Tasks"></a> Tarefas relacionadas  
 A tabela a seguir fornece links para tarefas que estão relacionadas a consultas de definição de dados.  
  
|||  
|-|-|  
|Trabalhar com modelos para consultas DMX.|[Usar modelos do Analysis Services no SQL Server Management Studio](../instances/use-analysis-services-templates-in-sql-server-management-studio.md)|  
|Criar consultas de todos os tipos, usando Construtor de Consultas de Previsão.|[Criar uma consulta de previsão usando o construtor de consultas de previsão](create-a-prediction-query-using-the-prediction-query-builder.md)|  
|Capturar definições de consultas usando o SQL Server Profiler e usar rastreamento para monitorar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|[Use SQL Server Profiler to Monitor Analysis Services](../instances/use-sql-server-profiler-to-monitor-analysis-services.md)|  
|Saiba mais sobre as linguagens de scripts e linguagens de programação fornecidas para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|[XML for Analysis &#40;referência de&#41; XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-xmla-reference)<br /><br /> [Desenvolvendo com Objetos de Gerenciamento de Análise &#40;AMO&#41;](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)|  
|Saiba como gerenciar modelos no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].|[Exportar e importar objetos de mineração de dados](export-and-import-data-mining-objects.md)<br /><br /> [EXPORTAR &#40;DMX&#41;](/sql/dmx/export-dmx)<br /><br /> [IMPORTAR &#40;&#41;DMX](/sql/dmx/import-dmx)|  
|Saiba mais sobre OPENROWSET e outros modos de consultar dados externos.|[&#62;de consulta de dados de origem&#60;](/sql/dmx/source-data-query).|  
  
## <a name="see-also"></a>Consulte Também  
 [Assistente de mineração de dados &#40;Analysis Services Data Mining&#41;](data-mining-wizard-analysis-services-data-mining.md)  
  
  
