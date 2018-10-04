---
title: Gerenciamento de soluções de mineração de dados e objetos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], managing
- managing mining models
ms.assetid: 06fc61dd-925c-4347-8677-7046ee5d2f6f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ad59ce6f605c913e621d4d377ec3d48e8cbf2b7f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48164286"
---
# <a name="management-of-data-mining-solutions-and-objects"></a>Gerenciamento de soluções de mineração de dados e objetos
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] fornece ferramentas de cliente que você pode usar para gerenciar estruturas de mineração e modelos de mineração existentes. Esta seção descreve as operações de gerenciamento que você pode executar usando cada ambiente.  
  
 Além dessas ferramentas, você pode gerenciar objetos de mineração de dados programaticamente, usando AMO, ou usar outros clientes que se conectam a um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , como os Suplementos de Mineração de Dados para [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2007.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Movendo objetos de Mineração de dados](moving-data-mining-objects.md)  
  
 [Requisitos e considerações de processamento &#40;mineração de dados&#41;](processing-requirements-and-considerations-data-mining.md)  
  
 [Usando o SQL Server Profiler para monitorar a mineração de dados &#40;Analysis Services - mineração de dados&#41;](using-sql-server-profiler-to-monitor-data-mining-analysis-services-data-mining.md)  
  
## <a name="location-of-data-mining-objects"></a>Localização de objetos de mineração de dados  
 As estruturas e os modelos de mineração que foram processados são armazenados em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Se você criar uma conexão para um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados no `Immediate` objetos de modo ao desenvolver a mineração de dados, todos os objetos que você cria são imediatamente adicionados ao servidor enquanto você trabalha. Entretanto, se você criar objetos de mineração de dados no modo **Offline** , que é o padrão quando trabalha no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], os objetos de mineração criados serão apenas contêineres de metadados, até serem implantados em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Assim, sempre que você fizer uma alteração em um objeto, deverá reimplantar o objeto no servidor [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para obter mais informações sobre a arquitetura de mineração de dados, consulte [Arquitetura física &#40;Analysis Services – Mineração de dados&#41;](physical-architecture-analysis-services-data-mining.md).  
  
> [!NOTE]  
>  Alguns clientes, como os Suplementos de Mineração de Dados para [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2007, também permitem criar modelos e estruturas de mineração de sessão que usam uma conexão com uma instância, mas armazenam a estrutura e os modelos de mineração no servidor somente durante a sessão. Também é possível gerenciar esses modelos através do cliente, da mesma forma que estruturas e modelos armazenados no banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , porém os objetos não persistem depois de desconectar da instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## <a name="managing-data-mining-objects-in-sql-server-data-tools"></a>Gerenciando objetos de mineração de dados em Ferramentas de Dados do SQL Server  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] oferece recursos que permitem criar, navegar e editar objetos de mineração de dados com facilidade.  
  
 Os links a seguir fornecem informações sobre como modificar objetos de mineração de dados usando o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]:  
  
-   [Editar a exibição da fonte de dados usada para a estrutura de mineração](edit-the-data-source-view-used-for-a-mining-structure.md)  
  
-   [Alterar as propriedades de uma estrutura de mineração](change-the-properties-of-a-mining-structure.md)  
  
-   [Alterar as propriedades de um modelo de mineração](change-the-properties-of-a-mining-model.md)  
  
-   [Exibir ou alterar sinalizadores de modelagem &#40;mineração de dados&#41;](modeling-flags-data-mining.md)  
  
-   [Exibir ou alterar parâmetros do algoritmo](view-or-change-algorithm-parameters.md)  
  
 Normalmente você usará o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] como uma ferramenta para desenvolver novos projetos e adicionar a projetos existentes e, em seguida, gerenciar projetos e objetos que foram implantados usando ferramentas como o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 No entanto, você pode modificar diretamente objetos que já estão implantados em uma instância do ssASnoversion usando a opção `Immediate` e conectando ao servidor em modo Online. Para obter mais informações, consulte [Connect in Online Mode to an Analysis Services Database](../multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md).  
  
> [!WARNING]  
>  Todas as alterações em uma estrutura ou um modelo de mineração, inclusive alterações em metadados como um nome ou uma descrição, requerem que a estrutura ou o modelo sejam reprocessados.  
  
 Se você não tiver o arquivo de solução que foi usado para criar o projeto de mineração de dados ou objetos, você pode importar o projeto existente do servidor usando o Assistente de importação do Analysis Services, fazer modificações aos objetos e, em seguida, reimplantar usando a `Incremental` opção. Para obter mais informações, consulte [Importar um projeto de mineração de dados usando o Assistente de Importação do Analysis Services](import-a-data-mining-project-using-the-analysis-services-import-wizard.md).  
  
## <a name="managing-data-mining-objects-in-sql-server-management-studio"></a>Gerenciando objetos de mineração de dados no SQL Server Management Studio  
 No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], é possível fazer scripts, processar ou excluir estruturas e modelos de mineração. Você pode exibir apenas um conjunto limitado de propriedades usando o Pesquisador de Objetos; entretanto, é possível exibir metadados adicionais sobre modelos de mineração abrindo a janela **Consultas DMX** e selecionando uma estrutura de mineração.  
  
-   [Criar uma consulta DMX no SQL Server Management Studio](create-a-dmx-query-in-sql-server-management-studio.md)  
  
## <a name="managing-data-mining-objects-programmatically"></a>Gerenciando programaticamente objetos de mineração de dados  
 Você pode criar, alterar, processar e excluir objetos de mineração de dados usando as linguagens de programação a seguir. Cada linguagem é designada para tarefas diferentes e, por isso, pode haver restrições no tipo de operações que você pode executar. Por exemplo, algumas propriedades dos objetos de mineração de dados não podem ser alteradas com o uso de extensões DMX; você deve utilizar XMLA ou AMO.  
  
### <a name="analysis-management-objects-amo"></a>Objetos de Gerenciamento de Análise (AMO)  
 AMO (Objetos de Gerenciamento de Análise) é um modelo de objeto criado com base em XMLA que lhe proporciona o controle total sobre objetos de mineração de dados. Usando o AMO, você pode criar, implantar e monitorar estruturas e modelos de mineração  
  
-   [Conceitos e modelo de objeto AMO](../multidimensional-models/analysis-management-objects/amo-concepts-and-object-model.md)  
  
-   <xref:Microsoft.AnalysisServices>  
  
 **Restrições:** nenhuma.  
  
### <a name="data-mining-extensions-dmx"></a>Extensões DMX  
 Extensões DMX podem ser usadas com outras interfaces de comando como [!INCLUDE[vstecado](../../includes/vstecado-md.md)] ou ADOMD.Net para criar, excluir e consultar estruturas e modelos de mineração.  
  
-   [Extensões de mineração de dados &#40;DMX&#41; instruções de definição de dados](/sql/dmx/dmx-statements-data-definition)  
  
 **Restrições:** algumas propriedades não podem ser alteradas usando DMX.  
  
### <a name="xml-for-analysis-xmla"></a>XML for Analysis (XMLA)  
 XML for Analysis (XMLA) é a linguagem de definição de dados para todos os Analysis Services. O XMLA dá a você o controle sobre a maioria dos objetos de mineração de dados e operações de servidor. Todas as operações de gerenciamento entre o cliente e o servidor podem ser executadas com o uso de XMLA. Para sua conveniência, é possível usar a ASSL ( [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Scripting Linguagem) para encapsular o XML.  
  
 **Restrições:** [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] gera algumas instruções XMLA que têm suporte apenas para uso interno e não podem ser usadas em scripts XML DDL.  
  
## <a name="see-also"></a>Consulte também  
 [Guia do desenvolvedor do &#40;Analysis Services&#41;](../analysis-services-developer-documentation.md)  
  
  
