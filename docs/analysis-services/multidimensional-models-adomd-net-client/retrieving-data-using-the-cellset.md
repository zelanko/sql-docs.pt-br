---
title: "Recuperando dados usando o conjunto de células | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- CellSet object
- retrieving data
- data retrieval [ADOMD.NET], CellSet object
ms.assetid: 77e4ee58-882d-4012-91a3-0565f18a4882
caps.latest.revision: "41"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 60ed3598bd03977ae56eb159afd01955e109275e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="retrieving-data-using-the-cellset"></a>Recuperando dados usando CellSet
  Ao recuperar dados analíticos, o objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> oferece o máximo de interatividade e de flexibilidade. O objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> é um cache em memória de dados hierárquicos e de metadados que armazena a dimensionalidade original dos dados. O objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> também pode ser atravessado em um estado conectado ou desconectado. Por causa desse recurso de desconexão, o objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> pode ser usado para exibir dados e metadados em qualquer ordem e oferece o modelo de dados mais abrangente para a recuperação de dados. O recurso de desconexão também faça com que o objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> obtenha o máximo de sobrecarga e seja o modelo de objeto de recuperação de dados do ADOMD.NET de preenchimento mais lento.  
  
## <a name="retrieving-data-in-a-connected-state"></a>Recuperando dados em um estado conectado  
 Para usar o objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> para recuperar dados, siga estas etapas:  
  
1.  **Crie uma nova instância do objeto.**  
  
     Para criar uma nova instância do objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>, chame o método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> ou <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteCellSet%2A> do objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>.  
  
2.  **Identifique metadados.**  
  
     Além de recuperar dados, o ADOMD.NET também recupera metadados para o conjunto de células. Assim que o comando tiver executado a consulta e retornado um <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>, você poderá recuperar os metadados por meio de vários objetos. Esses metadados são necessários para que aplicativos cliente exibam e interajam com os dados do conjunto de células. Por exemplo, muitos aplicativos cliente oferecem funcionalidade para busca detalhada de, ou a exibição hierárquica das posições filho de, uma posição especificada em um conjunto de células.  
  
     No ADOMD.NET, as propriedades <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.Axes%2A> e <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.FilterAxis%2A> do objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> representam os metadados de eixos de consulta e slicer, respectivamente, no conjunto de células retornado. Ambas as propriedades retornam referências a objetos de <xref:Microsoft.AnalysisServices.AdomdClient.Axis> que, por sua vez, contêm as posições representadas em cada eixo.  
  
     Cada objeto <xref:Microsoft.AnalysisServices.AdomdClient.Axis> contém uma coleção de objetos <xref:Microsoft.AnalysisServices.AdomdClient.Position> que representam o conjunto de tuplas disponível para aquele eixo. Cada objeto <xref:Microsoft.AnalysisServices.AdomdClient.Position> representa uma única tupla que contém um ou mais membros, representados por uma coleção de objetos de <xref:Microsoft.AnalysisServices.AdomdClient.Member>.  
  
3.  **Recupere dados da coleção de conjunto de células.**  
  
     Além de recuperar metadados, o ADOMD.NET também recupera dados para o conjunto de células. Assim que o comando tiver executado a consulta e retornado um <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>, você poderá recuperar os dados usando a coleção <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.Cells%2A> de <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>. Essa coleção contém os valores calculados para a interseção de todos os eixos na consulta. Dessa forma, existem vários indexadores para o acesso a cada interseção ou célula. Para obter uma lista de indexadores, consulte <xref:Microsoft.AnalysisServices.AdomdClient.CellCollection.Item%2A>.  
  
### <a name="example-of-retrieving-data-in-a-connected-state"></a>Exemplo de recuperação de dados em um estado conectado  
 O exemplo a seguir cria uma conexão ao servidor local e executa um comando nessa conexão. O exemplo analisa os resultados usando o **conjunto de células** modelo de objeto: as legendas (metadados) para as colunas são recuperadas do primeiro eixo e as legendas (metadados) para cada linha são recuperadas do segundo eixo e o dados de interseção é recuperado por meio de <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.Cells%2A> coleção.  
  
 [!code-cs[Adomd.NetClient#ReturnCommandUsingCellSet](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/retrieving-data-using-th_0_1.cs)]  
  
## <a name="retrieving-data-in-a-disconnected-state"></a>Recuperando dados em um estado desconectado  
 Ao carregar o XML retornado de uma consulta anterior, você poderá usar o objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> para fornecer um método abrangente de navegação nos dados analíticos sem exigir uma conexão ativa.  
  
> [!NOTE]  
>  Nem todas as propriedades dos objetos estão disponíveis a partir do objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> durante um estado desconectado. Para obter mais informações, consulte <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.LoadXml%2A>.  
  
### <a name="example-of-retrieving-data-in-a-disconnected-state"></a>Exemplo de recuperação de dados em um estado desconectado  
 O exemplo a seguir é semelhante ao exemplo de metadados e de dados mostrado anteriormente neste tópico. No entanto, o comando no exemplo a seguir é executado com uma chamada para <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A>, e o resultado é retornado como um **System.XML. XmlReader**. O exemplo preenche a <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> objeto usando este **System.XML. XmlReader** com o <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.LoadXml%2A> método. Embora este exemplo carrega o **System.XML. XmlReader** imediatamente, você pode armazenar em cache o XML contido pelo leitor em um disco rígido ou transportar esses dados para um aplicativo diferente por qualquer meio antes de carregar os dados em um o conjunto de células.  
  
 [!code-cs[Adomd.NetClient#DemonstrateDisconnectedCellset](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/retrieving-data-using-th_0_2.cs)]  
  
## <a name="see-also"></a>Consulte também  
 [Recuperando dados de uma fonte de dados analíticos](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md)   
 [Recuperando dados usando o AdomdDataReader](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-adomddatareader.md)   
 [Recuperando dados usando o XmlReader](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-xmlreader.md)  
  
  
