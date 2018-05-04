---
title: Recuperando dados de uma fonte de dados analíticos | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: adomd
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 91976fcd4f3922041152fe41c0e03f89e05483b2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
  
  
