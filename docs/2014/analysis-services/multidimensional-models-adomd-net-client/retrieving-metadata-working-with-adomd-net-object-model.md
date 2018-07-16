---
title: Trabalhando com o modelo de objeto do ADOMD.NET | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- metadata [ADOMD.NET]
- object model (client) [ADOMD.NET]
- retrieving metadata
ms.assetid: 0183dcdc-f2ea-4246-ad00-6e8ccc9d8217
caps.latest.revision: 36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0ceb363b3911afb3a1ea21d51e6a65eff09cd3f7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37328536"
---
# <a name="working-with-the-adomdnet-object-model"></a>Trabalhando com o modelo de objeto do ADOMD.NET
  O ADOMD.NET oferece um modelo de objeto para a exibição dos cubos e dos objetos subordinados contidos em uma fonte de dados analíticos. No entanto, nem todos os metadados de uma determinada fonte de dados analíticos estarão disponíveis por meio do modelo de objeto. O modelo de objeto só fornece acesso às informações mais úteis para que um aplicativo cliente as exiba e permita que um usuário crie comandos de forma interativa. Por causa da complexidade reduzida dos metadados em apresentar, o modelo de objeto do ADOMD.NET é mais fácil usar.  
  
 No modelo de objeto do ADOMD.NET, o objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> fornece acesso a informações nos cubos OLAP (processamento analítico online) e nos modelos de mineração definidos em uma fonte de dados analíticos e objetos relacionados, como dimensões, conjuntos nomeados e algoritmos de mineração.  
  
## <a name="retrieving-olap-metadata"></a>Recuperando metadados OLAP  
 Cada objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> tem uma coleção de objetos de <xref:Microsoft.AnalysisServices.AdomdClient.CubeDef> que representam os cubos disponíveis para o usuário ou para o aplicativo. O objeto <xref:Microsoft.AnalysisServices.AdomdClient.CubeDef> exibe informações sobre o cubo, além de vários objetos relacionados ao cubo, como dimensões, indicadores chave de desempenho, medidas, conjuntos nomeados e assim por diante.  
  
 Sempre que possível, use o objeto <xref:Microsoft.AnalysisServices.AdomdClient.CubeDef> para representar metadados em aplicativos cliente criados para dar suporte a vários servidores OLAP ou para fins de acesso e exibição de metadados gerais.  
  
> [!NOTE]  
>  Para provedor metadados específicos, ou para acesso e exibição detalhados de metadados, use conjuntos de linhas do esquema para recuperar metadados. Para obter mais informações, consulte [Working with Schema Rowsets in ADOMD.NET](retrieving-metadata-working-with-schema-rowsets.md)).  
  
 O exemplo a seguir usa o objeto <xref:Microsoft.AnalysisServices.AdomdClient.CubeDef> para recuperar os cubos visíveis e suas dimensões a partir do servidor local:  
  
 [!code-csharp[Adomd.NetClient#RetrieveCubesAndDimensions](../../snippets/csharp/SQL14/adomd.net/adomd.netclient/cs/adomdexample.cs#retrievecubesanddimensions)]  
  
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
 [Recuperando metadados de uma fonte de dados analíticos](retrieving-metadata-from-an-analytical-data-source.md)  
  
  
