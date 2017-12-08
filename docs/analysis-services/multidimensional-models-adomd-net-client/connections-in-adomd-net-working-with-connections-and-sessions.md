---
title: "Trabalhando com conexões e sessões no ADOMD.NET | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- sessions [ADOMD.NET]
- connections [ADOMD.NET]
ms.assetid: 72b43c06-f3e4-42c3-a696-4a3419c3b884
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 061a51539b40630874e36096cc59557ac375c671
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="connections-in-adomdnet---working-with-connections-and-sessions"></a>Conexões no ADOMD.NET - trabalhar com conexões e sessões
  No XMLA (XML for Analysis), sessões dão suporte a operações de estado durante o acesso a dados analíticos. As sessões enquadram o escopo e o contexto de comandos e de transações para uma fonte de dados analíticos. Os elementos XMLA usados para gerenciar sessões são [BeginSession](../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md), [Session](../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md)e [EndSession](../../analysis-services/xmla/xml-elements-headers/endsession-element-xmla.md).  
  
 O ADOMD.NET usa esses três elementos de sessão XMLA quando você inicia uma sessão, executa consultas ou recupera dados durante a sessão e fecha uma sessão.  
  
## <a name="starting-a-session"></a>Iniciando uma sessão  
 A propriedade <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> do objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> contém o identificador da sessão ativa associada ao objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>. Ao usar essa propriedade corretamente, você poderá controlar efetivamente a capacidade de manutenção de status do processo de cliente e de servidor em seu aplicativo:  
  
-   Se a propriedade <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> não for definida para uma ID de sessão válida quando o método de <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A> for chamado, o objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> solicitará uma nova ID de sessão do provedor. O ADOMD.NET inicia uma sessão enviando um cabeçalho **BeginSession** XMLA ao provedor. Se o ADOMD.NET tiver êxito em iniciar uma sessão, o ADOMD.NET definirá o valor da propriedade de <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> para a ID de sessão da sessão recém-criada.  
  
-   Se a propriedade <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> não for definida para uma ID de sessão válida quando o método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A> for chamado, o objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> tentará se conectar à sessão especificada.  
  
 Se o objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> não puder se conectar à sessão especificada, ou se o provedor não der suporte a sessões, uma exceção será lançada.  
  
> [!NOTE]  
>  Depois de fazer o ADOMD.NET criar uma sessão, você poderá conectar vários objetos de <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> a essa sessão ativa única ou poderá desconectar um único objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> dessa sessão e reconectá-lo a outra sessão.  
  
## <a name="working-in-a-session"></a>Trabalhando em uma sessão  
 Depois que o ADOMD.NET conecta o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> o objeto para uma sessão válida, enviará um XMLA **sessão** cabeçalho para o provedor com todas as solicitações de dados ou metadados feitas por um aplicativo. Todas as solicitações terão a ID de sessão definida como o valor da propriedade de <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A>.  
  
 Uma ID de sessão não garante que uma sessão permanecerá válida. Se a sessão expirar (por exemplo, se o tempo limite da sessão for alcançado ou se a conexão for interrompida), o provedor poderá optar por encerrar e reverter as ações dessa sessão. Se isso ocorrer, todas as chamadas método subsequentes do objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> lançarão uma exceção. Como as exceções são lançadas somente quando a próxima solicitação é enviada ao provedor, e não quando a sessão expira, o seu aplicativo deve ser capaz de manipulá-las sempre que o seu aplicativo recuperar dados ou metadados do provedor.  
  
## <a name="closing-a-session"></a>Fechando uma sessão  
 Se o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Close%2A> método for chamado sem especificar o valor da *endSession* parâmetro, ou se o *endSession* parâmetro for definido como True, os dois a conexão à sessão e a sessão associado a <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> objeto está fechado. Para fechar uma sessão, o ADOMD.NET envia um XMLA **EndSession** cabeçalho para o provedor, com a ID de sessão é definida como o valor da <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> propriedade.  
  
 Se o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Close%2A> método for chamado com o *endSession* parâmetro definido como False, a sessão associada a <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> objeto permanecerá ativo, mas a conexão para a sessão é fechada.  
  
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
 [Estabelecendo conexões no ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net.md)  
  
  
