---
title: Trabalhando com conexões e sessões no ADOMD.NET | Microsoft Docs
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
- sessions [ADOMD.NET]
- connections [ADOMD.NET]
ms.assetid: 72b43c06-f3e4-42c3-a696-4a3419c3b884
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6ef7c679aa0f295c486836763158a89a1f593ff8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37176953"
---
# <a name="working-with-connections-and-sessions-in-adomdnet"></a>Trabalhando com conexões e com sessões no ADOMD.NET
  No XMLA (XML for Analysis), sessões dão suporte a operações de estado durante o acesso a dados analíticos. As sessões enquadram o escopo e o contexto de comandos e de transações para uma fonte de dados analíticos. Os elementos XMLA usados para gerenciar sessões são [BeginSession](../xmla/xml-elements-headers/beginsession-element-xmla.md), [Session](../xmla/xml-elements-headers/session-element-xmla.md)e [EndSession](../xmla/xml-elements-headers/endsession-element-xmla.md).  
  
 O ADOMD.NET usa esses três elementos de sessão XMLA quando você inicia uma sessão, executa consultas ou recupera dados durante a sessão e fecha uma sessão.  
  
## <a name="starting-a-session"></a>Iniciando uma sessão  
 A propriedade <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> do objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> contém o identificador da sessão ativa associada ao objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>. Ao usar essa propriedade corretamente, você poderá controlar efetivamente a capacidade de manutenção de status do processo de cliente e de servidor em seu aplicativo:  
  
-   Se a propriedade <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> não for definida para uma ID de sessão válida quando o método de <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A> for chamado, o objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> solicitará uma nova ID de sessão do provedor. O ADOMD.NET inicia uma sessão enviando um cabeçalho `BeginSession` XMLA ao provedor. Se o ADOMD.NET tiver êxito em iniciar uma sessão, o ADOMD.NET definirá o valor da propriedade de <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> para a ID de sessão da sessão recém-criada.  
  
-   Se a propriedade <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> não for definida para uma ID de sessão válida quando o método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A> for chamado, o objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> tentará se conectar à sessão especificada.  
  
 Se o objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> não puder se conectar à sessão especificada, ou se o provedor não der suporte a sessões, uma exceção será lançada.  
  
> [!NOTE]  
>  Depois de fazer o ADOMD.NET criar uma sessão, você poderá conectar vários objetos de <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> a essa sessão ativa única ou poderá desconectar um único objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> dessa sessão e reconectá-lo a outra sessão.  
  
## <a name="working-in-a-session"></a>Trabalhando em uma sessão  
 Depois que o ADOMD.NET conecta o objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> a uma sessão válida, enviará um cabeçalho `Session` XMLA ao provedor com todas as solicitações de dados ou de metadados feitas por um aplicativo. Todas as solicitações terão a ID de sessão definida como o valor da propriedade de <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A>.  
  
 Uma ID de sessão não garante que uma sessão permanecerá válida. Se a sessão expirar (por exemplo, se o tempo limite da sessão for alcançado ou se a conexão for interrompida), o provedor poderá optar por encerrar e reverter as ações dessa sessão. Se isso ocorrer, todas as chamadas método subsequentes do objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> lançarão uma exceção. Como as exceções são lançadas somente quando a próxima solicitação é enviada ao provedor, e não quando a sessão expira, o seu aplicativo deve ser capaz de manipulá-las sempre que o seu aplicativo recuperar dados ou metadados do provedor.  
  
## <a name="closing-a-session"></a>Fechando uma sessão  
 Se o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Close%2A> método é chamado sem especificar o valor da *endSession* parâmetro, ou se o *endSession* parâmetro for definido como True, os dois a conexão à sessão e a sessão associado com o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> objeto está fechado. Para fechar uma sessão, o ADOMD.NET envia um cabeçalho `EndSession` XMLA ao provedor, com a ID de sessão definida como o valor da propriedade <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A>.  
  
 Se o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Close%2A> método for chamado com o *endSession* parâmetro definido como False, a sessão associada a <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> objeto permanece ativo, mas a conexão à sessão for fechada.  
  
## <a name="example-of-managing-a-session"></a>Exemplo de gerenciamento de uma sessão  
 O exemplo a seguir demonstra como abrir uma conexão, criar uma sessão e fechar a conexão mantendo-a aberta no ADOMD.NET:  
  
```vb  
Public Function CreateSession(ByVal connectionString As String) As String  
    Dim strSessionID As String = ""  
    Dim objConnection As New AdomdConnection  
  
    Try  
        ' First, try to connect to the specified data source.  
        ' If the connection string is not valid, or if the specified  
        ' provider does not support sessions, an exception is thrown.  
        objConnection.ConnectionString = connectionString  
        objConnection.Open()  
  
        ' Now that the connection is open, retrieve the new  
        ' active session ID.  
        strSessionID = objConnection.SessionID  
        ' Close the connection, but leave the session open.  
        objConnection.Close(False)  
        Return strSessionID  
  
    Finally  
        objConnection = Nothing  
    End Try  
End Function  
```  
  
```csharp  
static string CreateSession(string connectionString)  
{  
    string strSessionID = "";  
    AdomdConnection objConnection = new AdomdConnection();  
    try  
    {  
        /*First, try to connect to the specified data source.  
          If the connection string is not valid, or if the specified  
          provider does not support sessions, an exception is thrown. */  
        objConnection.ConnectionString = connectionString;  
        objConnection.Open();  
  
        // Now that the connection is open, retrieve the new  
        // active session ID.  
        strSessionID = objConnection.SessionID;  
        // Close the connection, but leave the session open.  
        objConnection.Close(false);  
        return strSessionID;  
    }  
    finally  
    {  
        objConnection = null;  
    }  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Estabelecendo conexões no ADOMD.NET](connections-in-adomd-net.md)  
  
  
