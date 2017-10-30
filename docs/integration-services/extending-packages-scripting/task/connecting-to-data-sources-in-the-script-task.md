---
title: Conectando-se a fontes de dados na tarefa Script | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- connections [Integration Services], scripts
- Integration Services packages, connections
- connection managers [Integration Services], scripts
- scripts [Integration Services], connections
- SSIS packages, connections
- packages [Integration Services], connections
- Script task [Integration Services], connections
- Connections property
- SQL Server Integration Services packages, connections
- SSIS Script task, connections
ms.assetid: 9c008380-715b-455b-9da7-22572d67c388
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 825ff059476614085a338dd9c568031885bed64b
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="connecting-to-data-sources-in-the-script-task"></a>Conectando a fontes de dados na tarefa Script
  Gerenciadores de conexões fornecem acesso a fontes de dados que foram configuradas no pacote. Para obter mais informações, consulte [Integration Services &#40;SSIS&#41; Conexões](../../../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
 A tarefa de Script pode acessar esses gerenciadores de conexão por meio de <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> propriedade o **Dts** objeto. Cada gerenciador de conexões na coleção <xref:Microsoft.SqlServer.Dts.Runtime.Connections> armazena informações sobre como conectar-se à fonte de dados subjacente.  
  
 Quando você chama o método <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> de um gerenciador de conexões, este se conecta à fonte de dados, se já não estiver conectado, e retorna a conexão apropriada ou as informações da conexão para você utilizar no código da tarefa Script.  
  
> [!NOTE]  
>  Você deve saber o tipo de conexão retornado pelo Gerenciador de conexão antes de chamar **AcquireConnection**. Como a tarefa de Script foi **Option Strict** habilitado, você deve converter a conexão, o que é retornado como tipo **objeto**, para o tipo de conexão apropriado antes de você pode usá-lo.  
  
 É possível usar o método <xref:Microsoft.SqlServer.Dts.Runtime.Connections.Contains%2A> da coleção <xref:Microsoft.SqlServer.Dts.Runtime.Connections> retornada pela propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> para procurar uma conexão existente antes de usá-la no seu código.  
  
> [!IMPORTANT]  
>  Não é possível chamar o método AcquireConnection de gerenciadores de conexão que retornam objetos não gerenciados, como o Gerenciador de conexão OLE DB e o Gerenciador de conexão do Excel, no código gerenciado de uma tarefa de Script. No entanto, você pode ler a propriedade ConnectionString desses gerenciadores de conexão e se conectar à fonte de dados diretamente em seu código usando a cadeia de caracteres de conexão com um **OledbConnection** do **OLEDB** namespace.  
>   
>  Se você deve chamar o método AcquireConnection de uma conexão Gerenciador que retorna um objeto não gerenciado, use um [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] Gerenciador de conexão. Quando você configura o gerenciador de conexões [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] para usar um provedor OLE DB, ele se conecta usando o Provedor de Dados [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] para OLE DB. Nesse caso, o método AcquireConnection retorna um **OleDbConnection** em vez de um objeto não gerenciado. Para configurar um [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] Gerenciador de conexão para uso com uma fonte de dados do Excel, selecione o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] OLE DB Provider for Jet, especifique um arquivo do Excel e insira `Excel 8.0` (para o Excel 97 e posterior) como o valor de **propriedades estendidas** no **todos os** página do **Gerenciador de Conexão** caixa de diálogo.  
  
## <a name="connections-example"></a>Exemplo de conexões  
 O exemplo seguinte demonstra como acessar gerenciadores de conexões da tarefa Script. O exemplo supõe que você criou e configurou um [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] Gerenciador de conexão denominado **teste ADO.NET Conexão** e um Gerenciador de conexão de arquivo simples nomeado **Conexão de arquivo simples de teste**. Observe que o [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] Gerenciador de conexão retorna um **SqlConnection** objeto que você pode usar imediatamente para se conectar à fonte de dados. Por outro lado, o gerenciador de conexões de arquivo simples retorna só uma cadeia de caracteres que contém o caminho e o nome do arquivo. Você deve usar métodos do **System.IO** namespace para abrir e trabalhar com o arquivo simples.  
  
```vb  
Public Sub Main()  
  
    Dim myADONETConnection As SqlClient.SqlConnection  
    myADONETConnection = _  
        DirectCast(Dts.Connections("Test ADO.NET Connection").AcquireConnection(Dts.Transaction), _  
        SqlClient.SqlConnection)  
    MsgBox(myADONETConnection.ConnectionString, _  
        MsgBoxStyle.Information, "ADO.NET Connection")  
  
    Dim myFlatFileConnection As String  
    myFlatFileConnection = _  
        DirectCast(Dts.Connections("Test Flat File Connection").AcquireConnection(Dts.Transaction), _  
        String)  
    MsgBox(myFlatFileConnection, MsgBoxStyle.Information, "Flat File Connection")  
  
    Dts.TaskResult = ScriptResults.Success  
  
End Sub  
```  
  
```csharp  
using System;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Dts.Runtime;  
using System.Windows.Forms;  
  
public class ScriptMain  
{  
  
        public void Main()  
        {  
            SqlConnection myADONETConnection = new SqlConnection();  
            myADONETConnection = (SqlConnection)(Dts.Connections["Test ADO.NET Connection"].AcquireConnection(Dts.Transaction)as SqlConnection);  
            MessageBox.Show(myADONETConnection.ConnectionString, "ADO.NET Connection");  
  
            string myFlatFileConnection;  
            myFlatFileConnection = (string)(Dts.Connections["Test Flat File Connection"].AcquireConnection(Dts.Transaction) as String);  
            MessageBox.Show(myFlatFileConnection, "Flat File Connection");  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
  
}  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Integration Services &#40; SSIS &#41; Conexões](../../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [Criar gerenciadores de Conexão](http://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)  
  
  

