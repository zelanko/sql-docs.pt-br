---
title: Reporting Services designers de consulta | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- query designers [Reporting Services]
ms.assetid: 07efd3f1-804f-45f7-b62a-3e727a3d9835
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c004b098f900606c2263391cf9363b6e5be2b97b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66102878"
---
# <a name="reporting-services-query-designers"></a>Designers de Consulta do Reporting Services
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]fornece designers de consulta gráficas e baseados em texto para ajudá-lo a criar consultas para cada tipo de fonte de dados em seu relatório.  
  
 Alguns designers gráficos de suporte a fontes de dados ajudam a criar uma consulta de maneira interativa. Outras fontes de dados usam um designer de consulta baseado em texto. Com um designer de consultas gráficas, é possível arrastar os itens de metadados que representam os dados subjacentes em uma fonte de dados para a superfície de design de consulta. Com um designer de consulta com base em texto, o texto do comando pode ser digitado em um painel de consulta. Você pode alterar de um designer de consultas gráficas para um designer de consulta baseado em texto com um clique no ícone do designer de consulta baseado em texto na barra de ferramentas.  
  
 Os tipos de fonte de dados que estão disponíveis em seu relatório são determinados pelas extensões de dados do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] instaladas em seu cliente ou servidor de relatório. Para obter mais informações, consulte [RSReportDesigner Configuration File](report-server/rsreportdesigner-configuration-file.md) e [RSReportServer Configuration File](report-server/rsreportserver-config-configuration-file.md).  
  
 Uma extensão de processamento de dados e seu designer de consulta associado podem diferir em termos de suporte para fontes de dados das seguintes maneiras:  
  
-   **Por tipo de designer de consulta.** Por exemplo, uma fonte de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] dá suporte a designers de consultas gráficas e baseadas em texto.  
  
-   **Por variação de linguagem de consulta.** Por exemplo, uma linguagem de consulta, como [!INCLUDE[tsql](../includes/tsql-md.md)] , pode ter sintaxes diferentes dependendo do tipo da fonte de dados. A [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[tsql](../includes/tsql-md.md)] linguagem e a linguagem SQL Oracle têm alguma variação na sintaxe de um comando de consulta.  
  
-   **Por suporte para a parte de esquema de um nome de objeto de banco de dados.** Quando uma fonte de dados usa esquemas como parte do identificador de objeto do banco de dados, o nome do esquema deve ser fornecido como parte da consulta para todos os nomes que não usam o esquema padrão. Por exemplo, `SELECT FirstName, LastName FROM [Person].[Person]`.  
  
-   **Por suporte para parâmetros de consulta.** Em termos de suporte, os provedores de dados diferem dos parâmetros. Alguns provedores de dados oferecem suporte a parâmetros nomeados; por exemplo, `SELECT Col1, Col2 FROM Table WHERE <parameter identifier><parameter name> = <value>`. Outros provedores de dados oferecem suporte a parâmetros não nomeados; por exemplo, `SELECT Col1, Col2 FROM Table WHERE <column name> = ?`. O identificador de parâmetro pode ser diferente com relação a provedores de dados; por exemplo, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa o símbolo "arroba" (@), o Oracle usa dois-pontos (:). Em alguns provedores de dados, não há suporte para parâmetros.  
  
-   **Por meio da capacidade de importar consultas.** Por exemplo, para uma fonte de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , você pode importar uma consulta de um arquivo de definição de relatório (.rdl) ou de um arquivo .sql.  
  
## <a name="query-designers"></a>Designers de Consulta  
 Os tópicos a seguir descrevem a interface do usuário para cada designer de consulta.  
  
-   [Interface do usuário do Designer de Consulta MDX do Analysis Services](report-data/analysis-services-mdx-query-designer-user-interface.md)  
  
-   [Interface de usuário do Designer de Consulta DMX do Analysis Services](report-data/analysis-services-dmx-query-designer-user-interface.md)  
  
-   [Interface de usuário do Designer de consultas gráficas](report-data/graphical-query-designer-user-interface.md)  
  
-   [Interface de usuário do Designer de Consulta relacional](../../2014/reporting-services/relational-query-designer-user-interface.md)  
  
-   [Interface de usuário do Designer de Consulta do Hyperion Essbase](report-data/hyperion-essbase-query-designer-user-interface.md)  
  
-   [Interface de usuário do Designer de Consulta do modelo de relatório](report-data/report-model-query-designer-user-interface.md)  
  
-   [Interface do usuário do Designer de Consulta do SAP NetWeaver BI](report-data/sap-netweaver-bi-query-designer-user-interface.md)  
  
-   [Designer de Consulta de Lista do SharePoint](../../2014/reporting-services/sharepoint-list-query-designer.md)  
  
-   [Interface de usuário do Designer de Consulta baseado em texto](../../2014/reporting-services/text-based-query-designer-user-interface.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Fontes de dados com suporte pelo Reporting Services &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [Adicionar dados de fontes de dados externas &#40;SSRS&#41;](report-data/add-data-from-external-data-sources-ssrs.md)   
 [Extensões de processamento de dados e provedores de dados de .NET Framework &#40;SSRS&#41;](report-data/data-processing-extensions-and-net-framework-data-providers-ssrs.md)   
 [Extensões &#40;SSRS&#41;](extensions-ssrs.md)  
  
  
