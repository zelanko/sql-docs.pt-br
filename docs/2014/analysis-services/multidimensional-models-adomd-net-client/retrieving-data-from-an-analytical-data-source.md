---
title: Recuperando dados de uma fonte de dados analíticos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- data retrieval [ADOMD.NET]
- retrieving data
- ADOMD.NET, data retrieval
- data retrieval [ADOMD.NET], about retrieving data
ms.assetid: 88358189-28aa-4bc7-8dda-5a92e3a012b8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0cfc0c783e8c61689d8f5b0ca3bab6ded39a57a4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48212376"
---
# <a name="retrieving-data-from-an-analytical-data-source"></a>Recuperando dados de uma fonte de dados analíticos
  Depois de fazer uma conexão e de criar a consulta, você poderá recuperar dados. No ADOMD.NET, você pode recuperar dados usando três objetos diferentes (<xref:Microsoft.AnalysisServices.AdomdClient.CellSet>, <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> e <xref:System.Xml.XmlReader>) chamando um dos métodos `Execute` do objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>.  
  
 Cada um desses três objetos equilibram interatividade e sobrecarga:  
  
-   *Interatividade* refere-se para a facilidade de uso e a quantidade de informações disponíveis por meio do modelo de objeto.  
  
-   *Sobrecarga* refere-se à quantidade de tráfego que um modelo de objeto gera sobre a conexão de rede para o servidor, a quantidade de memória necessária para o modelo de objeto e a velocidade com a qual o modelo de objeto recupera dados.  
  
 Para ajudar você a selecionar o objeto de recuperação de dados que melhor atenda às necessidades do seu aplicativo, a tabela a seguir realça as diferenças entre interatividade e sobrecarga para cada objeto.  
  
|Object|Interatividade|Sobrecarga|Mantém a dimensionalidade|Informações de uso|  
|------------|-------------------|--------------|----------------------------|-----------------------|  
|<xref:Microsoft.AnalysisServices.AdomdClient.CellSet>|Maior|Moderadamente alta, que resulta em uma recuperação mais lenta de dados|Sim|[Recuperando dados usando CellSet](retrieving-data-using-the-cellset.md)|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataAdapter>|Moderado|Moderado|não|[Populating a DataSet from a DataAdapter](http://go.microsoft.com/fwlink/?LinkId=70016)|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>|Moderado|Moderado|não|[Recuperando dados usando o AdomdDataReader](retrieving-data-using-the-adomddatareader.md)|  
|<xref:System.Xml.XmlReader>|Mais Baixo|Menor, que resulta em uma recuperação de dados mais rápida|Sim|[Recuperando dados usando o XmlReader](retrieving-data-using-the-xmlreader.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Programação do cliente no ADOMD.NET](adomd-net-client-programming.md)  
  
  
