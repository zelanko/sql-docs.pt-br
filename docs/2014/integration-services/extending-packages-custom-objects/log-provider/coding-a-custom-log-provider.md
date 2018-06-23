---
title: Codificar um provedor de logs personalizado | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- custom log providers [Integration Services], coding
ms.assetid: 979a29ca-956e-4fdd-ab47-f06e84cead7a
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: bb07f9cffabd0d01eff069e317410c1a016ad370
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118376"
---
# <a name="coding-a-custom-log-provider"></a>Codificando um provedor de log personalizado
  Depois de criar uma classe que herda da classe base <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase> e aplicar o atributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> a essa classe, você deve substituir a implementação das propriedades e dos métodos da classe base para fornecer sua funcionalidade personalizada.  
  
 Para amostras funcionais de provedores de logs personalizados, consulte [Desenvolver uma interface do usuário para um provedor de logs personalizado](developing-a-user-interface-for-a-custom-log-provider.md).  
  
## <a name="configuring-the-log-provider"></a>Configurando o provedor de log  
  
### <a name="initializing-the-log-provider"></a>Inicializando o provedor de log  
 Você substitui o método <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.InitializeLogProvider%2A> para armazenar em cache as referências à coleção de conexões e à interface de eventos. Você poderá usar essas referências armazenadas em cache posteriormente em outros métodos do provedor de log.  
  
### <a name="using-the-configstring-property"></a>Utilizando a propriedade ConfigString  
 Em tempo de design, um provedor de logs recebe informações de configuração da coluna **Configuração**. Essas informações de configuração correspondem à propriedade <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A> do provedor de log. Por padrão, esta coluna contém uma caixa de texto da qual você pode recuperar informações de cadeia de caracteres. A maioria dos provedores de log fornecida com o [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] usa essa propriedade para armazenar o nome do gerenciador de conexões que o provedor usa para se conectar com uma fonte de dados externa. Se o provedor de logs usar a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A>, use o método <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Validate%2A> para validar essa propriedade e verificar se ela está definida corretamente.  
  
### <a name="validating-the-log-provider"></a>Validando o provedor de log.  
 Substitua o método <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Validate%2A> para verificar se o provedor foi configurado corretamente e se está pronto para execução. Normalmente, um nível mínimo de validação é para verificar se a <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A> está definida corretamente. A execução não pode continuar até que o provedor de log retorne <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult.Success> do método <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Validate%2A>.  
  
 O exemplo de código a seguir mostra uma implementação de <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Validate%2A> que verifica se o nome do gerenciador de conexões está especificado, se o gerenciador de conexões existe no pacote e se ele retorna um nome de arquivo na propriedade <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A>.  
  
```csharp  
public override DTSExecResult Validate(IDTSInfoEvents infoEvents)  
{  
    if (this.ConfigString.Length == 0 || connections.Contains(ConfigString) == false)  
    {  
        infoEvents.FireError(0, "MyTextLogProvider", "The ConnectionManager " + ConfigString + " specified in the ConfigString property cannot be found in the collection.", "", 0);  
        return DTSExecResult.Failure;  
    }  
    else  
    {  
        string fileName = connections[ConfigString].AcquireConnection(null) as string;  
  
        if (fileName == null || fileName.Length == 0)  
        {  
            infoEvents.FireError(0, "MyTextLogProvider", "The ConnectionManager " + ConfigString + " specified in the ConfigString property cannot be found in the collection.", "", 0);  
            return DTSExecResult.Failure;  
        }  
    }  
    return DTSExecResult.Success;  
}  
```  
  
```vb  
Public Overrides Function Validate(ByVal infoEvents As IDTSInfoEvents) As DTSExecResult  
    If Me.ConfigString.Length = 0 Or connections.Contains(ConfigString) = False Then  
        infoEvents.FireError(0, "MyTextLogProvider", "The ConnectionManager " + ConfigString + " specified in the ConfigString property cannot be found in the collection.", "", 0)  
        Return DTSExecResult.Failure  
    Else   
        Dim fileName As String =  connections(ConfigString).AcquireConnectionCType(as string, Nothing)  
  
        If fileName = Nothing Or fileName.Length = 0 Then  
            infoEvents.FireError(0, "MyTextLogProvider", "The ConnectionManager " + ConfigString + " specified in the ConfigString property cannot be found in the collection.", "", 0)  
            Return DTSExecResult.Failure  
        End If  
    End If  
    Return DTSExecResult.Success  
End Function  
```  
  
### <a name="persisting-the-log-provider"></a>Persistência do provedor de log  
 Normalmente você não tem que implementar a persistência personalizada em um gerenciador de conexões. A persistência personalizada é necessária somente quando as propriedades de um objeto usam tipos de dados complexos. Para obter mais informações, consulte [Desenvolvendo objetos personalizados para o Integration Services](../developing-custom-objects-for-integration-services.md).  
  
## <a name="logging-with-the-log-provider"></a>Registrando em log com o provedor de log  
 Há três métodos de tempo de execução que devem ser substituídos por todos os provedores de log: <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A> e <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A>.  
  
> [!IMPORTANT]  
>  Durante a validação e execução de um único pacote, são chamados os métodos <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A> e <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A> mais de uma vez. Verifique se seu código personalizado não faz com que as entradas de log anteriores sejam substituídas pela próxima abertura e fechamento de log. Se você optou por registrar em log os eventos de validação em seu pacote de teste, o primeiro evento registrado que deverá ver é o OnPreValidate. Se, em vez disso, o primeiro evento registrado que você visualizar for o PackageStart, os eventos de validação iniciais foram substituídos.  
  
### <a name="opening-the-log"></a>Abrindo o log  
 A maioria dos provedores de log se conecta a fontes de dados externas, como um arquivo ou banco de dados, para armazenar as informações do evento coletadas durante a execução do pacote. Como com qualquer outro objeto no tempo de execução, a conexão com a fonte de dados externa normalmente é realizada por meio de objetos do gerenciador de conexões.  
  
 O método <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A> é chamado no início da execução do pacote. Substitua esse método para estabelecer uma conexão com a fonte de dados externa.  
  
 O código de exemplo seguinte mostra um provedor de log que abre um arquivo de texto para gravação durante o <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A>. Ele abre o arquivo chamando o método <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> do gerenciador de conexões que foi especificado na propriedade <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A>.  
  
```csharp  
public override void OpenLog()  
{  
    if(!this.connections.Contains(this.ConfigString))  
        throw new Exception("The ConnectionManager " + this.ConfigString + " does not exist in the Connections collection.");  
  
    this.connectionManager = connections[ConfigString];  
    string filePath = this.connectionManager.AcquireConnection(null) as string;  
  
    if(filePath == null || filePath.Length == 0)  
        throw new Exception("The ConnectionManager " + this.ConfigString + " is not a valid FILE ConnectionManager");  
  
    //  Create a StreamWriter to append to.  
    sw = new StreamWriter(filePath,true);  
  
    sw.WriteLine("Open log" + System.DateTime.Now.ToShortTimeString());  
}  
```  
  
```vb  
Public Overrides  Sub OpenLog()  
    If Not Me.connections.Contains(Me.ConfigString) Then  
        Throw New Exception("The ConnectionManager " + Me.ConfigString + " does not exist in the Connections collection.")  
    End If  
  
    Me.connectionManager = connections(ConfigString)  
    Dim filePath As String =  Me.connectionManager.AcquireConnectionCType(as string, Nothing)  
  
    If filePath = Nothing Or filePath.Length = 0 Then  
        Throw New Exception("The ConnectionManager " + Me.ConfigString + " is not a valid FILE ConnectionManager")  
    End If  
  
    '  Create a StreamWriter to append to.  
    sw = New StreamWriter(filePath,True)  
  
    sw.WriteLine("Open log" + System.DateTime.Now.ToShortTimeString())  
End Sub  
```  
  
### <a name="writing-log-entries"></a>Gravando entradas de log  
 O método <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A> é chamado sempre que um objeto no pacote gera um evento chamando-se um método Fire\<evento> em uma das interfaces do evento. Cada evento normalmente é gerado com informações sobre seu contexto e uma mensagem explicativa. Entretanto, nem toda chamada para o método <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A> inclui informações de cada parâmetro do método. Por exemplo, alguns eventos padrão cujos nomes são autoexplicativos não fornecem MessageText e DataCode e DataBytes são destinados para informações suplementares opcionais.  
  
 O exemplo de código seguinte implementa o método <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A> e grava os eventos no fluxo que foi aberto na seção anterior.  
  
```csharp  
public override void Log(string logEntryName, string computerName, string operatorName, string sourceName, string sourceID, string executionID, string messageText, DateTime startTime, DateTime endTime, int dataCode, byte[] dataBytes)  
{  
    sw.Write(logEntryName + ",");  
    sw.Write(computerName + ",");  
    sw.Write(operatorName + ",");  
    sw.Write(sourceName + ",");  
    sw.Write(sourceID + ",");  
    sw.Write(messageText + ",");  
    sw.Write(dataBytes + ",");  
    sw.WriteLine("");  
}  
```  
  
```vb  
Public Overrides  Sub Log(ByVal logEnTryName As String, ByVal computerName As String, ByVal operatorName As String, ByVal sourceName As String, ByVal sourceID As String, ByVal executionID As String, ByVal messageText As String, ByVal startTime As DateTime, ByVal endTime As DateTime, ByVal dataCode As Integer, ByVal dataBytes() As Byte)  
    sw.Write(logEnTryName + ",")  
    sw.Write(computerName + ",")  
    sw.Write(operatorName + ",")  
    sw.Write(sourceName + ",")  
    sw.Write(sourceID + ",")  
    sw.Write(messageText + ",")  
    sw.Write(dataBytes + ",")  
    sw.WriteLine("")  
End Sub  
```  
  
### <a name="closing-the-log"></a>Fechando o log  
 O método <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A> é chamado no final da execução do pacote, depois que todos os objetos do pacote concluíram a execução ou quando o pacote para devido a erros.  
  
 O exemplo de código a seguir demonstra uma implementação do método <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A> que fecha o fluxo de arquivos aberto durante o método <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A>.  
  
```csharp  
public override void CloseLog()  
{  
    if (sw != null)  
    {  
        sw.WriteLine("Close log" + System.DateTime.Now.ToShortTimeString());  
        sw.Close();  
    }  
}  
```  
  
```vb  
Public Overrides  Sub CloseLog()  
    If Not sw Is Nothing Then  
        sw.WriteLine("Close log" + System.DateTime.Now.ToShortTimeString())  
        sw.Close()  
    End If  
End Sub  
```  
  
![Ícone do Integration Services (pequeno)](../../media/dts-16.gif "ícone do Integration Services (pequeno)")**permanecer acima para data com o Integration Services** <br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte também  
 [Criar um provedor de logs personalizado](creating-a-custom-log-provider.md)   
 [Desenvolver uma interface do usuário para um provedor de logs personalizado](developing-a-user-interface-for-a-custom-log-provider.md)  
  
  