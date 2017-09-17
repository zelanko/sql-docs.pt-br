---
title: "Programação de cliente ADOMD.NET | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- programming [ADOMD.NET]
- ADOMD.NET, programming
ms.assetid: 55156115-ecd1-4ed9-876e-23406af9bbf9
caps.latest.revision: 42
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f8a7debab516c8f48b4184c66028c42f44d5bdd2
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="adomdnet-client-programming"></a>Programando o cliente no ADOMD.NET
  Os componentes de cliente do ADOMD.NET residem no **Microsoft.AnalysisServices.AdomdClient** namespace (em microsoft.analysisservices.adomdclient.dll). Esses componentes de cliente fornecem a funcionalidade de cliente e aplicativos de camada intermediária para consultar facilmente os dados e metadados de um repositório de dados analíticos, como [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## <a name="using-the-adomdnet-client-objects"></a>Usando os objetos de cliente do ADOMD.NET  
 Durante a consulta a uma fonte de dados analíticos, existe um conjunto de tarefas comuns que precisam ser executadas. A tabela a seguir representa as tarefas comuns nas quais você usa os objetos de cliente do ADOMD.NET para executar uma consulta assim.  
  
|Tarefa|Description|  
|----------|-----------------|  
|[Estabelecendo conexões no ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net.md)|No ADOMD.NET, você usa um objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> para estabelecer conexões com fontes de dados analíticos, como bancos de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Você pode usar o objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> para executar comandos, para recuperar dados para recuperar metadados da fonte de dados analíticos.|  
|[Recuperando metadados de uma fonte de dados analíticos](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)|Depois que uma conexão foi estabelecida, você poderá usar uma grande variedade de objetos para recuperar informações sobre a fonte de dados subjacente. Essa funcionalidade permite que aplicativos se adaptem à fonte de dados à qual se conectaram.|  
|[Executando comandos em uma fonte de dados analíticos](../../analysis-services/multidimensional-models-adomd-net-client/executing-commands-against-an-analytical-data-source.md)|O objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> oferece as interfaces necessárias para a execução de comandos na fonte de dados analíticos subjacente.|  
|[Recuperando dados de uma fonte de dados analíticos](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md)|Depois que um comando é executado, dados podem ser recuperados e analisados por meio do <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>, <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>, ou **System.XmlReader** objetos.|  
|[Executando transações no ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net-performing-transactions.md)|Todas as ações listadas nas linhas anteriores desta tabela podem ocorrer em uma transação confirmada por leitura, na qual bloqueios compartilhados são mantidos enquanto os dados são lidos para impedir leituras sujas. Os dados ainda podem ser alterados antes do término da transação, resultando em leituras não repetíveis ou em dados fantasma. O objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> oferece a funcionalidade de transação no ADOMD.NET.|  
  
 A interação com a hierarquia de objetos do ADOMD.NET normalmente começa com um ou mais objetos da camada superior, como descrito na tabela a seguir.  
  
|Para|Use este objeto|  
|--------|---------------------|  
|Conectar a uma fonte de dados analíticos|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection><br /> O objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> representa uma conexão a uma fonte de dados e os metadados de fonte de dados. Por exemplo, você pode se conectar a um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cubo local (. cub) de arquivo e, em seguida, examine o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Cubes%2A> propriedade para obter metadados sobre os cubos presentes na fonte de dados analíticos. Esse objeto também representa a implementação de **IDbConnection** interface, uma interface que é necessária para todos os provedores de dados do .NET Framework.|  
|Descobrir os recursos de mineração de dados da fonte de dados|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection><br /> O objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> exibe várias coleções de mineração:<br /><br /><br /><br /> <xref:Microsoft.AnalysisServices.AdomdClient.MiningModelCollection> contém uma lista de todos os modelo de mineração da fonte de dados.<br /><br /><br /><br /> <xref:Microsoft.AnalysisServices.AdomdClient.MiningServiceCollection> oferece informações sobre os algoritmos de mineração disponíveis.<br /><br /><br /><br /> <xref:Microsoft.AnalysisServices.AdomdClient.MiningStructureCollection> exibe informações sobre as estruturas de mineração no servidor.|  
|Consulte a fonte de dados|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand><br /> O objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> representa a instrução ou consulta que será enviada ao servidor. Após o estabelecimento de uma conexão a uma fonte de dados, use o objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> para executar instruções na linguagem suportada, como MDX (Multidimensional Expressions) ou DMX (Data Mining Extensions). Você também pode usar um objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> para retornar resultados na forma de objetos <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> ou <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>.|  
|Recupere dados de uma forma rápida e eficiente|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader><br /> <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> pode ser criado com uma chamada ao método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> ou <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteReader%2A> de um objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>. Esse objeto implementa a **IDbDataReader** de interface do **System. Data** namespace da biblioteca de classes do .NET Framework.|  
|Recupere dados analíticos com a maior quantidade de metadados|<xref:Microsoft.AnalysisServices.AdomdClient.CellSet><br /> <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> pode ser criado com uma chamada ao método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> ou <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteCellSet%2A> de <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>. Quando <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> tiver retornado <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>, você poderá examinar os dados analíticos contidos por <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>.|  
|Recupere metadados sobre cubos, como as dimensões, medidas, conjuntos nomeados disponíveis e assim por diante|<xref:Microsoft.AnalysisServices.AdomdClient.CubeDef><br /> <xref:Microsoft.AnalysisServices.AdomdClient.CubeDef> representa os metadados sobre um cubo. Você referencia <xref:Microsoft.AnalysisServices.AdomdClient.CubeDef> a partir de <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>.|  
|Recuperar dados usando o **System.Data.IDbDataAdapter** interface|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataAdapter><br /> <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataAdapter> oferece suporte somente leitura para aplicativos cliente do .NET Framework existentes.|  
  
## <a name="see-also"></a>Consulte também  
 [Programação do servidor do ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)   
 [Desenvolvendo com ADOMD.NET](../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)  
  
  
