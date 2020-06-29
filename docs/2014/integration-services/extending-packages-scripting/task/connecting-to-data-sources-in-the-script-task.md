---
title: Conectar-se a fontes de dados na Tarefa Script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 24013f8e0e60e7a441df09fc4ec5bd320318afe6
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85425943"
---
# <a name="connecting-to-data-sources-in-the-script-task"></a>Conectando a fontes de dados na tarefa Script
  Gerenciadores de conexões fornecem acesso a fontes de dados que foram configuradas no pacote. Para obter mais informações, consulte [Integration Services &#40;SSIS&#41; Conexões](../../connection-manager/integration-services-ssis-connections.md).  
  
 A tarefa Script pode acessar esses gerenciadores de conexões pela propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> do objeto **Dts**. Cada gerenciador de conexões na coleção <xref:Microsoft.SqlServer.Dts.Runtime.Connections> armazena informações sobre como conectar-se à fonte de dados subjacente.  
  
 Quando você chama o método <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> de um gerenciador de conexões, este se conecta à fonte de dados, se já não estiver conectado, e retorna a conexão apropriada ou as informações da conexão para você utilizar no código da tarefa Script.  
  
> [!NOTE]  
>  Você deve saber o tipo de conexão retornado pelo Gerenciador de conexões antes de chamar `AcquireConnection` . Como a tarefa Script tem `Option Strict` habilitada, você deve converter a conexão, que é retornada como tipo `Object`, para o tipo de conexão adequado antes de poder usá-lo.  
  
 É possível usar o método <xref:Microsoft.SqlServer.Dts.Runtime.Connections.Contains%2A> da coleção <xref:Microsoft.SqlServer.Dts.Runtime.Connections> retornada pela propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> para procurar uma conexão existente antes de usá-la no seu código.  
  
> [!IMPORTANT]  
>  Você não pode chamar o método AcquireConnection de gerenciadores de conexões que retornam objetos não gerenciados, tais como o gerenciador de conexões OLE DB e o Excel, no código gerenciado de uma tarefa Script. No entanto, você pode ler a propriedade ConnectionString desses gerenciadores de conexões e conectar-se à fonte de dados diretamente em seu código usando a cadeia de conexão com um `OledbConnection` do namespace **System. Data. OleDb** .  
>   
>  Se você deve chamar o método AcquireConnection de um gerenciador de conexões que retorna um objeto não gerenciado, use um gerenciador de conexões [!INCLUDE[vstecado](../../../includes/vstecado-md.md)]. Quando você configura o gerenciador de conexões [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] para usar um provedor OLE DB, ele se conecta usando o Provedor de Dados [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] para OLE DB. Nesse caso, o método AcquireConnection retorna um `System.Data.OleDb.OleDbConnection` em vez de um objeto não gerenciado. Para configurar um gerenciador de conexões [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] para usar com uma fonte de dados Excel, selecione o OLE DB Provider for [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Jet, especifique um arquivo em Excel e insira `Excel 8.0` (para Excel 97 e mais recente) como valor de **Propriedades Estendidas** na página **Todas** da caixa de diálogo **Gerenciador de Conexões**.  
  
## <a name="connections-example"></a>Exemplo de conexões  
 O exemplo seguinte demonstra como acessar gerenciadores de conexões da tarefa Script. A amostra supõe que você criou e configurou um gerenciador de conexões [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] chamado denominado **Testar Conexão ADO.NET** e um gerenciador de conexões de arquivo simples denominado **Testar Conexão de Arquivo Simples**. Observe que o gerenciador de conexões [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] retorna um objeto `SqlConnection` que você pode usar para se conectar à fonte de dados imediatamente. Por outro lado, o gerenciador de conexões de arquivo simples retorna só uma cadeia de caracteres que contém o caminho e o nome do arquivo. Você deve usar métodos do namespace `System.IO` para abrir e funcionar com o arquivo simples.  
  
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
  
![Ícone de Integration Services (pequeno)](../../media/dts-16.gif "Ícone do Integration Services (pequeno)")  **Mantenha-se atualizado com Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services &#40;conexões&#41; SSIS](../../connection-manager/integration-services-ssis-connections.md)   
 [Criar gerenciadores de conexões](../../create-connection-managers.md)  
  
  
