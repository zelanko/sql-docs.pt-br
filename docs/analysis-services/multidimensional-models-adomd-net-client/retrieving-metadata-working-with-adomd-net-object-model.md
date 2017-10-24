---
title: Trabalhando com o modelo de objeto do ADOMD.NET | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- metadata [ADOMD.NET]
- object model (client) [ADOMD.NET]
- retrieving metadata
ms.assetid: 0183dcdc-f2ea-4246-ad00-6e8ccc9d8217
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 81a9272284e662eb7f5f47e464e85e324b92a39d
ms.contentlocale: pt-br
ms.lasthandoff: 10/24/2017

---
# <a name="retrieving-metadata---working-with-adomdnet-object-model"></a>Recuperando metadados - trabalhando com o modelo de objeto do ADOMD.NET
  O ADOMD.NET oferece um modelo de objeto para a exibição dos cubos e dos objetos subordinados contidos em uma fonte de dados analíticos. No entanto, nem todos os metadados de uma determinada fonte de dados analíticos estarão disponíveis por meio do modelo de objeto. O modelo de objeto só fornece acesso às informações mais úteis para que um aplicativo cliente as exiba e permita que um usuário crie comandos de forma interativa. Por causa da complexidade reduzida dos metadados em apresentar, o modelo de objeto do ADOMD.NET é mais fácil usar.  
  
 No modelo de objeto do ADOMD.NET, o objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> fornece acesso a informações nos cubos OLAP (processamento analítico online) e nos modelos de mineração definidos em uma fonte de dados analíticos e objetos relacionados, como dimensões, conjuntos nomeados e algoritmos de mineração.  
  
## <a name="retrieving-olap-metadata"></a>Recuperando metadados OLAP  
 Cada objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> tem uma coleção de objetos de <xref:Microsoft.AnalysisServices.AdomdClient.CubeDef> que representam os cubos disponíveis para o usuário ou para o aplicativo. O objeto <xref:Microsoft.AnalysisServices.AdomdClient.CubeDef> exibe informações sobre o cubo, além de vários objetos relacionados ao cubo, como dimensões, indicadores chave de desempenho, medidas, conjuntos nomeados e assim por diante.  
  
 Sempre que possível, use o objeto <xref:Microsoft.AnalysisServices.AdomdClient.CubeDef> para representar metadados em aplicativos cliente criados para dar suporte a vários servidores OLAP ou para fins de acesso e exibição de metadados gerais.  
  
> [!NOTE]  
>  Para provedor metadados específicos, ou para acesso e exibição detalhados de metadados, use conjuntos de linhas do esquema para recuperar metadados. Para obter mais informações, consulte [Working with Schema Rowsets in ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 O exemplo a seguir usa o objeto <xref:Microsoft.AnalysisServices.AdomdClient.CubeDef> para recuperar os cubos visíveis e suas dimensões a partir do servidor local:  
  
 [!code-cs[Adomd.NetClient#RetrieveCubesAndDimensions](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/retrieving-metadata-work_1_1.cs)]  
  
## <a name="retrieving-data-mining-metadata"></a>Recuperando metadados de mineração de dados  
 Cada objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> tem várias coleções que oferecem informações sobre as capacidades de mineração de dados da fonte de dados:  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.MiningModelCollection> contém uma lista de todos os modelo de mineração da fonte de dados.  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.MiningServiceCollection> oferece informações sobre os algoritmos de mineração disponíveis.  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.MiningStructureCollection> exibe informações sobre as estruturas de mineração no servidor.  
  
 Para determinar como consultar um modelo de mineração no servidor, itere pela coleção <xref:Microsoft.AnalysisServices.AdomdServer.MiningModel.Columns%2A>. Cada objeto <xref:Microsoft.AnalysisServices.AdomdClient.MiningModelColumn> exibe as seguintes características:  
  
-   Se o objeto é uma coluna de entrada (<xref:Microsoft.AnalysisServices.AdomdClient.MiningModelColumn.IsInput%2A>).  
  
-   Se o objeto é uma coluna de previsão (<xref:Microsoft.AnalysisServices.AdomdClient.MiningModelColumn.IsPredictable%2A>).  
  
-   Os valores associados a uma coluna discreta (<xref:Microsoft.AnalysisServices.AdomdClient.MiningModelColumn.Values%2A>)  
  
-   O tipo de dados da coluna (<xref:Microsoft.AnalysisServices.AdomdClient.MiningModelColumn.Type%2A>).  
  
## <a name="see-also"></a>Consulte também  
 [Recuperando metadados de uma fonte de dados analíticos](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)  
  
  

