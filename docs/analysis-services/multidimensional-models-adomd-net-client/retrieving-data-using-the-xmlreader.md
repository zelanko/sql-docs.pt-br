---
title: Recuperando dados usando o XmlReader | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- retrieving data
- XmlReader object
- data retrieval [ADOMD.NET], XmlReader object
ms.assetid: 420ec40e-be2d-413a-b4b2-6d2b1756e270
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 70b268a896a7acbbf515ac49a722eccb17afdfd8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="retrieving-data-using-the-xmlreader"></a>Recuperando dados usando o XmlReader
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]O **XmlReader** parte da classe a **System. XML** namespace para a biblioteca de classes do Microsoft .NET Framework, é semelhante ao <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> classe em que o **XmlReader**classe também rápida, fornece acesso de não armazenado em cache, somente encaminhamento aos dados. Se não há necessidade de uma exibição na memória, análise de dados usando o <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> objeto, o **XmlReader** objeto é perfeito para recuperar dados XML, especialmente para grandes quantidades de dados. Porque **XmlReader** fluxos de dados, **XmlReader** não precisa recuperar e armazenar em cache todos os dados antes de exibi-los ao chamador, como seria o caso se um <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> objeto fosse usado para converter o Resposta do XML for Analysis em uma representação do modelo de objeto analítico.  
  
 O **XmlReader** classe fornece acesso direto ao XML para resposta de Analysis recebida pelo ADOMD.NET quando o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A> método o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> objeto é chamado. Como os dados recuperados são XML bruto, você terá de analisar os dados e os metadados manualmente. Assim que os dados foram recuperados, o **XmlReader** objeto deve ser fechado.  
  
## <a name="retrieving-data-and-metadata"></a>Recuperando dados e metadados  
 Para usar o **XmlReader** classe para recuperar dados, siga estas etapas:  
  
1.  **Crie uma nova instância do objeto.**  
  
     Para criar uma nova instância do **XmlReader** classe, chame o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> ou <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A> método o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> objeto.  
  
2.  **Recupere dados.**  
  
     Depois que o comando executa a consulta e retorna um **XmlReader**, você deve analisar os dados e metadados. Os dados e metadados XML são apresentados no formato nativo usado pelo provedor de XML for Analysis. A maioria dos XML para provedores de análise, o formato nativo é o **MDDataSet** formato. O **MDDataSet** formato fornece os dados e metadados para conjuntos de células em um formato bem estruturado. Para obter mais informações sobre o **MDDataSet** de formato, consulte a especificação XML for Analysis.  
  
3.  **Feche o leitor.**  
  
     Você sempre deve chamar o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Close%2A> método quando você terminar de usar o **XmlReader** objeto. Enquanto um **XmlReader** estiver aberto, o que **XmlReader** tem uso exclusivo do <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> objeto que foi usado para executar o comando. Você não poderá executar qualquer comando usando <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>, incluindo a criação de outro **XmlReader** ou <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>, até que você feche o original **XmlReader**.  
  
### <a name="example-of-retrieving-data-from-the-xmlreader"></a>Exemplo de recuperação de dados do XmlReader  
 O exemplo a seguir executa um comando e recupera os dados como um **XmlReader**, enviando o conteúdo do arquivo para o console.  
  
 [!code-cs[Adomd.NetClient#OutputDataWithXML](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/retrieving-data-using-th_1_1.cs)]  
  
## <a name="see-also"></a>Consulte Também  
 [Recuperando dados de uma fonte de dados analíticos](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md)   
 [Recuperando dados usando o conjunto de células](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-cellset.md)   
 [Recuperando dados usando o AdomdDataReader](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-adomddatareader.md)  
  
  
