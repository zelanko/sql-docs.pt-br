---
title: Trabalhando com conjuntos de linhas de esquema no ADOMD.NET | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
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
- retrieving metadata
- schema rowsets [ADOMD.NET]
ms.assetid: 7bf75bf8-f1e1-44f6-ac42-c38a681654cf
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e77a3a4c7d38779da149f63644ad9a3106034f51
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37310746"
---
# <a name="working-with-schema-rowsets-in-adomdnet"></a>Trabalhando com conjuntos de linhas do esquema no ADOMD.NET
  Quando você precisa de mais metadados do que os que estão disponíveis no modelo de objeto do ADOMD.NET, o ADOMD.NET oferece o recurso de recuperação de todo o intervalo de conjuntos de linhas do esquema XMLA (XML for Analysis), OLE DB, OLE DB for OLAP e OLE DB for Data Mining:  
  
 **Metadados XML for Analysis**  
 Os conjuntos de linhas do esquema do XML for Analysis oferecem um método para a recuperação de informações de baixo nível sobre o servidor. As informações disponíveis incluem as fontes de dados disponíveis no servidor, as palavras-chave reservadas pelo provedor, o literais suportados pelo provedor e mais. Você pode até usar um conjunto de linhas do esquema do XML for Analysis para descobrir todos os conjuntos de linhas do esquema suportados pelo provedor.  
  
 Para obter mais informações: [XML for Analysis Schema Rowsets](../schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
 **Metadados OLE DB**  
 Os conjuntos de linhas do esquema do OLE DB oferecem um método padrão do setor para a recuperação de informações de uma variedade de provedores.  
  
 Para obter mais informações: [OLE DB Schema Rowsets](../schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
 **Metadados OLAP**  
 As informações de esquema oferecidas para uma fonte de dados analíticos incluem bancos de dados ou catálogos disponíveis na fonte de dados analíticos, cubos e modelos de mineração em um banco de dados, funções existentes para cubos na fonte de dados e mais.  
  
 Para obter mais informações: [OLE DB para OLAP Schema Rowsets](../schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
 **Metadados de mineração de dados**  
 Além dos metadados OLAP, os metadados de mineração de dados podem ser recuperados por meio de conjuntos de linhas do esquema. Os conjuntos de linhas disponíveis exibem informações nos modelos de mineração de dados disponíveis no banco de dados, os algoritmos de mineração disponíveis, os parâmetros exigidos pelo algoritmo, estruturas de mineração e mais.  
  
 Para obter mais informações: [Data Mining Schema Rowsets](../schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
 Para cada um dos vários conjuntos de linhas do esquema, você recupera metadados do conjunto de linhas passando um GUID ou nome XMLA com o método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A> do objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>.  
  
## <a name="retrieving-metadata-by-passing-guids"></a>Recuperando metadados passando GUIDs  
 A classe <xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid> contém uma lista de campos que representam os conjuntos de linhas do esquema geralmente suportados por provedores e por fontes de dados analíticos. Para recuperar metadados gerais e específicos do provedor de um provedor ou de uma fonte de dados analíticos, use os GUIDs contidos no objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid> com um dos métodos a seguir:  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
> [!NOTE]  
>  O provedor de dados do ADOMD.NET exibe informações de esquema por meio da funcionalidade disponibilizada por seu provedor e pela fonte de dados analíticos específicos. Cada provedor e fonte de dados pode fornecer metadados diferentes.  
  
## <a name="retrieving-metadata-by-passing-xmla-names"></a>Recuperando metadados passando nomes XMLA  
 Os métodos a seguir obtém como argumentos o nome do esquema XMLA que identifica quais serão as informações de esquema a serem retornadas e uma matriz de restrições nas colunas retornadas:  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
 Cada um destes métodos retorna uma instância de um objeto `DataSet` preenchido com as informações de esquema. O objeto `DataSet` pertence ao namespace `System.Data` da Biblioteca de Classes do Microsoft .NET Framework.  
  
## <a name="example"></a>Exemplo  
 No exemplo a seguir, a função GetActions usa uma conexão, o nome do cubo, uma coordenada e um tipo de coordenada, recupera uma [conjunto de linhas MDSCHEMA_ACTIONS](../schema-rowsets/ole-db-olap/mdschema-actions-rowset.md)e retorna as ações disponíveis na coordenada selecionada.  
  
 [!code-csharp[Adomd.NetClient#GetActions](../../snippets/csharp/SQL14/adomd.net/adomd.netclient/cs/adomdexample.cs#getactions)]  
  
## <a name="see-also"></a>Consulte também  
 [Recuperando metadados de uma fonte de dados analíticos](retrieving-metadata-from-an-analytical-data-source.md)  
  
  
