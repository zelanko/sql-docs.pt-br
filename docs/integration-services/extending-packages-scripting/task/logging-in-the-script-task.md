---
title: Registro em log na tarefa Script | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- SQL Server Integration Services packages, logs
- SSIS packages, logs
- logs [Integration Services], scripts
- Integration Services packages, logs
- Log method
- SSIS Script task, logs
- Script task [Integration Services], logs
- packages [Integration Services], logs
ms.assetid: 2e11fc15-df18-4309-bd2d-fc58aa4b9b7a
caps.latest.revision: 57
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 98859dafe0b023954f10239fe11e8b76f36ab28b
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="logging-in-the-script-task"></a>Registrando a tarefa Script
  O uso de log em pacotes do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] permite que você grave informações detalhadas sobre o progresso da execução, resultados e problemas, por meio do registro de eventos predefinidos ou mensagens definidas pelo usuário para análise posterior. A tarefa de Script pode usar o <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> método o **Dts** objeto para registrar dados definidos pelo usuário. Se o log estiver habilitado e o **ScriptTaskLogEntry** evento é selecionado para o logon de **detalhes** guia do **configurar Logs de SSIS** caixa de diálogo, uma única chamada para o <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> método armazena as informações de evento em todos os provedores de log configurados para a tarefa.  
  
> [!NOTE]  
>  Embora seja possível executar o registro em log diretamente da tarefa Script, talvez você queira implementar eventos em vez de registrá-los. Ao utilizar eventos, você pode habilitar o registro de mensagens de eventos e também responder ao evento com manipuladores de eventos padrão ou definidos pelo usuário.  
  
 Para obter mais informações sobre registro em log, consulte [Integration Services &#40; SSIS &#41; Registro em log](../../../integration-services/performance/integration-services-ssis-logging.md).  
  
## <a name="logging-example"></a>Exemplo de registro em log  
 O exemplo a seguir demonstra o registro em log da tarefa Script, em que o valor registrado representa o número de linhas processadas.  
  
```vb  
Public Sub Main()  
  
    Dim rowsProcessed As Integer = 100  
    Dim emptyBytes(0) As Byte  
  
    Try  
        Dts.Log("Rows processed: " & rowsProcessed.ToString, _  
            0, _  
            emptyBytes)  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        'An error occurred.  
        Dts.Events.FireError(0, "Script Task Example", _  
            ex.Message & ControlChars.CrLf & ex.StackTrace, _  
            String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
```  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.SqlServer.Dts.Runtime;  
  
public class ScriptMain  
{  
  
    public void Main()  
        {  
            //  
            int rowsProcessed = 100;  
            byte[] emptyBytes = new byte[0];  
  
            try  
            {  
                Dts.Log("Rows processed: " + rowsProcessed.ToString(), 0, emptyBytes);  
                Dts.TaskResult = (int)ScriptResults.Success;  
            }  
            catch (Exception ex)  
            {  
                //An error occurred.  
                Dts.Events.FireError(0, "Script Task Example", ex.Message + "\r" + ex.StackTrace, String.Empty, 0);  
                Dts.TaskResult = (int)ScriptResults.Failure;  
            }  
  
        }  
```  
  
 }  
  
## <a name="external-resources"></a>Recursos externos  
  
-   Entrada de blog, [log de eventos personalizados para tarefas do Integration Services](http://go.microsoft.com/fwlink/?LinkId=165644), em dougbert.com  
  
## <a name="see-also"></a>Consulte também  
 [Integration Services &#40; SSIS &#41; Registro em log](../../../integration-services/performance/integration-services-ssis-logging.md)  
  
  

