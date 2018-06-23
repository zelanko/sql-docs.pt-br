---
title: Recuperando dados usando o XmlReader | Microsoft Docs
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
- retrieving data
- XmlReader object
- data retrieval [ADOMD.NET], XmlReader object
ms.assetid: 420ec40e-be2d-413a-b4b2-6d2b1756e270
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 257777c40c829921680b8fce333bd6e44f6f57fd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36011013"
---
# <a name="retrieving-data-using-the-xmlreader"></a>Recuperando dados usando o XmlReader
  A classe `XmlReader`, parte do namespace `System.Xml` da Biblioteca de Classes do Microsoft .NET Framework, é similar à classe <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>, uma vez que a classe `XmlReader` também oferece acesso aos dados rápido, sem-cache e somente para encaminhamento. Se não houver necessidade de uma exibição analítica em memória dos dados usando o objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>, o objeto `XmlReader` será perfeito para a recuperação de dados XML, especialmente para grandes quantidades de dados. Como o `XmlReader` cria fluxos de dados, o `XmlReader` não precisa recuperar e armazenar em cache todos os dados antes de exibi-los ao chamador, como seria o caso se um objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> fosse usado para converter a resposta do XML for Analysis para uma representação do modelo de objeto analítico.  
  
 A classe `XmlReader` fornece acesso direto à resposta XML for Analysis recebida pelo ADOMD.NET quando o método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A> do objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> é chamado. Como os dados recuperados são XML bruto, você terá de analisar os dados e os metadados manualmente. Assim que os dados forem recuperados, o objeto `XmlReader` deverá ser fechado.  
  
## <a name="retrieving-data-and-metadata"></a>Recuperando dados e metadados  
 Para usar a classe `XmlReader` para recuperar dados, siga estas etapas:  
  
1.  **Crie uma nova instância do objeto.**  
  
     Para criar uma nova instância da classe `XmlReader`, chame o método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> ou <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A> do objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>.  
  
2.  **Recupere dados.**  
  
     Depois que o comando executar a consulta e retornar um `XmlReader`, analise os dados e os metadados. Os dados e metadados XML são apresentados no formato nativo usado pelo provedor de XML for Analysis. Para a maioria dos provedores de XML for Analysis, o formato nativo será o formato `MDDataSet`. O formato `MDDataSet` fornece dados e metadados para conjuntos de células em um formato bem-estruturado. Para obter mais informações sobre o formato `MDDataSet`, consulte a especificação do XML for Analysis.  
  
3.  **Feche o leitor.**  
  
     Você deve sempre chamar o método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Close%2A> ao terminar de usar o objeto `XmlReader`. Enquanto um `XmlReader` estiver aberto, esse `XmlReader` terá uso exclusivo do objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> usado para executar o comando. Você não poderá executar qualquer comando usando esse <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>, incluindo a criação de outro `XmlReader` ou <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>, até fechar o `XmlReader` original.  
  
### <a name="example-of-retrieving-data-from-the-xmlreader"></a>Exemplo de recuperação de dados do XmlReader  
 O exemplo a seguir executa um comando e recupera os dados como um `XmlReader`, enviando o conteúdo do arquivo para o console.  
  
 [!code-csharp[Adomd.NetClient#OutputDataWithXML](../../snippets/csharp/SQL14/adomd.net/adomd.netclient/cs/adomdexample.cs#outputdatawithxml)]  
  
## <a name="see-also"></a>Consulte também  
 [Recuperando dados de uma fonte de dados analíticos](retrieving-data-from-an-analytical-data-source.md)   
 [Recuperando dados usando o conjunto de células](retrieving-data-using-the-cellset.md)   
 [Recuperando dados usando o AdomdDataReader](retrieving-data-using-the-adomddatareader.md)  
  
  