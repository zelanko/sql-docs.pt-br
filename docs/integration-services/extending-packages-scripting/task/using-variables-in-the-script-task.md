---
title: "Usando variáveis na tarefa Script | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
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
- Foreach Loop containers
- Script task [Integration Services], variables
- scripts [Integration Services], variables
- Variables property
- Variable object
- SSIS Script task, variables
- variables [Integration Services], Script task
ms.assetid: 593b5961-4bfa-4ce1-9531-a251c34e89d3
caps.latest.revision: 63
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ccfd7ce8e8f53d12dac3b021d5f62bd03947413d
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="using-variables-in-the-script-task"></a>Usando variáveis na tarefa Script
  Variáveis possibilitam que a tarefa Script troque dados com outros objetos no pacote. Para obter mais informações, consulte [Integration Services &#40;SSIS&#41; Variables](../../../integration-services/integration-services-ssis-variables.md).  
  
 A tarefa Script usa o <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> propriedade o **Dts** objeto para ler e gravar <xref:Microsoft.SqlServer.Dts.Runtime.Variable> objetos no pacote.  
  
> [!NOTE]  
>  O <xref:Microsoft.SqlServer.Dts.Runtime.Variable.Value%2A> propriedade o <xref:Microsoft.SqlServer.Dts.Runtime.Variable> classe é do tipo **objeto**. Como a tarefa de Script foi **Option Strict** habilitado, você deve converter o <xref:Microsoft.SqlServer.Dts.Runtime.Variable.Value%2A> propriedade para o tipo apropriado antes de você pode usá-lo.  
  
 Você adiciona variáveis existentes para o <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadOnlyVariables%2A> e <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadWriteVariables%2A> listas no **Editor da tarefa Script** para disponibilizá-los para o script personalizado. Lembre-se de que os nomes de variáveis diferenciam maiúsculas de minúsculas. Dentro do script, você acessa variáveis de ambos os tipos através de <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> propriedade o **Dts** objeto. Use o **valor** propriedade de leitura e gravação em variáveis individuais. A tarefa Script gerencia de forma transparente o bloqueio à medida que o script lê e modifica os valores de variáveis.  
  
 Você pode usar o método <xref:Microsoft.SqlServer.Dts.Runtime.Variables.Contains%2A> da coleção <xref:Microsoft.SqlServer.Dts.Runtime.Variables> retornada pela propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> para verificar a existência de uma variável antes de usá-la no seu código.  
  
 Você também pode usar o <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A> propriedade (Dts.VariableDispenser) para trabalhar com variáveis na tarefa Script. Ao usar o <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A>, você deve tratar as semânticas de bloqueio e a conversão de tipos de dados para obter valores variáveis em seu próprio código. Talvez seja necessário usar a propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A> em vez da propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> para trabalhar com uma variável que não está disponível no tempo de design mas é criada programaticamente no tempo de execução.  
  
## <a name="using-the-script-task-within-a-foreach-loop-container"></a>Usando a tarefa Script dentro de um contêiner Loop Foreach  
 Quando uma tarefa Script é executada repetidas vezes dentro de um contêiner Loop Foreach, em geral o script precisa trabalhar com o conteúdo do item atual no enumerador. Por exemplo, ao usar o enumerador de Arquivo Foreach, o script precisa saber o nome do arquivo atual; ao usar o enumerador ADO Foreach, o script precisa saber o conteúdo das colunas da linha de dados atual.  
  
 As variáveis possibilitam essa comunicação entre o contêiner Loop Foreach e a tarefa Script. Sobre o **mapeamentos de variáveis** página do **Editor de Loop Foreach**, atribuir variáveis para cada item de dados que são retornados por um único item enumerado. Por exemplo, um enumerador de Arquivo Foreach retorna apenas um nome de arquivo no Índice 0 e, portanto, requer apenas um mapeamento de variável, enquanto um enumerador que retorna várias colunas de dados em cada linha requer o mapeamento de uma variável diferente para cada coluna a ser usada na tarefa Script.  
  
 Após mapear itens enumerados para variáveis, em seguida, você deve adicionar as variáveis mapeadas para o **ReadOnlyVariables** propriedade o **Script** página do **Editor da tarefa Script** para disponibilizá-las para o seu script. Para obter um exemplo de uma tarefa de Script em um contêiner de Foreach Loop que processa os arquivos de imagem em uma pasta, consulte [trabalhando com imagens com a tarefa de Script](../../../integration-services/extending-packages-scripting-task-examples/working-with-images-with-the-script-task.md).  
  
## <a name="variables-example"></a>Exemplo de variáveis  
 O exemplo a seguir demonstra como acessar e usar variáveis em uma tarefa Script para determinar o caminho do fluxo de trabalho do pacote. O exemplo supõe que você criou variáveis de inteiro nomeadas `CustomerCount` e `MaxRecordCount` e adicioná-las para o **ReadOnlyVariables** coleção no **Editor da tarefa Script**. A variável `CustomerCount` contém o número de registros de cliente a serem importados. Se seu valor for maior que o valor de `MaxRecordCount`, a tarefa Script reportará uma falha. Quando uma falha ocorre porque o limite de `MaxRecordCount` foi excedido, o caminho de erro do fluxo de trabalho pode implementar qualquer limpeza exigida.  
  
 Para compilar o exemplo com êxito, adicione uma referência ao assembly Microsoft.SqlServer.ScriptTask.  
  
```vb  
Public Sub Main()  
  
    Dim customerCount As Integer  
    Dim maxRecordCount As Integer  
  
    If Dts.Variables.Contains("CustomerCount") = True AndAlso _  
        Dts.Variables.Contains("MaxRecordCount") = True Then  
  
        customerCount = _  
            CType(Dts.Variables("CustomerCount").Value, Integer)  
        maxRecordCount = _  
            CType(Dts.Variables("MaxRecordCount").Value, Integer)  
  
    End If  
  
    If customerCount > maxRecordCount Then  
            Dts.TaskResult = ScriptResults.Failure  
    Else  
            Dts.TaskResult = ScriptResults.Success  
    End If  
  
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
        int customerCount;  
        int maxRecordCount;  
  
        if (Dts.Variables.Contains("CustomerCount")==true&&Dts.Variables.Contains("MaxRecordCount")==true)  
  
        {  
            customerCount = (int) Dts.Variables["CustomerCount"].Value;  
            maxRecordCount = (int) Dts.Variables["MaxRecordCount"].Value;  
  
        }  
  
        if (customerCount>maxRecordCount)  
        {  
            Dts.TaskResult = (int)ScriptResults.Failure;  
        }  
        else  
        {  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
  
    }  
  
}  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Integration Services &#40; SSIS &#41; Variáveis](../../../integration-services/integration-services-ssis-variables.md)   
 [Usar variáveis em pacotes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)  
  
  
