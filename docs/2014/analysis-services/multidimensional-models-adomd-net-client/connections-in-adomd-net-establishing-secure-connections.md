---
title: Estabelecendo conexões seguras no ADOMD.NET | Microsoft Docs
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
- connections [ADOMD.NET]
- security [ADOMD.NET]
ms.assetid: b084d447-1456-45a4-8e0e-746c07d7d6fd
caps.latest.revision: 40
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d97079ca400d92502cf3ff217137eb6f32d1920d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37180853"
---
# <a name="establishing-secure-connections-in-adomdnet"></a>Estabelecendo conexões seguras no ADOMD.NET
  Quando você usa uma conexão no ADOMD.NET, o método de segurança usado para a conexão dependerá do valor da propriedade `ProtectionLevel` da cadeia de conexão usada durante a chamada do método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A> de <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>.  
  
 A propriedade `ProtectionLevel` oferece quatro níveis de segurança: não autenticado, autenticado, assinado e criptografado. A tabela a seguir descreve esses vários níveis de segurança.  
  
> [!NOTE]  
>  Se você optar por usar o pooling de conexões de banco de dados, o banco de dados não será capaz de gerenciar a segurança. Isso acontece porque o pooling de conexões de banco de dados exige que a cadeia de conexão seja idêntica para a criação do conexões. Dessa forma, você deve gerenciar a segurança em outro lugar.  
  
|Nível de segurança|Valor de ProtectionLevel|  
|--------------------|---------------------------|  
|*conexão não autenticada*<br /> Uma conexão não autenticada não faz nenhuma forma de autenticação. Esse tipo de conexão representa a forma de conexão mais suportada, mas também a menos segura.|`None`|  
|*conexão autenticada*<br /> Uma conexão autenticada autentica o usuário que está fazendo a conexão, mas não protege comunicações adicionais. Esse tipo de conexão é útil para que você possa estabelecer a identidade do usuário ou do aplicativo que estiver se conectando a uma fonte de dados analíticos.|`Connect`|  
|*conexão assinada*<br /> Uma conexão assinada autentica o usuário que está solicitando a conexão e garante que as transmissões não serão modificadas. Esse tipo de conexão é útil quando a autenticidade dos dados transferidos deve ser verificada. No entanto, uma conexão assinada só impede a modificação do conteúdo do pacote de dados. Ele ainda poderá ser exibido em trânsito. **Observação:** uma conexão assinada só é suportada pelo provedor XML for Analysis fornecido pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|`Pkt Integrity` ou `PktIntegrity`|  
|*conexão criptografada*<br /> Uma conexão criptografada é o tipo de conexão padrão usado pelo ADOMD.NET. Esse tipo de conexão autentica o usuário que está solicitando a conexão e então também criptografa os dados transmitidos. Uma conexão criptografada é a forma mais segura de conexão que pode ser criada pelo ADOMD.NET. O conteúdo do pacote de dados não pode ser exibido ou modificado, protegendo assim os dados durante o trânsito. **Observação:** uma conexão criptografada só é suportada pelo provedor XML for Analysis fornecido pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|`Pkt Privacy` ou `PktPrivacy`|  
  
 No entanto, nem todos os níveis de segurança estão disponíveis para todos os tipos de conexões:  
  
-   Uma conexão TCP pode usar qualquer um dos quatro níveis de segurança. Na verdade, uma conexão TCP, quando usada com a com Segurança Integrada do Windows, oferece o método mais seguro de conexão a uma fonte de dados analíticos.  
  
-   Uma conexão HTTP só pode ser do tipo autenticada. Dessa forma, a propriedade `ProtectionLevel` deve ser definida como `Connect`.  
  
-   Uma conexão HTTPS só pode ser do tipo criptografada. Dessa forma, a propriedade `ProtectionLevel` deve ser definida como `Pkt Privacy` ou `PktPrivacy`.  
  
## <a name="securing-tcp-connections"></a>Protegendo conexões TCP  
 Para uma conexão TCP, a propriedade `ProtectionLevel` dá suporte a todos os quatro níveis de segurança, como mostrado na tabela a seguir.  
  
|Valor de ProtectionLevel|Usar com conexão TCP?|Resultados|  
|---------------------------|------------------------------|-------------|  
|`None`|Sim|Especifica uma conexão não autenticada.<br /><br /> Um fluxo TCP é solicitado do provedor, mas não há nenhuma forma de autenticação executada no usuário que está solicitando o fluxo.|  
|`Connect`|Sim|Especifica uma conexão autenticada.<br /><br /> Um fluxo TCP é solicitado do provedor e, em seguida, o contexto de segurança do usuário que está solicitando o fluxo é autenticado no servidor:<br /><br /> -Se a autenticação for bem-sucedida, nenhuma outra ação é executada.<br />-Se a autenticação falhar, o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> desconecta do objeto de fonte de dados multidimensional e uma exceção será lançada.<br /><br /> Depois que a autenticação tiver êxito ou falhar, o contexto de segurança usado para autenticar a conexão será descartado.|  
|`Pkt Integrity` ou `PktIntegrity`|Sim|Especifica uma conexão assinada.<br /><br /> Um fluxo TCP é solicitado do provedor e, em seguida, o contexto de segurança do usuário que está solicitando o fluxo é autenticado no servidor:<br /><br /> -Se a autenticação for bem-sucedida, o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> objeto fecha o fluxo TCP existente e abre um fluxo TCP assinado para manipular todas as solicitações. Cada solicitação de dados ou de metadados é autenticada por meio do contexto de segurança usado para abrir a conexão. Adicionalmente, cada pacote é assinado digitalmente para garantir que a carga do pacote TCP não tenha sido alterada de qualquer forma.<br />-Se a autenticação falhar, o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> desconecta do objeto de fonte de dados multidimensional e uma exceção será lançada.|  
|`Pkt Privacy` ou `PktPrivacy`|Sim|Especifica uma conexão criptografada. **Observação:** você também pode especificar uma conexão criptografada não definindo a `ProtectionLevel` propriedade na cadeia de conexão. <br /><br /> Um fluxo TCP é solicitado do provedor e o contexto de segurança do usuário que está solicitando o fluxo é autenticado no servidor:<br /><br /> -Se a autenticação for bem-sucedida, o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> objeto fecha o fluxo TCP existente e abrirá um fluxo TCP criptografado para manipular todas as solicitações. Cada solicitação de dados ou de metadados é autenticada por meio do contexto de segurança usado para abrir a conexão. Adicionalmente, a carga de cada pacote TCP será criptografada usando o maior método de criptografia suportado pelo provedor e pela fonte de dados multidimensional.<br />-Se a autenticação falhar, o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> desconecta do objeto de fonte de dados multidimensional e uma exceção será lançada.|  
  
### <a name="using-windows-integrated-security-for-the-connection"></a>Usando a Segurança Integrada do Windows para a conexão  
 A Segurança Integrada do Windows e a forma mais segura de estabelecer e de proteger uma conexão a uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. A Segurança Integrada do Windows não revela credenciais de segurança, como um nome de usuário e senha, durante o processo de autenticação, mas usa o identificador de segurança do processo em execução para estabelecer a identidade. Para a maioria dos aplicativos cliente, esse identificador de segurança representa a identidade do usuário atualmente conectado.  
  
 Para usar a Segurança Integrada do Windows, a cadeia de conexão exige as seguintes configurações:  
  
-   Para a propriedade `Integrated Security`, não defina essa propriedade ou a defina como `SSPI`.  
  
    > [!NOTE]  
    >  A Segurança Integrada do Windows só está disponível para conexões TCP, já que as conexões HTTP devem usar a configuração `Basic` para a propriedade `Integrated Security`.  
  
-   Para a propriedade `ProtectionLevel`, defina-a como `Connect`, `Pkt Integrity` ou `Pkt Privacy`.  
  
## <a name="securing-http-connections"></a>Protegendo conexões HTTP  
 HTTPS e SSL (Secure Sockets Layer) podem ser usados para a proteção externa das comunicações HTTP seguras com uma fonte de dados analíticos.  
  
 Como um provedor de XMLA só usa o HTTP seguro, uma conexão HTTP no ADOMD.NET deve ser assinada, como mostrado na tabela a seguir.  
  
|Valor de ProtectionLevel|Usar com HTTP ou HTTPS|  
|---------------------------|----------------------------|  
|`None`|não|  
|`Connect`|HTTP|  
|`Pkt Integrity` ou `PktIntegrity`|não|  
|`Pkt Privacy` ou `PktPrivacy`|HTTPS|  
  
### <a name="opening-a-secure-http-connection"></a>Abrindo uma conexão HTTP segura  
 O exemplo a seguir demonstra como usar o ADOMD.NET para abrir uma conexão HTTP para o banco de dados de exemplo `AdventureWorksAS` do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:  
  
```vb  
Public Function GetAWEncryptedConnection( _  
    Optional ByVal serverName As String = "https:\\localhost\isapy\msmdpump.dll") _  
    As AdomdConnection  
  
    Dim strConnectionString As String = ""  
    Dim objConnection As New AdomdConnection  
  
    Try  
        ' To establish an encrypted connection, set the   
        ' ProtectionLevel setting to PktPrivacy.  
        strConnectionString = "DataSource=" & serverName & ";" & _  
            "Catalog=AdventureWorksAS;" & _  
            "ProtectionLevel=PktPrivacy;"  
  
        ' Note that username and password are not supplied here.  
        ' The current security context is used for authentication  
        ' purposes.  
  
        objConnection.ConnectionString = strConnectionString  
        objConnection.Open()  
    Catch ex As Exception  
        objConnection = Nothing  
        Throw ex  
    Finally  
        ' Return the encrypted connection.  
        GetAWEncryptedConnection = objConnection  
    End Try  
End Function  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Estabelecendo conexões no ADOMD.NET](connections-in-adomd-net.md)  
  
  
