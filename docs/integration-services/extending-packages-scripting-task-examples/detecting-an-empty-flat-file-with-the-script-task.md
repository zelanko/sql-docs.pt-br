---
title: Detectar um arquivo simples vazio com a tarefa Script | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: extending-packages-scripting-task-examples
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- flat files
- Script task [Integration Services], empty flat files
- SSIS Script task, empty flat files
- Script task [Integration Services], examples
ms.assetid: 1b4defb8-886a-483d-8056-d1b91d37bc90
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2553da2693a51dcec0874a7ba35f919afc1b44a3
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35402198"
---
# <a name="detecting-an-empty-flat-file-with-the-script-task"></a>Detectando um arquivo simples vazio com a tarefa Script
  A origem Arquivo Simples não determina se um arquivo simples contém linhas de dados antes de tentar processá-las. Talvez você queira aumentar a eficácia de um pacote, especialmente de um pacote que itera em diversos arquivos simples, ignorando os arquivos que não contêm linhas de dados. A tarefa Script pode procurar um arquivo simples vazio antes de o pacote começar a processar o fluxo de dados.  
  
> [!NOTE]  
>  Se desejar criar uma tarefa mais fácil de ser reutilizada em vários pacotes, procure utilizar o código desse exemplo de tarefa Script como o ponto inicial de uma tarefa personalizada. Para obter mais informações, consulte [Desenvolvendo uma tarefa personalizada](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="description"></a>Descrição  
 O exemplo a seguir utiliza métodos do namespace **System.IO** para testar o arquivo simples especificado em um gerenciador de conexões de arquivo simples, a fim de determinar se o arquivo está vazio ou se ele contém apenas linhas esperadas que não são de dados, assim como títulos de coluna ou uma linha vazia. O script verifica primeiro o tamanho do arquivo; se o tamanho é zero bytes, o arquivo está vazio. Quando o tamanho do arquivo é maior que zero, o script lê linhas do arquivo até não encontrar mais linhas ou até o número de linhas exceder o número esperado de linhas que não são de dados. Quando o número de linhas no arquivo é menor que ou igual ao número esperado de linhas que não são de dados, o arquivo é considerado vazio. Os resultados são retornados como um valor booliano em uma variável de usuário, cujo valor pode ser usado para criar ramificação no fluxo de controle do pacote. O método **FireInformation** também exibe o resultado na janela de **Saída** do VSTA ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications).  
  
#### <a name="to-configure-this-script-task-example"></a>Para configurar esse exemplo de tarefa Script  
  
1.  Crie e configure um gerenciador de conexões de arquivo simples nomeado **EmptyFlatFileTest**.  
  
2.  Crie uma variável de inteiro nomeada `FFNonDataRows` e defina seu valor como o número de linhas que não são de dados esperadas no arquivo simples.  
  
3.  Crie uma variável booliana nomeada `FFIsEmpty`.  
  
4.  Adicione a variável `FFNonDataRows` à propriedade **ReadOnlyVariables** da tarefa Script.  
  
5.  Adicione a variável `FFIsEmpty` à propriedade **ReadWriteVariables** da tarefa Script.  
  
6.  No seu código, importe o namespace **System.IO**.  
  
 Se você estiver iterando em arquivos com um enumerador de arquivo Foreach, em vez de utilizar um único gerenciador de conexões de arquivos simples, modifique o código de exemplo a seguir para obter o nome e o caminho do arquivo a partir da variável em que o valor enumerado é armazenado, e não do gerenciador de conexões.  
  
### <a name="code"></a>Código  
  
```vb  
Public Sub Main()  
  
  Dim nonDataRows As Integer = _  
      DirectCast(Dts.Variables("FFNonDataRows").Value, Integer)  
  Dim ffConnection As String = _  
      DirectCast(Dts.Connections("EmptyFlatFileTest").AcquireConnection(Nothing), _  
      String)  
  Dim flatFileInfo As New FileInfo(ffConnection)  
  ' If file size is 0 bytes, flat file does not contain data.  
  Dim fileSize As Long = flatFileInfo.Length  
  If fileSize > 0 Then  
    Dim lineCount As Integer = 0  
    Dim line As String  
    Dim fsFlatFile As New StreamReader(ffConnection)  
    Do Until fsFlatFile.EndOfStream  
      line = fsFlatFile.ReadLine  
      lineCount += 1  
      ' If line count > expected number of non-data rows,  
      '  flat file contains data (default value).  
      If lineCount > nonDataRows Then  
        Exit Do  
      End If  
      ' If line count <= expected number of non-data rows,  
      '  flat file does not contain data.  
      If lineCount <= nonDataRows Then  
        Dts.Variables("FFIsEmpty").Value = True  
      End If  
    Loop  
  Else  
    Dts.Variables("FFIsEmpty").Value = True  
  End If  
  
  Dim fireAgain As Boolean = False  
  Dts.Events.FireInformation(0, "Script Task", _  
      String.Format("{0}: {1}", ffConnection, _  
      Dts.Variables("FFIsEmpty").Value.ToString), _  
      String.Empty, 0, fireAgain)  
  
  Dts.TaskResult = ScriptResults.Success  
  
End Sub  
```  
  
```csharp  
public void Main()  
        {  
  
            int nonDataRows = (int)(Dts.Variables["FFNonDataRows"].Value);  
            string ffConnection = (string)(Dts.Connections["EmptyFlatFileTest"].AcquireConnection(null) as String);  
            FileInfo flatFileInfo = new FileInfo(ffConnection);  
            // If file size is 0 bytes, flat file does not contain data.  
            long fileSize = flatFileInfo.Length;  
            if (fileSize > 0)  
            {  
  
                int lineCount = 0;  
                string line;  
                StreamReader fsFlatFile = new StreamReader(ffConnection);  
                while (!(fsFlatFile.EndOfStream))  
                {  
                    Console.WriteLine (fsFlatFile.ReadLine());  
                    lineCount += 1;  
                    // If line count > expected number of non-data rows,  
                    //  flat file contains data (default value).  
                    if (lineCount > nonDataRows)  
                    {  
                        break;  
                    }  
                    // If line count <= expected number of non-data rows,  
                    //  flat file does not contain data.  
                    if (lineCount <= nonDataRows)  
                    {  
                        Dts.Variables["FFIsEmpty"].Value = true;  
                    }  
                }  
            }  
            else  
            {  
                Dts.Variables["FFIsEmpty"].Value = true;  
            }  
  
            bool fireAgain = false;  
            Dts.Events.FireInformation(0, "Script Task", String.Format("{0}: {1}", ffConnection, Dts.Variables["FFIsEmpty"].Value), String.Empty, 0, ref fireAgain);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplos de tarefa Script](../../integration-services/extending-packages-scripting-task-examples/script-task-examples.md)  
  
  
