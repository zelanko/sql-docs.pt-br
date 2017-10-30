---
title: Conectando-se a fontes de dados em uma tarefa personalizada | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ConnectionManager objects
- connection managers [Integration Services], external data sources
- data sources [Integration Services], external
- custom tasks [Integration Services], external data sources
- external data sources [Integration Services]
- connections [Integration Services], external data sources
- SSIS custom tasks, external data sources
ms.assetid: 9f0b3a43-3eaa-4b3c-bb08-29b630c11306
caps.latest.revision: 51
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 5b9446be2b632e6df78fbc1f66762de02d4644f5
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="connecting-to-data-sources-in-a-custom-task"></a>Conectando a fontes de dados em uma tarefa personalizada
  As tarefas conectam-se a fontes de dados externas para recuperar ou salvar dados por meio de um gerenciador de conexões. Em tempo de design, um gerenciador de conexões representa uma conexão lógica e descreve informações chave como o nome do servidor e qualquer propriedade de autenticação. Em tempo de execução, as tarefas chamam o método <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> do gerenciador de conexões para estabelecer a conexão física com a fonte de dados.  
  
 Como um pacote pode conter muitas tarefas, e cada uma dessas tarefas pode ter conexões com diferentes fontes de dados, o pacote rastreia todos os gerenciadores de conexões em uma coleção, a coleção <xref:Microsoft.SqlServer.Dts.Runtime.Connections>. As tarefas usam a coleção do pacote para localizar o gerenciador de conexões que elas usarão durante a validação e a execução. A coleção <xref:Microsoft.SqlServer.Dts.Runtime.Connections> é o primeiro parâmetro dos métodos <xref:Microsoft.SqlServer.Dts.Runtime.Task.Validate%2A> e <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A>.  
  
 Você pode impedir que a tarefa use o gerenciador de conexões errado exibindo os objetos <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> da coleção para o usuário, usando uma caixa de diálogo ou lista suspensa na interface gráfica do usuário. Isso dá ao usuário um modo de selecionar somente entre os objetos <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> do tipo apropriado que estão no pacote.  
  
 As tarefas chamam o método <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> para estabelecer a conexão física com a fonte de dados. O método retorna o objeto de conexão subjacente que, então, pode ser usado pela tarefa. Como o gerenciador de conexões isola os detalhes de implementação do objeto de conexão subjacente da tarefa, a tarefa tem que chamar somente o método <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> para estabelecer a conexão, e não tem que estar conectada a outros aspectos da conexão.  
  
## <a name="example"></a>Exemplo  
 O código de exemplo seguinte demonstra a validação do nome <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> nos métodos Validar e Executar, e mostra como usar o método <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> para estabelecer a conexão física no método Executar.  
  
```csharp  
private string connectionManagerName = "";  
  
public string ConnectionManagerName  
{  
  get { return this.connectionManagerName; }  
  set { this.connectionManagerName = value; }  
}  
  
public override DTSExecResult Validate(  
  Connections connections, VariableDispenser variableDispenser,  
  IDTSComponentEvents componentEvents, IDTSLogging log)  
{  
  // If the connection manager exists, validation is successful;  
  // otherwise, fail validation.  
  try  
  {  
    ConnectionManager cm = connections[this.connectionManagerName];  
    return DTSExecResult.Success;  
  }  
  catch (System.Exception e)  
  {  
    componentEvents.FireError(0, "SampleTask", "Invalid connection manager.", "", 0);  
    return DTSExecResult.Failure;  
  }  
}  
  
public override DTSExecResult Execute(Connections connections,   
  VariableDispenser variableDispenser, IDTSComponentEvents componentEvents,   
  IDTSLogging log, object transaction)  
{  
  try  
  {  
    ConnectionManager cm = connections[this.connectionManagerName];  
    object connection = cm.AcquireConnection(transaction);  
    return DTSExecResult.Success;  
  }  
  catch (System.Exception exception)  
  {  
    componentEvents.FireError(0, "SampleTask", exception.Message, "", 0);  
    return DTSExecResult.Failure;  
  }  
}  
```  
  
```vb  
Private _connectionManagerName As String = ""  
  
Public Property ConnectionManagerName() As String  
  Get  
    Return Me._connectionManagerName  
  End Get  
  Set(ByVal Value As String)  
    Me._connectionManagerName = value  
  End Set  
End Property  
  
Public Overrides Function Validate( _  
  ByVal connections As Microsoft.SqlServer.Dts.Runtime.Connections, _  
  ByVal variableDispenser As Microsoft.SqlServer.Dts.Runtime.VariableDispenser, _  
  ByVal componentEvents As Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents, _  
  ByVal log As Microsoft.SqlServer.Dts.Runtime.IDTSLogging) _  
  As Microsoft.SqlServer.Dts.Runtime.DTSExecResult  
  
  ' If the connection manager exists, validation is successful;  
  ' otherwise fail validation.  
  Try  
    Dim cm As ConnectionManager = connections(Me._connectionManagerName)  
    Return DTSExecResult.Success  
  Catch e As System.Exception  
    componentEvents.FireError(0, "SampleTask", "Invalid connection manager.", "", 0)  
    Return DTSExecResult.Failure  
  End Try  
  
End Function  
  
Public Overrides Function Execute( _  
  ByVal connections As Microsoft.SqlServer.Dts.Runtime.Connections, _  
  ByVal variableDispenser As Microsoft.SqlServer.Dts.Runtime.VariableDispenser, _  
  ByVal componentEvents As Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents, _  
  ByVal log As Microsoft.SqlServer.Dts.Runtime.IDTSLogging, ByVal transaction As Object) _  
  As Microsoft.SqlServer.Dts.Runtime.DTSExecResult  
  
  Try  
    Dim cm As ConnectionManager = connections(Me._connectionManagerName)  
    Dim connection As Object = cm.AcquireConnection(transaction)  
    Return DTSExecResult.Success  
  Catch exception As System.Exception  
    componentEvents.FireError(0, "SampleTask", exception.Message, "", 0)  
    Return DTSExecResult.Failure  
  End Try  
  
End Function  
```  
  
## <a name="see-also"></a>Consulte também  
 [Integration Services &#40; SSIS &#41; Conexões](../../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [Criar gerenciadores de Conexão](http://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)  
  
  

