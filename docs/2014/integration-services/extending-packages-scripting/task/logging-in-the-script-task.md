---
title: Registro em log na tarefa Script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e2ab23134ef193c4dfc17c901fc7d41e1af2083d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62768372"
---
# <a name="logging-in-the-script-task"></a>Registrando a tarefa Script
  O uso de log em pacotes do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] permite que você grave informações detalhadas sobre o progresso da execução, resultados e problemas, por meio do registro de eventos predefinidos ou mensagens definidas pelo usuário para análise posterior. A tarefa Script pode usar o método <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> do objeto `Dts` para registrar dados definidos pelo usuário. Se o registro em log estiver habilitado e o evento **ScriptTaskLogEntry** for selecionado para o registro na guia **Detalhes** da caixa de diálogo **Configurar Logs de SSIS**, uma única chamada ao método <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> armazenará as informações do evento em todos os provedores de log configurados para a tarefa.  
  
> [!NOTE]  
>  Embora seja possível executar o registro em log diretamente da tarefa Script, talvez você queira implementar eventos em vez de registrá-los. Ao utilizar eventos, você pode habilitar o registro de mensagens de eventos e também responder ao evento com manipuladores de eventos padrão ou definidos pelo usuário.  
  
 Para obter mais informações sobre registro em log, consulte [Log do SSIS &#40;Integration Services&#41;](../../performance/integration-services-ssis-logging.md).  
  
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
  
-   Entrada de blog [Logging custom events for Integration Services tasks](https://go.microsoft.com/fwlink/?LinkId=165644) (Registrando eventos personalizados para tarefas do Integration Services), em dougbert.com  
  
![Ícone de Integration Services (pequeno)](../../media/dts-16.gif "Ícone do Integration Services (pequeno)")  **Mantenha-se atualizado com Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte Também  
 [Registro em Log do SSIS &#40;Integration Services&#41;](../../performance/integration-services-ssis-logging.md)  
  
  
