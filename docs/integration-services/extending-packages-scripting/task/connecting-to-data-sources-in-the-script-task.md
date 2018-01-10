---
title: Conectar-se a fontes de dados na Tarefa Script | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
dev_langs: VB
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
caps.latest.revision: "59"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 76108d1b6c4004d85456b0f412874012b8d71228
ms.sourcegitcommit: 4aeedbb88c60a4b035a49754eff48128714ad290
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="connecting-to-data-sources-in-the-script-task"></a>Conectando a fontes de dados na tarefa Script
  Gerenciadores de conexões fornecem acesso a fontes de dados que foram configuradas no pacote. Para obter mais informações, consulte [Integration Services &#40;SSIS&#41; Conexões](../../../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
 A tarefa Script pode acessar esses gerenciadores de conexões pela propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> do objeto **Dts**. Cada gerenciador de conexões na coleção <xref:Microsoft.SqlServer.Dts.Runtime.Connections> armazena informações sobre como conectar-se à fonte de dados subjacente.  
  
 Quando você chama o método <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> de um gerenciador de conexões, este se conecta à fonte de dados, se já não estiver conectado, e retorna a conexão apropriada ou as informações da conexão para você utilizar no código da tarefa Script.  
  
> [!NOTE]  
>  Você deve saber o tipo de conexão retornado pelo gerenciador de conexões antes de chamar **AcquireConnection**. Já que a tarefa Script tem **Option Strict** habilitada, você deve converter a conexão, que é retornada como tipo **Object**, para o tipo de conexão adequado antes de poder usá-la.  
  
 É possível usar o método <xref:Microsoft.SqlServer.Dts.Runtime.Connections.Contains%2A> da coleção <xref:Microsoft.SqlServer.Dts.Runtime.Connections> retornada pela propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> para procurar uma conexão existente antes de usá-la no seu código.  
  
> [!IMPORTANT]  
>  Você não pode chamar o método AcquireConnection de gerenciadores de conexões que retornam objetos não gerenciados, tais como o gerenciador de conexões OLE DB e o Excel, no código gerenciado de uma tarefa Script. Entretanto, você pode ler a propriedade ConnectionString desses gerenciadores de conexões e conectar-se à fonte de dados diretamente em seu código por meio da cadeia de conexão com uma **OledbConnection** do namespace **System.Data.OleDb**.  
>   
>  Se você deve chamar o método AcquireConnection de um gerenciador de conexões que retorna um objeto não gerenciado, use um gerenciador de conexões [!INCLUDE[vstecado](../../../includes/vstecado-md.md)]. Quando você configura o gerenciador de conexões [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] para usar um provedor OLE DB, ele se conecta usando o Provedor de Dados [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] para OLE DB. Nesse caso, o método AcquireConnection retorna um **System.Data.OleDb.OleDbConnection** em vez de um objeto não gerenciado. Para configurar um gerenciador de conexões [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] para usar com uma fonte de dados Excel, selecione o OLE DB Provider for [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Jet, especifique um arquivo em Excel e insira `Excel 8.0` (para Excel 97 e mais recente) como valor de **Propriedades Estendidas** na página **Todas** da caixa de diálogo **Gerenciador de Conexões**.  
  
## <a name="connections-example"></a>Exemplo de conexões  
 O exemplo seguinte demonstra como acessar gerenciadores de conexões da tarefa Script. A amostra supõe que você criou e configurou um gerenciador de conexões [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] chamado denominado **Testar Conexão ADO.NET** e um gerenciador de conexões de arquivo simples denominado **Testar Conexão de Arquivo Simples**. Observe que o gerenciador de conexões [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] retorna um objeto **SqlConnection** que você pode usar imediatamente para se conectar à fonte de dados. Por outro lado, o gerenciador de conexões de arquivo simples retorna só uma cadeia de caracteres que contém o caminho e o nome do arquivo. Você deve usar métodos do namespace **System.IO** para abrir e funcionar com o arquivo simples.  
  
```vb  
    Public Sub Main()

        Dim myADONETConnection As SqlClient.SqlConnection =
            DirectCast(Dts.Connections("Test ADO.NET Connection").AcquireConnection(Dts.Transaction),
                SqlClient.SqlConnection)
        MsgBox(myADONETConnection.ConnectionString,
            MsgBoxStyle.Information, "ADO.NET Connection")

        Dim myFlatFileConnection As String =
            DirectCast(Dts.Connections("Test Flat File Connection").AcquireConnection(Dts.Transaction),
                String)
        MsgBox(myFlatFileConnection, MsgBoxStyle.Information, "Flat File Connection")

        Dts.TaskResult = ScriptResults.Success

    End Sub
```  
  
```csharp  
        public void Main()
        {
            SqlConnection myADONETConnection = 
                Dts.Connections["Test ADO.NET Connection"].AcquireConnection(Dts.Transaction)
                as SqlConnection;
            MessageBox.Show(myADONETConnection.ConnectionString, "ADO.NET Connection");

            string myFlatFileConnection = 
                Dts.Connections["Test Flat File Connection"].AcquireConnection(Dts.Transaction) 
                as string;
            MessageBox.Show(myFlatFileConnection, "Flat File Connection");

            Dts.TaskResult = (int)ScriptResults.Success;
        }
```  
  
## <a name="see-also"></a>Consulte Também  
 [Conexões do SSIS &#40;Integration Services&#41;](../../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [Criar Gerenciadores de Conexões](http://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)  
  
  
