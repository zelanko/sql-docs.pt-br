---
title: Estabelecendo conexões no ADOMD.NET | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: adomd
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e135ba498b4ad4b09b330ddab0e49df6144d161d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="connections-in-adomdnet"></a>Conexões no ADOMD.NET
  No ADOMD.NET, você usa o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> objeto para abrir conexões com fontes de dados analíticos, como [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bancos de dados. Quando a conexão não for mais necessária, feche-a explicitamente.  
  
## <a name="opening-a-connection"></a>Abrindo uma conexão  
 Para abrir uma conexão no ADOMD.NET, primeiro especifique uma cadeia de conexão para uma fonte de dados analíticos e um banco de dados válidos. Em seguida, abra a conexão explicitamente para a fonte de dados.  
  
### <a name="specifying-a-multidimensional-data-source"></a>Especificando uma fonte de dados multidimensional  
 Para especificar uma fonte de dados analíticos e um banco de dados, defina a propriedade <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> propriedade do objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>. A cadeia de conexão especificada para a propriedade <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> é uma cadeia de caracteres compatível com OLE DB. O ADOMD.NET usa a cadeia de conexão especificada para determinar como será feita a conexão ao servidor.  
  
 A propriedade <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> pode ser definida em um objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> existente ou durante a criação de uma instância de um objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>. O seguinte código demonstra como definir a propriedade <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> durante a criação de uma conexão ADOMD:  
  
```vb  
Dim advwrksConnection As New AdomdConnection("Data Source=localhost;Catalog=AdventureWorksAS")  
System.Diagnostics.Debug.Writeline(advwrksConnection.ConnectionString)  
```  
  
```csharp  
AdomdConnection advwrksConnection = new AdomdConnection("Data Source=localhost;Catalog=AdventureWorksAS");  
System.Diagnostics.Debug.Writeline(advwrksConnection.ConnectionString);  
```  
  
### <a name="opening-a-connection-to-the-data-source"></a>Abrindo uma conexão à fonte de dados  
 Depois de especificar a cadeia de conexão, use o método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A> para abrir a conexão. Quando você abre um objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>, pode definir vários níveis de segurança para a conexão. O nível de segurança que é usado para a conexão depende do valor da **ProtectionLevel** configuração de cadeia de caracteres de conexão. Para obter mais informações sobre como abrir conexões seguras no ADOMD.NET, consulte [estabelecer conexões seguras no ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net-establishing-secure-connections.md).  
  
## <a name="working-with-a-connection"></a>Trabalhando com uma conexão  
 Cada conexão aberta existe em uma sessão, fornecendo suporte para operações de monitoração de estado. Uma sessão pode ser compartilhada por mais de uma conexão aberta. O compartilhamento de uma sessão permite que mais de um cliente use o mesmo contexto. Para obter mais informações, consulte [trabalhar com conexões e sessões no ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net-working-with-connections-and-sessions.md).  
  
 Você pode usar uma conexão aberta para recuperar metadados, dados e executar comandos. Para obter mais informações, consulte [recuperar metadados de uma fonte de dados analíticos](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md), [recuperando dados de uma fonte de dados analíticos](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md), e [executar comandos em relação a um dados analíticos Origem](../../analysis-services/multidimensional-models-adomd-net-client/executing-commands-against-an-analytical-data-source.md).  
  
 Enquanto a conexão estiver aberta, você poderá recuperar dados, recuperar metadados e executar comandos de uma transação confirmada por leitura, na qual bloqueios compartilhados são mantidos enquanto os dados são lidos para impedir leituras sujas. Os dados ainda podem ser alterados antes do término da transação, resultando em leituras não repetíveis ou em dados fantasma. Para obter mais informações, consulte [executando transações no ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net-performing-transactions.md).  
  
## <a name="closing-a-connection"></a>Fechando uma conexão  
 Recomendamos que você feche explicitamente um objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> assim que a conexão não for mais necessária. Para fechar explicitamente a conexão, você deve usar o **fechar** e **Dispose** métodos do <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> objeto.  
  
 Uma conexão que não foi explicitamente fechada, mas que pode sair do escopo, pode não liberar recursos do servidor rápido o suficiente para permitir que aplicativos clientes de alta simultaneidade do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] abram novas conexões com eficiência. Dependendo da forma como você criou a conexão, a sessão usada pelo objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> poderá permanecer ativa se a conexão não for fechada explicitamente.  
  
 Para obter mais informações sobre as sessões, consulte [trabalhar com conexões e sessões no ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net-working-with-connections-and-sessions.md).  
  
> [!IMPORTANT]  
>  No **Finalize** implementado de método de qualquer classe, não chame o **fechar** ou **Dispose** métodos de um <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> objeto, ou qualquer outro objeto gerenciado. Em um finalizador, só libere os recursos não gerenciados de propriedade direta da classe implementada. Se a classe implementada não possuir algum recurso não gerenciado, não inclua um **Finalize** método na definição de classe.  
  
## <a name="see-also"></a>Consulte também  
 [Programação do cliente no ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)  
  
  
