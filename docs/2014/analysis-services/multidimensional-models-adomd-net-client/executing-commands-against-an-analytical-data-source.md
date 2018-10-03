---
title: Executando comandos em uma fonte de dados analíticos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- AdomdCommand object
- commands [ADOMD.NET]
- ADOMD.NET, commands
ms.assetid: 1a958e5f-fc18-480b-9706-fc44e3b1d534
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6f37e3fe4cccfbfc8824971881c7d5fb68240252
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48117338"
---
# <a name="executing-commands-against-an-analytical-data-source"></a>Executando comandos em uma fonte de dados analíticos
  Depois de estabelecer uma conexão com uma fonte de dados analíticos, você poderá usar um objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> para executar comandos nessa fonte de dados e retornar resultados dela. Esses comandos podem recuperar dados usando MDX (Multidimensional Expressions), DMX (Data Mining Extensions) ou até mesmo uma sintaxe limitada de SQL. Além disso, você poderá usar comandos ASSL (Analysis Services Scripting Language) para modificar o banco de dados subjacente.  
  
## <a name="creating-a-command"></a>Criando um comando  
 Antes de executar um comando, você deverá criá-lo. Você pode criar um comando usando um destes métodos:  
  
-   O primeiro método usa o construtor <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>, que pode fazer com que um comando seja executado na fonte de dados, e usa um objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> no qual o comando será executado.  
  
-   O segundo método usa o método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.CreateCommand%2A> do objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>.  
  
 O texto do comando a ser executado pode ser consultado e modificado por meio da propriedade <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.CommandText%2A>. Os comandos criados por você não precisam retornar dados depois de executados.  
  
## <a name="running-a-command"></a>Executar um comando  
 Depois que criar um objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>, existem vários métodos <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> que o seu comando poderá usar para executar diversas ações. A tabela a seguir lista algumas dessas ações.  
  
|Para|Use este método|  
|--------|---------------------|  
|Retornar resultados como um fluxo de dados|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteReader%2A> para retornar um objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>|  
|Retornar um objeto <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteCellSet%2A>|  
|Executar comandos que não retornam linhas|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteNonQuery%2A>|  
|Retorne um objeto `XMLReader` que contenha os dados em um formato compatível com XMLA (XML for Analysis)|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A>|  
  
### <a name="example-of-running-a-command"></a>Exemplo de execução de um comando  
 Este exemplo usa o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> para executar um comando XMLA que processará o cubo `Adventure Works DW` no servidor local, sem retornar dados.  
  
 [!code-csharp[Adomd.NetClient#ExecuteXMLAProcessCommand](../../snippets/csharp/SQL14/adomd.net/adomd.netclient/cs/adomdexample.cs#executexmlaprocesscommand)]  
  
  
