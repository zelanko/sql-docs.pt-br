---
title: "Recuperando dados de uma fonte de dados analíticos | Microsoft Docs"
ms.custom: 
ms.date: 02/14/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- data retrieval [ADOMD.NET]
- retrieving data
- ADOMD.NET, data retrieval
- data retrieval [ADOMD.NET], about retrieving data
ms.assetid: 88358189-28aa-4bc7-8dda-5a92e3a012b8
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 215310100f5151b20e8d813e49c54c056a9e760d
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="retrieving-data-from-an-analytical-data-source"></a>Recuperando dados de uma fonte de dados analíticos
  Depois de fazer uma conexão e de criar a consulta, você poderá recuperar dados. No ADOMD.NET, você pode recuperar dados usando três objetos diferentes (<xref:Microsoft.AnalysisServices.AdomdClient.CellSet>, <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>, e <xref:System.Xml.XmlReader>) chamando um do **Execute** métodos do <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> objeto.  
  
 Cada um desses três objetos equilibram interatividade e sobrecarga:  
  
-   *Interatividade* refere-se a facilidade de uso e a quantidade de informações disponíveis por meio do modelo de objeto.  
  
-   *Sobrecarga* refere-se à quantidade de tráfego que gera um modelo de objeto sobre a conexão de rede para o servidor, a quantidade de memória necessária para o modelo de objeto e a velocidade com que o modelo de objeto recupera dados.  
  
 Para ajudar você a selecionar o objeto de recuperação de dados que melhor atenda às necessidades do seu aplicativo, a tabela a seguir realça as diferenças entre interatividade e sobrecarga para cada objeto.  
  
|Objeto|Interatividade|Sobrecarga|Mantém a dimensionalidade|Informações de uso|  
|------------|-------------------|--------------|----------------------------|-----------------------|  
|<xref:Microsoft.AnalysisServices.AdomdClient.CellSet>|Maior|Moderadamente alta, que resulta em uma recuperação mais lenta de dados|Sim|[Recuperando dados usando CellSet](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-cellset.md)|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataAdapter>|Moderado|Moderado|não|[Preenchendo um DataSet de um DataAdapter](http://go.microsoft.com/fwlink/?LinkId=70016)|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>|Moderado|Moderado|não|[Recuperando dados usando o AdomdDataReader](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-adomddatareader.md)|  
|<xref:System.Xml.XmlReader>|Mais Baixo|Menor, que resulta em uma recuperação de dados mais rápida|Sim|[Recuperando dados usando o XmlReader](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-xmlreader.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Programação do cliente no ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)  
  
  
