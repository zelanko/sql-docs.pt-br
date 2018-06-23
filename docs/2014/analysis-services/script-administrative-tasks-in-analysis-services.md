---
title: Scripts a tarefas administrativas no Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- automatic Analysis Services administration
- administering Analysis Services
ms.assetid: 106415df-81ff-4ec3-b2e1-ca66324f4cab
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: f449636db50cdb64ba968e82dbd50c65798fa2ba
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009915"
---
# <a name="script-administrative-tasks-in-analysis-services"></a>Script de tarefas administrativas no Analysis Services
  Você pode automatizar tarefas administrativas do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] gravando ou gerando scripts que podem ser executados manualmente ou agendados pelo SQL Server Agent. A tabela a seguir resume as opções de script disponíveis para você e fornece links para mais informações.  
  
 Todas as metodologias listadas abaixo oferecem suporte a scripts que podem ser salvos a um arquivo e executados como uma operação independente. Como a linguagem DAX usada em modelos tabulares e pastas de trabalho PowerPivot não atende aos critérios, ela não está incluída na lista a seguir.  
  
|Metodologia|Formato do arquivo|Description|Links|  
|-----------------|-----------------|-----------------|-----------|  
|PowerShell|.ps1|O Analysis Services oferece suporte ao ambiente de script do SQL Server PowerShell por um novo provedor que agrega navegação em objetos da linha de comando, bem como novos cmdlets para tarefas administrativas como backup, restauração, processamento e gerenciamento de funções.<br /><br /> Além disso, o provedor do SQLPS (SQL Server PowerPivot) inclui um cmdlet de uso geral, `Invoke-ASCmd`, que permite executar arquivos de script XMLA, MDX ou DMX em uma sessão do PowerShell.<br /><br /> O script do Analysis Services PowerShell tem suporte para modelos multidimensionais e tabulares, mas não para pastas de trabalho PowerPivot acessadas no SharePoint.|[O Analysis Services PowerShell](analysis-services-powershell.md)<br /><br /> [Guia de sobrevivência do Windows PowerShell](http://go.microsoft.com/fwlink/?LinkId=233747)|  
|Script ASSL ou XMLA|.xmla|ASSL (Analysis Services Scripting Language) é uma extensão do XMLA que fornece acesso a dados de objetos e operações em uma instância do Analysis Services executada no modo tabular ou multidimensional. A linguagem ASSL inclui definição de dados e suporte de linguagem de comandos, permitindo que a expressão completa de objetos e operações do Analysis Services em um formato XML. Os scripts que usam os objetos e comandos fornecidos por ASSL são salvos como arquivos .xmla. Dentro do contexto do Analysis Services, é uma prática comum para recorrer à linguagem ASSL como script XMLA. Escolha esta abordagem quando seus requisitos incluírem o seguinte:<br /><br /> Seu script cria objetos diretamente em um servidor ou executa tarefas de definição de dados e operacionais (por exemplo, recriar e processar banco de dados).<br /><br /> Você requer reutilização máxima de script por várias ferramentas e tecnologias. Scripts XMLA podem ser adicionados a tarefas de comandos do Analysis Services no SQL Server Agent, referenciadas em pacotes do SSIS ou em scripts do PowerShell.<br /><br /> O script deve ser executado de forma independente. Você pode usar o SQL Server Agent para agendar um trabalho que contém script XMLA ou um pacote do SSIS que contém XMLA.<br /><br /> Você tem requisitos de aplicativo para usar XMLA. XMLA é uma interface que não requer um ambiente de código gerenciado. Você pode executar script XMLA em um aplicativo que não usa o .NET Framework.|[Criar Scripts do Analysis Services no Management Studio](instances/create-analysis-services-scripts-in-management-studio.md)<br /><br /> [Usar modelos do Analysis Services no SQL Server Management Studio](instances/use-analysis-services-templates-in-sql-server-management-studio.md)<br /><br /> [Agendar tarefas administrativas do SSAS com o SQL Server Agent](instances/schedule-ssas-administrative-tasks-with-sql-server-agent.md)<br /><br /> [Desenvolvimento com o Analysis Services Scripting Language &#40;ASSL&#41;](multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)<br /><br /> [Cmdlet Invoke-ASCmd](/sql/analysis-services/powershell/invoke-ascmd-cmdlet)|  
|||Para criar script XMLA, você pode usar o gerador de scripts no Management Studio. No nível de objeto, clique com o botão direito em um objeto para gerar um script que crie, altere ou exclua um objeto. No nível de comando, como para processar, fazer backup ou restaurar, design de agregação ou outro comando, você pode gerar script usando o recurso Script na caixa de diálogo, escolhendo opções que colocam o script em uma nova janela, arquivo ou área de transferência. Você também pode gravar scripts XMLA manualmente em um editor de texto ou de códigos, ou usar um modelo do Gerenciador de Modelos. Para executar o script, use uma destas abordagens:<br /><br /> Use o Management Studio para criar ou modificar diretamente objetos em uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].<br /><br /> Use o SQL Server Agent para agendar um trabalho que inclui uma tarefa de comando do Analysis Services.<br /><br /> Use o cmdlet Invoke-ASCmd para executar o script em uma sessão do PowerShell.||  
|MDX Script|.mdx|MDX é uma linguagem de consulta padrão do setor para fontes de dados analíticos que também faz parte da especificação de XMLA.<br /><br /> Você pode criar um arquivo de script MDX autônomo que consulte dados ou informações do sistema. Por exemplo, as exibições DMV (exibição de gerenciamento dinâmico) que expõem informações sobre as operações do servidor local e a integridade do servidor são acessadas por meio da instrução MDX Select.<br /><br /> O script MDX será executado em servidores no modo multidimensional e tabular. Você pode executar o script interativamente no SQL Server Management Studio ou em uma sessão do PowerShell usando `Invoke-ASCmd`.|[Conceitos básicos de script MDX &#40;do Analysis Services&#41;](multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)<br /><br /> [Usar exibições de gerenciamento dinâmico &#40;DMVs&#41; monitorar o Analysis Services](instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)<br /><br /> [Usar modelos do Analysis Services no SQL Server Management Studio](instances/use-analysis-services-templates-in-sql-server-management-studio.md)|  
|DMX Script|.dmx|DMX é uma linguagem de definição, manipulação e consulta de dados para modelos de mineração de dados. Você pode usar um modelo como ponto de partida.|[Criar uma consulta DMX no SQL Server Management Studio](data-mining/create-a-dmx-query-in-sql-server-management-studio.md)<br /><br /> [Usar modelos do Analysis Services no SQL Server Management Studio](instances/use-analysis-services-templates-in-sql-server-management-studio.md)|  
|[!INCLUDE[ssIS](../includes/ssis-md.md)] pacotes|.dtsx|[!INCLUDE[ssIS](../includes/ssis-md.md)] fornece tarefas e fluxos de dados que criarem, modificar, excluam e processam objetos do Analysis Services, incluindo modelos de mineração de dados. Você pode agendar um pacote para ser executado usando o SQL Server Agent.|[Tarefa Executar DDL do Analysis Services](../integration-services/control-flow/analysis-services-execute-ddl-task.md)<br /><br /> [Tarefa Processamento do Analysis Services](../integration-services/control-flow/analysis-services-processing-task.md)<br /><br /> [Tarefa Consulta de Mineração de Dados](../integration-services/control-flow/data-mining-query-task.md)<br /><br /> [Destino de treinamento do modelo de mineração de dados](../integration-services/data-flow/data-mining-model-training-destination.md)<br /><br /> [Destino de processamento de dimensões](../integration-services/data-flow/dimension-processing-destination.md)<br /><br /> [Destino de processamento de partições](../integration-services/data-flow/partition-processing-destination.md)|  
|Objetos de Gerenciamento de Análise||AMO (Objetos de Gerenciamento de Análise) é uma interface gerenciada que os programadores podem usar para desenvolver aplicativos personalizados que automatizam operações administrativas. Usando o AMO, você pode desenvolver um aplicativo personalizado que executa scripts XMLA, MDX ou DMX fornecidos.|[Programando tarefas administrativas com AMO](multidimensional-models/analysis-management-objects/programming-administrative-tasks-with-amo.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Linguagem de script do Analysis Services &#40;ASSL&#41; referência](scripting/analysis-services-scripting-language-assl-for-xmla.md)   
 [Desenvolvendo com objetos de gerenciamento de análise &#40;AMO&#41;](multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)   
 [Processamento de objetos de modelo multidimensional](multidimensional-models/processing-a-multidimensional-model-analysis-services.md)  
  
  
